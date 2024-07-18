
QISKIT:

# Import necessary libraries
from qiskit import QuantumCircuit, Aer, transpile, assemble
from qiskit.visualization import plot_bloch_multivector, plot_histogram

# Create a Quantum Circuit with 1 qubit and 1 classical bit
qc = QuantumCircuit(1, 1)

# Add a Hadamard gate to put the qubit in superposition
qc.h(0)

# Measure the qubit
qc.measure(0, 0)

# Simulate the circuit
simulator = Aer.get_backend('qasm_simulator')
compiled_circuit = transpile(qc, simulator)
job = simulator.run(assemble(compiled_circuit))
result = job.result()

# Get the counts (measurement results)
counts = result.get_counts(qc)
print(counts)

# Plot the result
plot_histogram(counts)
