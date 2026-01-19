Step-by-Step Procedure

Step 1: Circuit model and parameter definition

A two-layer network of Wien–bridge oscillators is implemented in LTspice.
Each layer consists of five oscillators, with intralayer coupling resistors layer1R, layer2R and an interlayer coupling resistor 
inter_R.

The interlayer coupling resistance inter_R is treated as the control parameter and is varied adiabatically over a prescribed range.

Step 2: Automated parameter sweep

The LTspice schematic is executed programmatically using Python via the PyLTSpice interface.
The interlayer coupling resistor inter_R is swept over a range.
For each value of inter_R, an independent transient simulation is launched, generating a corresponding waveform (.raw) file.

Step 3: Data management and validation

Prior to running the parameter sweep, all previously generated waveform files are removed to avoid contamination from earlier simulations.
After the completion of the simulations, the waveform files are automatically detected and sorted in the order of execution, ensuring a one-to-one correspondence between coupling strength and simulation output.

Step 4: Signal extraction

For each simulation, the time-dependent voltage signals at the output nodes of all oscillators are extracted separately for the two layers.
Only nodes corresponding to valid oscillator outputs are considered for further analysis.

Step 5: Phase reconstruction

The instantaneous phase of each oscillator is obtained from its voltage signal using the Hilbert transform.
Phase unwrapping is applied to remove artificial 2pi discontinuities, yielding smooth phase trajectories. 

Step 6: Synchronization quantification

The collective synchronization of each layer is quantified using the Kuramoto order parameter,


Step 7: Steady-state averaging

To eliminate transient effects, the order parameter is averaged over the steady-state portion of the time series.
The resulting time-averaged order parameter ⟨R⟩ provides a single synchronization measure for each layer and each coupling strength.

Step 8: Construction of synchronization curves

The steady-state order parameters of both layers are plotted as functions of the coupling resistor R or coupling strength k=1/R.
