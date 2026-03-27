# NYSC Portal Performance Study (AWS Simulation)

This repository contains an independent cloud performance study simulating real-world behavior of a public service portal under load.

The project models how fixed infrastructure fails under pressure and how an elastic AWS architecture improves system performance.

---

## Overview

The study is divided into two controlled phases:

* Phase A → Fixed, single-instance environment
* Phase B → Elastic, load-balanced environment

Both environments run the same backend logic to ensure fair comparison.

---

## Repository Structure

```id="3p0gk2"
NYSC WHITEPAPER/
├── CHAPTER 3.pdf
├── PHASE 1.docx
├── PHASE3_AWS_GUIDE.docx
├── method.txt
│
├── AWS SIMULATION/
│   ├── AUDIT_LOG.txt
│   ├── RECOVERY_TEST.PNG
│   ├── stress_test.PNG
│   └── 01_PHASE_A/
│       └── phase_a_results.tsv
│
├── NYSC_AUDIT_12MAR2026/
│   ├── lighthouse/
│   ├── traceroute/
│   ├── headers/
│   ├── har/
│   └── screenshots/
```

---

## Problem

Public service systems often fail during peak demand due to:

* single-server bottlenecks
* lack of load distribution
* poor recovery after traffic spikes

This study reproduces those conditions in a controlled environment.

---

## Experimental Setup

### Phase A — Control

* Single EC2 instance
* Apache + PHP
* Simulated delay using `usleep()`
* No load balancing

---

### Phase B — Elastic

* Application Load Balancer (ALB)
* Auto Scaling Group (2–5 instances)
* Multi-AZ deployment
* Same backend logic

---

## Load Testing

Tool used: ApacheBench (`ab`)

* 10,000 requests
* High concurrency stress
* Recovery testing after load

---

## Results

### Phase A

* Mean latency: 2,458 ms
* Max latency: 66,522 ms
* Throughput: ~40 rps
* No recovery after load

---

### Phase B

* Mean latency: 1,200 ms
* Max latency: 5,083 ms
* Throughput: ~41 rps
* Stable response distribution

---

## Key Findings

* Load balancing reduced connection delay from ~977 ms to ~1 ms
* Tail latency improved significantly (66s → 5s)
* Elastic architecture improves stability, not just speed
* Recovery issues persist due to application-level constraints

---

## CloudWatch Insights

* CPU usage remained low (~21%)
* No scaling triggered
* Reason: workload simulated I/O delay, not CPU load

---

## Research Contribution

This work combines:

* forensic audit data
* controlled AWS simulation
* empirical performance validation

It shows that:

* infrastructure design directly impacts user experience
* elastic systems improve reliability even without scaling events

---

## Notes

* This is an independent research project
* Not affiliated with NYSC
* Designed for educational and engineering analysis

---

## Author

Daniel Akinrinmade
