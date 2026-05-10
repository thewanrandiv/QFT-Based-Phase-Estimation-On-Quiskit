# QFT-Based Phase Estimation On Quiskit
Implemention of  phase estimation for a simple unitary, such as a rotation gate. 


# QFT Phase Estimation
 
**Target gate:** `Rz(θ)`
 
---
 
## Parameters
 
| Parameter | Value |
|---|---|
| Rotation angle θ (radians) | π/2 |
| Counting qubits n | 4 |
 
---
 
## Results
 
| Metric | Value |
|---|---|
| True phase φ | 0.2499 |
| SpinQ estimate | 0.2500 |
| Qiskit estimate | 0.2500 |
| Resolution 1/2ⁿ | 0.0625 |
 
---
 
## QPE Circuit Structure
 
```
q[0] ─── H ──●──────────────────── QFT⁻¹ ── M
q[1] ─── H ──────●────────────────  QFT⁻¹ ── M
q[2] ─── H ──────────●──────────── QFT⁻¹ ── M
q[3] ─── H ──────────────●──────── QFT⁻¹ ── M
|ψ⟩ ─── X ── U ── U² ── U⁴ ── U⁸ ──────────
```
 
- Counting qubits (q[0]–q[3]) each initialized with a Hadamard gate (**H**)
- Controlled unitary operations applied to the target qubit `|ψ⟩`
- Inverse QFT (QFT⁻¹) applied across all counting qubits
- Each counting qubit measured (**M**) at the end
---
 
## Probability Distributions
 
### SpinQ Backend
- Peak bitstring: **0100** with probability ≈ **0.88**
- All other bitstrings have near-zero probability
### Qiskit Simulator
- Peak bitstring: **0100** with probability ≈ **0.95**
- All other bitstrings have near-zero probability
Both distributions show a strong, sharp peak at bitstring `0100`, confirming a clean phase estimate.
 
---
 
## Backend Comparison
 
| Metric | SpinQ Backend | Qiskit Simulator |
|---|---|---|
| Estimated phase | 0.25000 | 0.25000 |
| Absolute error | 0.00013 | 0.00013 |
| Peak bitstring | 0100 | 0100 |
| Representable? | ✅ Yes | ✅ Yes |
