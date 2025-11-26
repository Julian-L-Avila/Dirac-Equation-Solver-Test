# User Manual

## 1. Licensing and Citation

### Licensing

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

### Citation

If you use this software in your research, please cite it as follows:

```
[Placeholder for academic citation]
```

## 2. Theoretical Formulation

The dynamics of the spinor field ψ(x) are governed by the Dirac equation:

(iγ^μ ∂_μ - m)ψ(x) = 0

where:
- γ^μ are the gamma matrices, which satisfy the Clifford algebra {γ^μ, γ^ν} = 2g^μν I.
- g^μν is the metric tensor with signature (+, -, -, -).
- m is the mass of the particle.
- The spinor field ψ(x) is a four-component complex vector.

## 3. The Discretization Scheme

The Dirac equation is discretized on a space-time lattice using the staggered grid formulation. This approach ensures numerical stability and avoids the fermion doubling problem.

### Space-Time Lattice

The space-time continuum is replaced by a discrete lattice with spacing `Δx` in the spatial dimensions and `Δt` in the time dimension.

### Staggered Grid Formulation

The components of the spinor field are placed at different points on the lattice, which allows for a more accurate representation of the derivatives in the Dirac equation.

### Stability Criteria

For the time-evolution operator to be stable, the time step `Δt` must satisfy the following condition:

Δt <= Δx / c

where `c` is the speed of light. In this simulation, we use natural units where `c = 1`.

## 4. API Reference

The `dirac_solver` library is designed with a modular architecture that separates grid initialization, spinor state preparation, external potential coupling, and boundary condition management.

### Grid Initialization (`geometry.py`)

The `Grid` class in `dirac_solver.geometry` is used to define the spatial grid for the simulation.

- `Grid(extents, num_points)`: Creates a grid with the specified extents and number of points in each dimension.

### Spinor State Preparation (`initial_state.py`)

The `InitialState` class in `dirac_solver.initial_state` is used to define the initial state of the spinor field.

- `InitialState(grid, mass)`: Creates an initial state on the given grid with the specified mass.

### External Potential Coupling (`potentials.py`)

The `dirac_solver.potentials` module provides a variety of potentials that can be coupled to the Dirac equation.

- `ScalarPotential(grid, potential_function)`: Creates a scalar potential from a given function.
- `CoulombPotential(grid, charge_center, strength)`: Creates a Coulomb potential.
- `YukawaPotential(grid, charge_center, strength, range)`: Creates a Yukawa potential.
- `InfiniteWellPotential(grid, well_region)`: Creates an infinite well potential.

### Boundary Condition Management

Boundary conditions are managed by the `DiracSolver` class in `dirac_solver.core`.

- `DiracSolver(grid, initial_state, potential, boundary_conditions)`: Creates a solver with the specified grid, initial state, potential, and boundary conditions.

## 5. Validation and Physical Benchmarks

The numerical fidelity of the `dirac_solver` is verified through a series of canonical tests.

### Dispersion Relations

The simulation correctly reproduces the dispersion relation for a free particle, `E^2 = p^2 + m^2`.

### Klein Tunneling

The simulation demonstrates the phenomenon of Klein tunneling, where a relativistic particle can penetrate a potential barrier of arbitrary height.

### Zitterbewegung

The simulation reproduces the rapid oscillatory motion of a free relativistic particle, known as Zitterbewegung.

## 6. Authors and About Us

This project was created by [Author Name].

For questions, feedback, or support, please open an issue on the GitHub repository.
