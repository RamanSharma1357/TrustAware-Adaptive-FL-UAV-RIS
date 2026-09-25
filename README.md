Author name: Raman Sharma ,
NIT Kurukshetra
"Trust-Aware Adaptive Federated Learning Under Non-IID and
Time-Varying Channels for Energy-Aware UAV-RIS-Assisted
6G Networks."

# Trust-Aware Adaptive Federated Learning for UAV-RIS-Assisted Wireless Networks

MATLAB implementation for the research paper:

**“Trust-Aware Adaptive Federated Learning Under Non-IID and Time-Varying Channels for Energy-Aware UAV-RIS-Assisted 6G Networks”**

The repository contains a MATLAB R2024a, toolbox-free simulation framework for studying trust-aware adaptive federated learning in UAV-RIS-assisted wireless environments under non-IID data, UAV mobility, time-varying channels, malicious model updates, communication reliability, and energy constraints.

> **Important:** The simulation is designed as a lightweight research-oriented UAV-RIS wireless model motivated by 6G applications. It does not implement a complete 6G protocol stack or standardized 6G air interface.

---

## Features

The V4.3 implementation includes:

- Trust-aware adaptive federated learning
- Strong non-IID local datasets
- UAV mobility
- Time-varying Channel State Information (CSI)
- Temporally correlated wireless channels
- UAV-RIS-assisted wireless propagation
- Channel-dependent RIS phase optimization
- 2-bit quantized RIS phase shifts
- Malicious UAV/model-update attacks
- Label-free anomaly detection
- Trust and communication reliability estimation
- Energy-aware aggregation
- Local model accuracy evaluation
- Progressive aggregation ablation
- Monte-Carlo evaluation
- Paired attack-scenario comparison
- Communication-overhead analysis
- Convergence analysis
- RIS-assisted sum-rate evaluation
- Energy-efficiency evaluation

---

## Aggregation Methods

Five aggregation strategies are evaluated progressively:

1. **FedAvg**
2. **Trust-FL**
3. **Trust+Channel**
4. **Trust+Channel+Energy**
5. **Full Proposed**

The Full Proposed method combines:

- UAV trust
- Channel quality
- Local model accuracy
- Residual energy
- Data quality
- Communication reliability
- Label-free anomaly gating

---

## Simulation Configuration

The default V4.3 configuration uses:

| Parameter | Value |
|---|---:|
| Number of UAVs | 10 |
| Number of ground users | 100 |
| RIS elements | 128 |
| Features | 8 |
| Local samples/UAV | 300 |
| FL rounds | 80 |
| Local epochs | 3 |
| Batch size | 32 |
| Monte-Carlo runs | 8 |
| Malicious UAV ratios | 0%, 10%, 20%, 30% |
| Carrier frequency | 28 GHz |
| Bandwidth | 100 MHz |
| UAV transmit power | 30 dBm |
| Noise power | -94 dBm |
| Area | 500 m × 500 m |
| UAV height | 100 m |
| Maximum UAV speed | 8 m/s |
| CSI correlation | 0.965 |
| Mobility correlation | 0.90 |
| RIS phase quantization | 2-bit |
| RIS elements optimized/round | 32 |
| RIS coordinate iterations | 2 |
| Initial UAV energy | 100 J |
| Trust memory | 0.90 |

---

## Fair Experimental Design

V4.3 uses several controls to make the comparison between aggregation methods and attack scenarios more reproducible.

### Common data realization

For each Monte-Carlo run, the same local datasets are reused across all attack scenarios.

### Common physical realization

The same UAV mobility, CSI innovations, RIS channel trajectories, and initial wireless conditions are reused across attack fractions within each Monte-Carlo run.

### Fixed attacker ordering

A fixed attacker ordering is generated for each Monte-Carlo run. Increasing the attack fraction therefore adds malicious UAVs from the same predefined ordering.

### Common mini-batches

The same mini-batch indices are reused across methods and attack scenarios.

### Separate local accuracy

Local model accuracy is calculated separately for every FL method.

### Attacker ground truth

The malicious-UAV ground truth is used only for:

- controlled attack generation
- evaluation of malicious aggregation contribution

It is **not** used for:

- trust calculation
- communication reliability
- anomaly detection
- adaptive aggregation

This prevents attacker labels from leaking into the proposed aggregation mechanism.

---

## RIS Model

The implementation contains a channel-dependent, lightweight RIS model.

The simulation explicitly generates:

- BS-RIS channel
- RIS-UAV/user channels
- Time-correlated RIS channels
- Cascaded RIS propagation

A quantized RIS phase vector is optimized using coordinate updates.

The RIS configuration uses:

- 128 RIS elements
- 2-bit phase quantization
- 4 candidate phase levels
- 32 optimized elements per round
- 2 coordinate-optimization iterations

The RIS model is intentionally lightweight and does not represent a full multi-user beamforming optimization solver.

---

## Federated Learning Model

Each UAV locally trains a lightweight binary classification model using logistic regression.

The local model contains:

- 8 input features
- 1 bias term

The local optimization uses:

- Mini-batch gradient updates
- 3 local epochs
- Batch size of 32
- Learning rate = 0.030
- L2 regularization = 1e-3

The global model is obtained by aggregation of the local model parameters.

---

## Non-IID Data

The simulation creates heterogeneous local datasets using UAV-specific class biases.

The class-bias values are:

```text
0.02
0.05
0.10
0.15
0.25
0.75
0.85
0.90
0.95
0.98
