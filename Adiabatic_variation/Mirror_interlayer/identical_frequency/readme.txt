Step 1: Definition of simulation environment
The LTspice schematic describing a two-layer Wien-bridge oscillator network is specified.
Two separate directories are created to store waveform files corresponding to forward and backward parameter sweeps.

Step 2: Control parameter and sweep protocol
The interlayer coupling resistor inter_R is selected as the control parameter.
Two  spaced parameter sequences are defined: one for forward and other for backward.
The two sequences are concatenated to form a single sweep protocol. 

Step 3: Selection of monitored nodes
A comprehensive set of circuit nodes is specified, including:
	Output voltages of all oscillators in both layers
	Internal and coupling nodes of the circuit
These nodes are used to record the final dynamical state of the system after each simulation.

Step 4: Initialization of state memory
An initially empty dictionary is created to store the final voltages of all monitored nodes from the previous simulation step.
This stored state is later used to initialize subsequent simulations, enforcing adiabatic continuation.

Step 5: Iterative parameter sweep
For each value of the coupling resistor R:
	The sweep direction (forward or backward) is identified.
	A new LTspice simulation instance is created.
	The coupling resistor value is updated accordingly.

Step 6: Injection of initial conditions
If a previous simulation state exists, the final node voltages from the preceding step are injected into the new simulation using a .ic directive.
This ensures that each simulation starts from the previous steady state, allowing the system to remain on the same dynamical branch unless a transition occurs.

Step 7: Execution and file detection
The LTspice simulation is executed.
The script then actively monitors the working directory and identifies the most recently generated .raw file, ensuring robust handling of LTspice’s automatic file naming.

Step 8: Organized storage of waveform files
The generated waveform file is renamed according to the corresponding parameter value and moved into the appropriate directory (forward or backward).
This preserves a clean, reproducible record of the hysteresis branches.

Step 9: Extraction of final states
From each waveform file, the final voltage values of all monitored nodes are extracted.
The script automatically adapts to different LTspice naming conventions (with or without the V(...) prefix).
These final voltages are stored and reused as initial conditions for the next parameter step.


