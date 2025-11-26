# 🦆 DGCP™ Indexing Layer Specification v1.0.0  
### Open, Federated, Read-Optimized Access to the Global Proof Registry

The DGCP Indexing Layer provides a **read-optimized view** of the  
Global Proof Registry (GPR) for auditors, researchers, regulators,  
and public institutions.

It does **not** replace the GPR.  
It is an optional, open-source mirror that anyone can run.

---

## 1. Purpose of the Indexing Layer

The Indexing Layer exists to:

1. Make it easy to **query** DGCP proofs at scale  
2. Allow third parties to run their own **independent index**  
3. Avoid centralization of query power in a single operator  
4. Provide fast filters (by date, location_label, work_type, tags, etc.)  
5. Keep all write-authority in the original GitHub + DLT registry

The Indexing Layer is **read-only** by design.

---

## 2. Design Principles

1. **Open-Source Default**  
   – Client code and DB schema must be public.  
2. **Federated Deployment**  
   – Any auditor, NGO, university, or government may run their own instance.  
3. **Read-Only Access**  
   – No component can modify the original proofs.  
4. **Deterministic Rebuild**  
   – Any index must be fully reconstructible from the GPR.  
5. **No Hidden APIs**  
   – No private backdoors or proprietary endpoints.  

---

## 3. High-Level Architecture

The Indexing Layer follows a simple 3-step pipeline:

1. **Clone / Pull** from the DGCP Global Proof Registry (Git repository)  
2. **Parse & Validate** DMS metadata files  
3. **Index** into a read-optimized database (e.g., PostgreSQL)

Optional API layer:
- REST / GraphQL / simple HTTP read endpoints

---

## 4. Canonical Data Model (Database Schema)

A minimal relational schema (e.g., PostgreSQL) is recommended:

### 4.1. Table: `proofs`

| Column              | Type           | Description                           |
|---------------------|----------------|---------------------------------------|
| id                  | SERIAL / INT   | Local DB key                          |
| proof_id            | TEXT (unique)  | DMS `proof_id`                        |
| dms_version         | TEXT           | DMS version                           |
| worker_id_public    | TEXT           | Public key                            |
| timestamp_utc       | TIMESTAMPTZ    | UTC timestamp                         |
| timestamp_local     | TIMESTAMPTZ    | Local timestamp (approx)              |
| location_label      | TEXT           | Coarse location                       |
| work_type           | TEXT           | Work category                         |
| short_description   | TEXT           | Human description                     |
| ipfs_cid_primary    | TEXT           | Primary IPFS CID                      |
| git_repo_url        | TEXT           | Registry repo URL                     |
| git_commit_sha256   | TEXT           | Git commit hash                       |
| ots_timestamp_ref   | TEXT           | OTS / Bitcoin reference               |
| raw_metadata_path   | TEXT           | File path inside repo                 |
| inserted_at         | TIMESTAMPTZ    | When indexed                          |
| updated_at          | TIMESTAMPTZ    | Last re-index time                    |

### 4.2. Table: `proof_tags`

| Column     | Type         | Description              |
|-----------|--------------|--------------------------|
| id        | SERIAL / INT | Local key                |
| proof_id  | TEXT         | Foreign key to proofs    |
| tag       | TEXT         | Single tag value         |

Composite index recommended on `(tag, proof_id)`.

### 4.3. Table: `daily_roots`

| Column          | Type         | Description                     |
|-----------------|--------------|---------------------------------|
| date_utc        | DATE         | Day (UTC)                       |
| root_sha256     | TEXT         | Daily root hash                 |
| ots_ref         | TEXT         | OTS / Bitcoin TXID / proof ref  |
| registry_commit | TEXT         | Optional reference commit       |

---

## 5. Indexing Process

### Step 1 – Repository Sync

- `git clone` or `git pull` the GPR repository  
- Never write to this repo; it is read-only for the indexer

### Step 2 – Discovery

- Scan `/proofs/YYYY/MM/` directories  
- Detect new or changed DMS files  
- Keep a local pointer/marker for last indexed commit

### Step 3 – Validation

For each proof:

- Parse JSON/YAML  
- Optionally re-run **Validator** (Machine-Critical checks)  
- If invalid → log + skip, but do not modify registry  

### Step 4 – Insert / Update

- Insert new rows in `proofs` and `proof_tags`  
- Ensure `proof_id` uniqueness  
- Mark timestamps for rebuild traceability  

---

## 6. Read-Only API (Optional)

A reference implementation MAY expose:

### Example Endpoints:

- `GET /proofs?date=YYYY-MM-DD`  
- `GET /proofs?location_label=MaMeeFarm`  
- `GET /proofs?work_type=duck_care`  
- `GET /proofs?tag=weather:cold`  
- `GET /proofs/{proof_id}`  

Security note:  
- No authentication is required for read-only public endpoints  
- Rate limiting MAY be applied to avoid abuse  

---

## 7. Independence & Federation

DGCP requires that:

- Indexing Layer instances **MUST NOT** be controlled by a single actor  
- Anyone can run an indexer from the open-source client + schema  
- No instance can become a central “gatekeeper” of truth  

The original registry (Git + DLT) always remains the source of truth.

---

## 8. What the Indexing Layer MUST NOT Do

To avoid power concentration:

- MUST NOT write back to the GPR  
- MUST NOT alter proofs  
- MUST NOT hide or censor valid proofs  
- MUST NOT apply hidden ranking or scoring  
- MUST NOT run ML-based “quality filters” on worker content  

Indexes are **mirrors**, not judges.

---

## 9. Rebuild & Portability

Any Indexing Layer instance MUST be:

- Fully rebuildable from scratch  
- Independent of proprietary cloud features  
- Portable to on-premises environments  
- Able to run on modest hardware (e.g., a basic VPS)

This allows small NGOs, universities, and local auditors to participate fairly.

---

## 10. License

The Indexing Layer Specification is governed by:  
**MMFARM-POL-2025 License**  
with **CC BY-NC 4.0** compatibility.

