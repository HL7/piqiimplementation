### Consensus PIQI Instances

To support broad interoperability and repeatable benchmarking, PIQI publishes consensus instances that are community-vetted and intended for common baseline use across implementations. These artifacts pair a shared PIQI model with a corresponding evaluation rubric so organizations can evaluate data quality using consistent structure and scoring logic.

#### Clinical Data Model

- **File:** [PAT_CLINICAL_V1.json](PAT_CLINICAL_V1.json)
- **Role in consensus baseline:** Defines the canonical patient-centered PIQI model used as the reference structure for community-aligned clinical quality evaluation.
- **What it captures:**
	- Fifteen data classes spanning core clinical content domains, including demographics, allergies, conditions, immunizations, labs, imaging, medications, procedures, vitals, devices, health assessments, documents, encounters, goals, and provider information.
	- Attribute-level definitions (for example, codeable concepts and simple attributes), role metadata (for example, start/end datetime semantics), cardinality expectations, and remediation weighting by data class.
- **Why it is consensus-relevant:** Establishes a common structural target for PIQI implementations so quality checks and score interpretation are performed against the same clinical data model assumptions.

#### Clinical Data Evaluation Rubric

- **File:** [USCDI_v3_1.json](USCDI_v3_1.json)
- **Role in consensus baseline:** Provides the shared USCDI-inspired evaluation rubric that operationalizes data quality checks for the clinical model.
- **What it captures:**
	- A sequenced criteria set (66 total checks) with predominantly scoring rules, plus informational checks.
	- Concrete SAM-driven validation logic across entities, including terminology membership checks (for example, LOINC, SNOMED-CT, RxNorm, ICD-10-CM), value set/list validation, conditional checks, and temporal validity rules such as past-date validation.
	- Criterion-level scoring controls such as weighting and criticality to standardize how failures contribute to quality outcomes.
- **Why it is consensus-relevant:** Creates a widely reusable, transparent scoring baseline so different PIQI adopters can evaluate similar clinical datasets with consistent criteria and comparable results.

### Schema Artifacts

To support consistent evaluation across PIQI implementations, each core PIQI component adheres to a specific json schema. These schemas define the structure of the modular PIQI components and the resulting data quality scoring responses.

#### Evaluation Report Schema

- **File:** [evaluationreport.json](evaluationreport.json)
- **Purpose:** Defines the shape of a PIQI scoring response payload (`PIQXLResponse`) returned after an evaluation run.
- **What it includes:**
	- Run-level status metadata such as `succeeded`, `errorMessage`, and elapsed processing time.
	- A `scoringData` object with source identifiers, rubric metadata, and processing timestamp.
	- Aggregated scoring outputs at multiple levels, including message-level totals, per-data-class results, informational results, and detection counts.
	- Optional audited message content.
- **How it supports PIQI:** Provides a consistent output contract for communicating pass/fail-derived scoring and quality findings across implementations.

#### Rubric Schema

- **File:** [rubric.json](rubric.json)
- **Purpose:** Defines the structure of an evaluation rubric that organizes SAMs into a scored set of criteria for a specific model and source.
- **What it includes:**
	- Rubric identity and governance metadata (`name`, `mnemonic`, `description`, `version`, `authorityName`).
	- Model and source references that bind the rubric to a PIQI model context.
	- A sequenced `criteria` collection with SAM linkage (`samMnemonic`), conditional logic hooks, scoring effect/weight, criticality flag, and parameterization.
- **How it supports PIQI:** Encodes the use-case-oriented evaluation logic described in the PIQI framework, enabling repeatable, configurable scoring behavior.

#### SAM Schema

- **File:** [sam.json](sam.json)
- **Purpose:** Defines the structure of a Simple Assessment Module (SAM), the atomic reusable quality check in PIQI.
- **What it includes:**
	- SAM identity and descriptive fields (`mnemonic`, `name`, `description`, `failName`).
	- Execution context metadata including dimension alignment (`hdqtDimensionMnemonic`), execution type, data type, and timestamps.
	- Optional prerequisite and conditional SAM references for composing assessment logic.
	- PIQI model/source linkage and SAM parameter definitions.
- **How it supports PIQI:** Standardizes how individual quality checks are represented so they can be shared, parameterized, and assembled into higher-level rubrics.

