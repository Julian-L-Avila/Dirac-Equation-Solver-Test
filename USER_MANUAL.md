# Manual de Usuario

## 1. Licencia y Citación

### Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulte el archivo [LICENSE](LICENSE) para más detalles.

### Citación

Si utiliza este software en su investigación, por favor cítelo de la siguiente manera:

```
[Espacio reservado para la citación académica]
```

## 2. Formulación Teórica

La dinámica del campo espinorial ψ(x) se rige por la ecuación de Dirac:

(iγ^μ ∂_μ - m)ψ(x) = 0

donde:
- γ^μ son las matrices gamma, que satisfacen el álgebra de Clifford {γ^μ, γ^ν} = 2g^μν I.
- g^μν es el tensor métrico con signatura (+, -, -, -).
- m es la masa de la partícula.
- El campo espinorial ψ(x) es un vector complejo de cuatro componentes.

Un estado de partícula libre con momento `p` y espín `s` se describe mediante un espinor de Dirac `u(p, s)`, que se construye a partir de un espinor de Pauli de dos componentes χ_s. El espinor de Dirac tiene la forma:

u(p, s) = (sqrt(E + m) * χ_s)
          (sqrt(E - m) * (p·σ / |p|) * χ_s)

donde `E` es la energía relativista y `σ` son las matrices de Pauli.

## 3. Esquema de Discretización

La ecuación de Dirac se discretiza en una red espacio-temporal utilizando la formulación de rejilla escalonada (staggered grid). Este enfoque garantiza la estabilidad numérica y evita el problema del doblado de fermiones.

### Red Espacio-Temporal

El continuo espacio-temporal se reemplaza por una red discreta con un espaciado `Δx` en las dimensiones espaciales y `Δt` en la dimensión temporal.

### Formulación de Rejilla Escalonada

Las componentes del campo espinorial se sitúan en diferentes puntos de la red, lo que permite una representación más precisa de las derivadas en la ecuación de Dirac.

### Criterio de Estabilidad

Para que el operador de evolución temporal sea estable, el paso de tiempo `Δt` debe satisfacer la siguiente condición:

Δt <= Δx / c

donde `c` es la velocidad de la luz. En esta simulación, utilizamos unidades naturales donde `c = 1`.

## 4. Referencia de la API

La biblioteca `dirac_solver` está diseñada con una arquitectura modular que separa la inicialización de la rejilla, la preparación del estado del espinor, el acoplamiento de potenciales externos y la gestión de las condiciones de contorno.

### Arquitectura del Solucionador

Para configurar y ejecutar una simulación, se utiliza el patrón `Builder`.

1.  **`DiracProblemBuilder`**: Una clase que guía la construcción de un problema de simulación paso a paso.
2.  **`SimulationProblem`**: Un objeto que contiene todos los parámetros de la simulación (rejilla, estado inicial, potencial, etc.).
3.  **`DiracSolver`**: La clase principal que toma un `SimulationProblem` y ejecuta la simulación.

### Inicialización de la Rejilla (`geometry.py`)

La clase `Grid` se utiliza para definir la rejilla espacial para la simulación.

- `Grid(shape, spacing, origin=None)`: Crea una rejilla.
  - `shape`: Una tupla que especifica el número de puntos en cada dimensión (p. ej., `(100,)` para 1D, `(100, 100)` para 2D).
  - `spacing`: Una tupla que especifica el espaciado entre puntos en cada dimensión (p. ej., `(0.1,)`).
  - `origin`: El punto de inicio de la rejilla (por defecto, centrada en 0).

### Preparación del Estado del Espinor (`initial_state.py`)

Estas clases se utilizan para definir el estado inicial del campo espinorial. `InitialState` es una clase base abstracta.

- `GaussianPacket(constant_spinor, center, spatial_width)`: Crea un paquete de ondas gaussiano.
- `PlaneWave(constant_spinor)`: Crea una onda plana.

### Acoplamiento de Potenciales Externos (`potentials.py`)

El módulo `dirac_solver.potentials` proporciona varios potenciales.

- `FreeParticle()`: Potencial cero para una partícula libre.
- `ScalarPotential(func)`: Crea un potencial escalar a partir de una función `func` que toma una posición y devuelve un escalar.
- `CoulombPotential(Z, epsilon=1e-6)`: Potencial de Coulomb regularizado.
- `YukawaPotential(strength, range)`: Potencial de Yukawa para interacciones de corto alcance.
- `InfiniteWellPotential(widths)`: Potencial de pozo infinito.

### Gestión de Condiciones de Contorno (`boundaries.py`)

Las condiciones de contorno se especifican al construir el problema.

- `PeriodicBoundary()`: Condiciones de contorno periódicas.
- `AbsorbingBoundary(strength, width=20)`: Una capa absorbente en los bordes de la rejilla.

## 5. Validación y Puntos de Referencia Físicos

La fidelidad numérica de `dirac_solver` se verifica a través de una serie de pruebas canónicas.

### Relaciones de Dispersión

La simulación reproduce correctamente la relación de dispersión para una partícula libre, `E^2 = p^2 + m^2`.

### Túnel de Klein

La simulación demuestra el fenómeno del túnel de Klein, donde una partícula relativista puede penetrar una barrera de potencial de altura arbitraria.

### Zitterbewegung

La simulación reproduce el rápido movimiento oscilatorio de una partícula relativista libre, conocido como Zitterbewegung.

## 6. Autores y Sobre Nosotros

Este proyecto fue creado por [Nombre del Autor].

Para preguntas, comentarios o soporte, por favor abra un *issue* en el repositorio de GitHub.
