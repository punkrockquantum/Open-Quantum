
# Import necessary libraries
from qiskit import QuantumCircuit
from qiskit.visualization import plot_histogram, plot_bloch_multivector
from qiskit import Aer, transpile, assemble
from numpy import pi

# Function to perform QFT
def qft(circuit, n):
    for j in range(n):
        for k in range(j):
            circuit.cp(pi/2**(j-k), k, j)
        circuit.h(j)

# Create a Quantum Circuit with 3 qubits
qc = QuantumCircuit(3)

# Apply QFT
qft(qc, 3)

# Draw the circuit
print(qc.draw())

# Simulate the circuit
simulator = Aer.get_backend('statevector_simulator')
compiled_circuit = transpile(qc, simulator)
job = simulator.run(assemble(compiled_circuit))
result = job.result()

# Get the statevector
statevector = result.get_statevector()
print(statevector)

# Plot the statevector on the Bloch sphere
plot_bloch_multivector(statevector)
