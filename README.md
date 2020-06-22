# BoteSalvatICX.jl

![Build Badge](https://travis-ci.com/usnistgov/BoteSalvatICX.jl.svg?branch=master)

Implements the Bote-Salvat ionization cross section model described in

* D. Bote and F. Salvat, _"Calculations of inner-shell ionization by electron impact with the distorted-wave and plane-wave Born approximations"_, Phys. Rev. **A77**, 042701 (2008).
* Bote, David, et al. _"Cross sections for ionization of K, L and M shells of atoms by impact of electrons and positrons with energies up to 1 GeV: Analytical formulas."_ Atomic Data and Nuclear Data Tables **95.6** (2009): 871-909.

This is a very lean implementation that only handles electrons.

Elements are identified by atomic number, `z`.

Sub-shells are identified by integer indices where 1->K, 2->L₁, 3->L₂, ...,9->M₅ (IUPAC notation) or
1->1S½, 2->2S½, 3->2P½, 4->2P³/₂,... (atomic notation).

```julia
boteSalvatICX(z::Int, subshell::Int, energy::AbstractFloat, edgeenergy::AbstractFloat=boteSalvatEdgeEnergy(z, subshell))
```
* Computes the cross-section in square centimeters for z=1:99, subshell=1:<=9, energy = 0 to 1 GeV in eV
* If edgeenergy is nothing, the B-S recommended value is used, otherwise the user may provide an edge energy in eV
* Returns 0.0 if energy<edgeenergy
* Throws an assertion if data isn't available for the specified element and sub-shell.

```julia
boteSalvatAvailable(z::Integer, subshell::Int)
```
* True if data is available to compute the cross section for the specified sub-shell

```julia
boteSalvatEdgeEnergy(z::Integer, subshell::Int)
```
* The ionization energy for the specified element and sub-shell.


If the plotting module [Gadfly](https://github.com/GiovineItalia/Gadfly.jl) is loaded, the function
```julia
plotBoteSalvatICX(z::Integer)
```
will produce a log-log plot of the cross sections for all available sub-shells from threshold to 1 GeV.
