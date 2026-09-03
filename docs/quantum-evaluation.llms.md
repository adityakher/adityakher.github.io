# Evaluating Quantum Technologies for Mission Use

Government and enterprise customers evaluating quantum hardware face a recurring problem: vendor claims are stated in the language of physics, while procurement decisions are made in the language of readiness, sustainment, and budget cycles. This page presents a framework for translating between the two. It scores any quantum device class — sensors, networking hardware, or processors — along five axes: delta against the classical incumbent, survival of the operational envelope, integration and logistics burden, deployment readiness on a five-level ladder, and vendor viability. Each assessment terminates in one of five dispositions, paired with a revisit trigger. We claim that technical assessment necessary is but not sufficient, and that the transition path — acquisition vehicle, accreditation, sustainment, workforce — is what makes a recommendation actionable.

[Download slide deck (PDF)](files/quantum-evaluation/quantum-tech-evaluation.pdf)

## Motivation

We aim not to pick winners in quantum R&D, but to prevent three specific mistakes:

| Failure mode | What it looks like | Cost |
|----|----|----|
| **Buying too early** | A device that works in a lab and not on a platform | Money, credibility, a soured customer |
| **Buying the wrong thing** | A QKD procurement when the actual problem is PQC migration | Solves nothing, consumes budget |
| **Missing the window** | Deployable tech exists and no one advocated for it in the POM | A capability gap that takes years to close |

Everything below is in service of separating these three cases. Vendors sell devices, while customers are looking for outcomes under constraints. Technology evaluation is the translation layer between them, and its most valuable output is often saying “not yet.”

## Approach

These apply to all three device classes. The class-specific sections that follow are the same five axes with different discriminators.

### 1. Classical baseline delta

*What does this replace, and what is the delta against the best classical alternative at comparable SWaP and cost?*

This question disqualifies most candidates immediately. Every quantum device competes against a mature classical incumbent: chip-scale atomic clocks, navigation-grade FOG and RLG inertial units, existing gravimeters, HPC. A vendor who cannot state their classical baseline honestly, or who benchmarks against a strawman, has told you something important about the rest of their claims.

### 2. Survival of the operational envelope

Lab sensitivity is not fielded performance. Quantum sensors are exquisitely sensitive, often to exactly the things its operational platform would supply: vibration, magnetic fields, thermal gradients, EMI. Vendor artifacts that should be examined include environmental test data, drift and bias stability over mission duration, warm-up time, duty cycle, and behavior under motion. If these don’t exist, the technology is likely too immature to consider.

### 3. Integration and logistics burden

*What does it take to keep this running in year four?*

Depending on the technology, considerations can include cryogenics and the helium supply chain, laser alignment and replacement, vacuum systems, calibration cadence, power, floor loading, EMI, facility modification, etc. Further, a training pipeline must exist to keep all of these systems in order. Especially for government customers with decade(s)-long program sustainments, these burdens must be carefully accounted for.

### 4. Deployment readiness

Rather than TRL, which can be subjective, we provide an alternate ladder:

| Level  | Definition                                      |
|--------|-------------------------------------------------|
| **L1** | Lab demonstration                               |
| **L2** | Engineered prototype                            |
| **L3** | Ruggedized unit, environmental testing complete |
| **L4** | Field trial with a real user                    |
| **L5** | Sustained operational use with a logistics tail |

Most quantum sensing sits at L2–L3, while most quantum networking sits at L1–L2. QPUs are at L5 as a cloud service and L1 as customer-owned infrastructure.

### 5. Vendor and supply-chain viability

What is the vendor’s funding runway and revenue mix? For government customers, things like single-source components, FOCI/ITAR/EAR posture, foreign ownership, long-term lifecycle support, and IP position are potential risks. A technically superior device from a vendor who will not exist in ten years is the wrong buy.

## Application

> **IMPORTANT:**
>
> The class-level assessments below reflect the technology landscape as of **September 2026**. Named companies are illustrative of categories and not endorsements.

### Quantum sensing

This is the only category with credible L3–L4 systems today. Separates into PNT (clocks, inertial), RF sensing (Rydberg), magnetometry (OPM, NV, SQUID), gravimetry and gradiometry, and imaging.

Discriminators that matter more than sensitivity:

- **Bias stability and drift over mission duration.** A GPS-denied navigation solution that needs periodic external fixes is not a mission solution at all. Instantaneous sensitivity is the wrong figure of merit.
- **Environmental hardening**, per Axis 2, and usually the binding constraint.
- **What the product actually is.** For magnetic-anomaly navigation the sensor is arguably the easy part; the map, the platform-noise separation, and the algorithm are what adds the most value.

**Illustrative vendors:**

- Vector Atomic (rack-mounted optical clocks with at-sea trials)
- Infleqtion (clocks and Rydberg RF sensing)
- Q-CTRL (software-layer quantum-assured navigation)
- AOSense and Exail (inertial and gravimetry)
- SandboxAQ (magnetic-anomaly navigation as a sensor-plus-data-product play).

**Typical disposition:** *Pilot* on selected PNT applications.

### Quantum networking

Triage into three buckets that often get confused:

| Bucket | Status | Customer answer |
|----|----|----|
| **PQC migration** | Standards published and mandated | Real work, today |
| **QKD** | Not endorsed for national security systems | Requires extraordinary justification |
| **Entanglement distribution, repeaters, memories, transduction** | Research | Monitor; participate in testbeds |

Directing a customer from QKD to PQC, if it’s the appropriate solution, can save them a lot of money.

Physical constraints worth considering:

- Fiber loss of roughly 0.2 dB/km at telecom wavelengths caps repeaterless links to the 100–200 km class.
- Without functioning repeaters and quantum memories, a “quantum network” is a set of point-to-point links joined by trusted nodes, which reintroduces the trust assumption the architecture is typically sold as removing.
- Quantum channels generally cannot traverse existing amplified, switched telecom infrastructure. Dark fiber is a hard dependency, and in many cases difficult to guarantee.

Regarding component maturity: SNSPDs are commercially mature, sources are maturing, memories and microwave-optical transducers are research, repeaters are still being developed. Distributed sensing and precision time transfer, on the other hand, is available near-term, though even there classical optical two-way time transfer performs well.

**Typical disposition:** *Monitor*, with selective testbed engagement.

### Quantum computing

The headline recommendation for nearly every customer is “access, don’t acquire:” cloud or hosted access, with owned hardware justified only by a specific research mission. The facility burden alone (refrigeration, helium-3 supply, power, vibration, EMI, floor loading) is often underestimated.

Beyond physical qubit count, look at:

- Two-qubit gate fidelity, with benchmarking methodology stated
- Logical qubit count, and the physical error rate the roadmap assumes
- Connectivity, gate speed, mid-circuit measurement, reset
- Error-correction trajectory: distance to threshold, demonstrated below-threshold scaling
- Benchmarks published against the best classical method: quantum-inspired and HPC methods have repeatedly closed claimed advantages.

Current maturity stage does not mean ultimate promise. Superconducting qubits offer fast gates with heavy cryogenic infrastructure; trapped ions the highest fidelities and all-to-all connectivity but with slow gates; neutral atoms have a strong scaling story; photonic qubits have attractive operating conditions but loss limits; spin qubits provide a CMOS manufacturability path at an earlier stage; topological qubits are a high risk/high reward technology still in foundational stages.

Where to spend money instead: workforce development, algorithm and use-case readiness, benchmarking discipline, and cryptographic inventory work.

**Typical disposition:** *Access + Monitor.* If appropriate, revisit acquisition when a vendor demonstrates a specific logical-qubit threshold against a customer-relevant problem.

## Result

Assessments terminate in one of five dispositions, each with a revisit trigger:

> **Acquire · Pilot · Access (don’t acquire) · Monitor · Pass**
>
> *Example: pass on QKD for this enclave; revisit if agency guidance changes, or if a repeater-based architecture removes the trusted-node assumption.*

Capability and maturity are necessary but not sufficient. A recommendation is not actionable for a government customer until it addresses the acquisition path, accreditation, facility and/or SCIF constraints, sustainment framework, training pipeline, supply chain (covering FOCI, ITAR and EAR, and single-source risk), budget reality (given that POM cycles mean a three-year technology must be advocated for while the window is open), and workforce (*i.e.*, whether the customer can operate the platform themselves).

## Scope and Limitations

This framework is a screening and triage instrument, and depends on existing vendor-provided test and evaluation data. It assumes a customer whose procurement operates on federal timelines and accreditation requirements; commercial buyers face a different constraint set, particularly around Axis 3. The class-level assessments are subject to change as technologies mature, but the five evaluation axes and the transition-path layer should outlast any particular vendor/technology landscape.
