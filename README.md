# fairness-pipeline-toolkit

config.yml → run_pipeline.py → MLflow
       ↙ ↘
Measurement Debias+Train+Validate


config.yml          → reads settings (DisparateImpactRemover, threshold 0.1)
       ↓
run_pipeline.py     → main script that runs 3 steps:
       ↙                   ↘
1. Measurement    2. Debias+Train    3. Validate
(Baseline bias)     (Fix data+model)   (Check PASS/FAIL)
       ↓
MLflow              → saves results (accuracy, fairness score, model file)



┌─────────────────┐    ┌──────────────────┐    ┌──────────┐
│   config.yml    │───▶│  run_pipeline.py │───▶│  MLflow  │
│                 │    │                  │    │          │
│ • Preprocessor  │    │ • Step 1: Measure│    │ • Metrics│
│ • Trainer       │    │ • Step 2: Debias │    │ • Model  │
│ • Threshold     │    │ • Step 3: Validate│   │ • Config │
└─────────────────┘    └──────────────────┘    └──────────┘
                              │
                       ┌──────────────┐
                       │   RESULTS    │
                       │ Accuracy: 0.82│
                       │ Fairness: 0.05│
                       └──────────────┘
