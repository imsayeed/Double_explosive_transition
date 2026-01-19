Step 1: Import required libraries
The script imports numerical, signal-processing, plotting, and LTspice-interface libraries required for:
	Reading LTspice waveform files
	Extracting oscillator phases
	Computing synchronization order parameters
	Visualizing results

Step 2: Definition of coupling parameter values
A logarithmically spaced set of interlayer coupling resistances is defined:

This range matches the coupling values used during the LTspice simulations.

Step 3: Detection and sorting of waveform files
All LTspice waveform files matching the pattern inter_R_*.raw are automatically detected.
Files associated with operating-point analysis (.op) are excluded.
The waveform files are numerically sorted according to their filename indices to preserve the correct correspondence between coupling resistance and simulation output.
Each waveform file is then paired with its corresponding coupling resistance value.

Step 4: Definition of the order-parameter function
A function is defined to compute the Kuramoto order parameter from LTspice voltage signals:
4.1 Voltage extraction
For a given waveform file, voltage time series from a specified list of oscillator output nodes are extracted.
4.2 Phase reconstruction
The instantaneous phase of each oscillator is reconstructed using the Hilbert transform.
Phase unwrapping is applied to eliminate artificial 2πdiscontinuities.
4.3 Synchronization quantification
The Kuramoto order parameter is computed as
R(t)=∣1/N ∑_(k=1)^N e^(iϕ_k (t)) ∣,

where N=5is the number of oscillators per layer.
4.4 Steady-state averaging
The time-dependent order parameter is averaged over the simulation time window to obtain a single steady-state synchronization measure for each layer.

Step 5: Layer definition
Two sets of nodes are specified:
	Layer 1 (environmental / driving layer)
	Layer 2 (dynamical / controlled layer)
Each layer contains five Wien-bridge oscillators.

Step 6: Order-parameter computation
For each coupling resistance value:
	The corresponding waveform file is loaded.
	The order parameter of Layer 1 is computed.
	The order parameter of Layer 2 is computed.
	The inverse coupling strength K=1/Ris calculated.
	All quantities are stored for further analysis.

Step 7: Construction of data table
The extracted quantities are assembled into a structured data table containing:
	Coupling resistance R
	Effective coupling strength K=1/R
	Order parameter of Layer 1
	Order parameter of Layer 2
The data are sorted according to the coupling parameter.

