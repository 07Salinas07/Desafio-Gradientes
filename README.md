# Desafío de Métodos Numéricos: Gradientes Conjugados Precondicionado en finanzas

**Universidad Mayor de San Andrés · Facultad de Ciencias Puras y Naturales · Carrera de Informática**

- **Autor:** Carlos Salinas
- **Mención:** (escribe aquí tu mención)
- **Página web:** https://07salinas07.github.io/Desafio-Gradientes/

## Descripción

Página web interactiva que modela la asignación óptima de una cartera de 6 activos (Bonos del Tesoro, Acciones locales, Acciones de tecnología, Oro, Inmobiliario y Mercados emergentes) como un sistema lineal simétrico y definido positivo **Σx = b**, y lo resuelve con el **Método de Gradientes Conjugados Precondicionado (GCP)** de Suñagua (2020).

El modelo sale de maximizar μᵀx − (λ/2)·xᵀΣx, que lleva a Σx = μ/λ, donde Σ es la matriz de covarianzas, μ los retornos esperados y λ = 1 la aversión al riesgo. Los datos son sintéticos e ilustrativos y se pueden editar en la propia página.

## Escenarios

| Escenario | Descripción |
|---|---|
| Ideal | Mercado estable, volatilidades moderadas y correlación baja. κ(A) bajo. |
| Bajo estrés | Inflación y alza de tasas: más volatilidad y correlación, menores retornos. |
| Mal condicionado | Variables en escalas muy distintas: κ(A) muy alto por mal escalamiento diagonal. |

## Funcionalidades

- Edición de A, b, x₀, tolerancia, N máx y precondicionador, con recálculo automático.
- Verificación de simetría y definición positiva (criterio de Sylvester y autovalores).
- Solución numérica de referencia por método directo (factorización de Cholesky).
- GCP (Jacobi o SSOR) contrastado con GC simple, con gráfico de convergencia.
- Errores absoluto, relativo y porcentual por variable, y residuo relativo global.
- Números de condición κ(A) y κ(M⁻¹A).
- Tabla comparativa de los tres escenarios.
- Módulo de pruebas (QA) con 4 casos: carga de escenarios, matriz no válida, edición dinámica y comparativa de precondicionamiento.

## Arquitectura

Aplicación de **un solo archivo**, `index.html`, con HTML, CSS y JavaScript puro, sin dependencias ni servidor.

- `build(k)`: construye A y b de cada escenario.
- `validate`, `chol`, `det`, `eig`: validación de la matriz y factorización de Cholesky.
- `pcg`: algoritmo GCP (con M = I equivale a GC simple).
- `Mmat`, `kap`, `cond`: precondicionadores y números de condición.
- `solve`: integra solución directa, GCP, GC y errores.
- `go`, `draw`, `qa`: interfaz reactiva, tablas, gráfico y pruebas.

## Ejecución local

No requiere instalación. Hay dos opciones:

1. Descargar o clonar el repositorio y abrir `index.html` en un navegador moderno.
2. Opcionalmente, servirlo con `python -m http.server` y abrir `http://localhost:8000`.

```bash
git clone https://github.com/07Salinas07/Desafio-Gradientes.git
cd Desafio-Gradientes
```

## Referencias

- Suñagua S., P. (2020). Método de Gradientes Conjugados Precondicionado. *Revista Boliviana de Matemática – UMSA*, 04, 2–7.
- Golub, G. H., y Van Loan, C. F. (2013). *Matrix Computations* (4.ª ed.). Johns Hopkins University Press.
- Saad, Y. (2003). *Iterative Methods for Sparse Linear Systems* (2.ª ed.). SIAM.
