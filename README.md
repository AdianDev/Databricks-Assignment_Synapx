# Databricks-Assignment_Synapx
Assignment





Gold layer ER model preview: 
erDiagram
    DIM_PATIENT ||--o{ FACT_ENCOUNTER : has
    DIM_PATIENT ||--o{ FACT_CONDITION : has
    DIM_PATIENT ||--o{ FACT_OBSERVATION : has
    DIM_ENCOUNTER ||--o{ FACT_ENCOUNTER : relates

    DIM_PATIENT {
        string patient_key PK
        string patient_id
        string gender
        string birth_date
        string city
        string state
        string country
    }

    FACT_ENCOUNTER {
        string encounter_key PK
        string patient_key FK
        string status
        string period_start
        string period_end
    }

    FACT_CONDITION {
        string condition_id PK
        string patient_key FK
        string encounter_key FK
        string condition_text
        boolean is_current
    }

    FACT_OBSERVATION {
        string observation_id PK
        string patient_key FK
        string encounter_key FK
        string value_quantity
        string loinc_code
    }

    DIM_ENCOUNTER {
        string encounter_key PK
        string encounter_id
        string organization
    }
                    ┌───────────────────┐
                    │    dim_patient    │
                    │-------------------│
                    │ patient_key (PK)  │
                    │ patient_id        │
                    │ gender            │
                    │ birth_date        │
                    │ city              │
                    │ state             │
                    │ country           │
                    │ ...               │
                    └─────────┬─────────┘
                              │
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
┌───────▼────────┐   ┌────────▼────────┐   ┌────────▼────────┐
│ fact_encounter │   │ fact_condition  │   │ fact_observation│
│----------------│   │-----------------│   │-----------------│
│ encounter_key  │   │ condition_id    │   │ observation_id  │
│ patient_key FK │   │ patient_key FK  │   │ patient_key FK  │
│ status         │   │ encounter_key FK│   │ encounter_key FK│
│ period_start   │   │ condition_text  │   │ value_quantity  │
│ period_end     │   │ is_current      │   │ loinc_code      │
└────────┬───────┘   └────────┬────────┘   └────────┬────────┘
         │                    │                     │
         └──────────────┬─────┴──────────────┬──────┘
                        │                    │
                  ┌─────▼─────────┐
                  │ dim_encounter │
                  │---------------│
                  │ encounter_key │
                  │ encounter_id  │
                  │ organization  │
                  └───────────────┘
