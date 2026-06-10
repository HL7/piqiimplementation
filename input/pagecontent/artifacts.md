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

