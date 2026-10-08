# Hospital Appointment Scheduling — Single-Agent Baseline

## Project Purpose

This repository contains the **Single-Agent baseline** for the Hospital Appointment Scheduling project. It is the reference system that will later be compared with the Multi-Agent System (MAS) under the same environments, constraints, inputs, dynamic events, random seeds, and evaluation metrics.

There are two notebooks, but **only one scheduling implementation**:

- `Hospital_Appointment_Scheduling_FULL_PROJECT.ipynb` → the complete research baseline containing both experiments.
- `M4_Single_Agent_Baseline.ipynb` → a simplified 5-minute live-demo view of the **same Easy / Static code** from the full notebook. It is not a third implementation.

## M4 Requirements Coverage

### C4.1 — Live Demo: End-to-End Task

The baseline completes a full scheduling task from synthetic hospital data generation through scheduling, validation, evaluation, and saved outputs.

For the 5-minute demonstration, use `M4_Single_Agent_Baseline.ipynb`. Its final verification block reports:

- Total requests: 100
- Scheduled: 100
- Unscheduled: 0
- Constraint violations: 0
- Assignment rate: 100.00%
- Baseline valid: True

### C4.2 — Fair and Well-Configured Baseline

The Single-Agent baseline is a centralized scheduler using synthetic appointment requests and explicitly defined scheduling constraints.

**Environment 1 — Easy / Static**
- 20 doctors
- 10 specialties
- 100 appointment requests
- 6 scheduling days
- 60-minute slots
- 09:00–17:00 working hours
- No dynamic events

**Environment 2 — Complex / Dynamic**
- 40 doctors
- 2,200 patients
- 3,298 initial appointment requests
- 21 scheduling days
- 30-minute base slots
- 30- and 60-minute appointments
- Doctor daily appointment and daily-minute capacity constraints
- 290 dynamic events:
  - 100 patient cancellations
  - 40 doctor unavailability events
  - 120 new appointment requests
  - 30 doctor schedule changes

The 40 doctor-unavailability events are anchored to appointments from the initial baseline schedule, and the notebook verifies that every generated unavailability event overlaps an initial appointment. This ensures that recovery is tested against actual scheduled disruptions rather than events that affect no appointment.

The final schedule is revalidated after the dynamic events. The executed baseline produced zero final constraint violations.

### C4.3 — Repository and README

A third party can run the notebooks using Python/Jupyter or Google Colab. The required dependencies are listed in `requirements.txt`, and the setup steps are provided below.

## Results Summary

### Experiment 1 — Easy / Static

| Metric | Result |
|---|---:|
| Appointment requests | 100 |
| Scheduled | 100 |
| Unscheduled | 0 |
| Assignment rate | 100.00% |
| Constraint violations | 0 |
| Preferred doctor satisfaction | 95.24% |
| Preferred date satisfaction | 76.00% |
| Preferred time satisfaction | 100.00% |
| Average date deviation | 0.27 days |
| Maximum date deviation | 2 days |

### Experiment 2 — Complex / Dynamic

Initial static baseline:

| Metric | Result |
|---|---:|
| Appointment requests | 3,298 |
| Scheduled | 3,113 |
| Unscheduled | 185 |
| Assignment rate | 94.39% |
| Constraint violations | 0 |
| Doctor capacity utilization | 74.74% |

After 290 dynamic events:

| Metric | Result |
|---|---:|
| Final active requests | 3,318 |
| Final scheduled appointments | 3,107 |
| Unscheduled active requests | 211 |
| Assignment rate | 93.64% |
| New request scheduling rate | 78.33% |
| Constraint violations | 0 |
| Event success rate | 91.03% |
| Affected appointments | 270 |
| Recovered appointments | 170 |
| Overall recovery rate | 62.96% |

For existing-appointment disruptions specifically:
- Doctor unavailability: 67 affected, 67 recovered (100% recovery)
- Doctor schedule change: 103 affected, 103 recovered (100% recovery)

The 26 failed dynamic events are unscheduled new appointment requests caused by insufficient available resources; they are not constraint violations.

## Reproducibility and Fair Comparison

The baseline uses fixed random seeds for reproducible synthetic environments and event generation. The future MAS evaluation should use the **same generated inputs, constraints, event sequence, random seeds, and evaluation metrics** when comparing against this Single-Agent baseline.

This keeps the comparison focused on the scheduling architecture rather than differences in test cases.

## How to Run

### Google Colab

1. Open the desired `.ipynb` file in Google Colab.
2. Select **Runtime → Run all**.
3. The full notebook runs both experiments.
4. The M4 notebook runs only the Easy / Static experiment and its final verification block.

### Local Jupyter

```bash
pip install -r requirements.txt
jupyter notebook
```

Then open the desired notebook and run all cells.

## Repository Structure

```text
Hospital-Appointment-Scheduling/
├── Hospital_Appointment_Scheduling_FULL_PROJECT.ipynb
├── M4_Single_Agent_Baseline.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Notebook Relationship — Important

`M4_Single_Agent_Baseline.ipynb` is derived directly from the beginning of `Hospital_Appointment_Scheduling_FULL_PROJECT.ipynb`.

The Easy / Static scheduling code and the M4 end-to-end verification code are copied **unchanged** from the full notebook. The M4 notebook only omits Experiment 2 so that the live demonstration can fit within five minutes.

Therefore, there is **no separate third scheduling implementation** to maintain.

If the Easy / Static baseline code is changed later, update the canonical section in the full notebook first and regenerate the M4 notebook from that section.

## Project Scope Beyond M4

M4 establishes the working Single-Agent baseline. The complete project uses the full notebook as the reference implementation for the later Single-Agent vs Multi-Agent comparison across the Easy / Static and Complex / Dynamic environments.
