# SolventShellInteractions

Computes the electrostatic potential of the molecules which have at least
one atom within a distance from a solute. 

Currently only works with Gromacs topology and trajectory formats. 

## Installation

```julia
julia> import Pkg

julia> Pkg.add(url="http://github.com/m3g/SolventShellInteractions.jl")
```

## Example

```julia
using Plots
using PDBTools
using SolventShellInteractions

dir="./test/files"

# read pdb file
pdb = readPDB("$dir/simulacao_EMIMDCA.pdb")

# solute atoms
solute = select(pdb, "protein")
solvent = select(pdb, "resname EMI")

# trajectory file (Gromacs xtc only)
trajectory = "$dir/simulacao_EMIMDCA_curta.xtc"

# topology files
top_files = [ "$dir/topol.top", "$dir/tip3p.itp" ]

# distance of the first dip in the distribution
cutoff = 10.

# compute electrostatic potential
u = electrostatic_potential(
    solute,
    solvent,
    cutoff,
    trajectory, 
    top_files,
)

plot(
    u,
    xlabel="step",
    ylabel="electrostaic potential / kJ / mol",
    linewidth=2, framestyle=:box, label=nothing
)
```

Will produce (for a longer trajectory):

![example.png](./docs/example.png)

## References










