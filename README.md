# Cuatro patas, un hogar · EDO logística con Heun y RK4

Desafío individual de **Métodos Numéricos** (Carrera de Informática, UMSA).
Simulación web de una campaña de adopción responsable de perros rescatados en La Paz, modelada con una ecuación diferencial ordinaria de primer orden con condición inicial.

- **Autor:** Nivardo Roman Leon Dueñas
- **Materia:** Métodos Numéricos


## Problema

Los refugios tienen capacidad limitada y necesitan saber cuánto tardará una campaña de difusión en alcanzar una cantidad suficiente de familias inscritas para adoptar.

**Pregunta del desafío:** ¿en cuántas semanas se alcanzará la meta de 150 familias inscritas y qué tan precisas son las aproximaciones de Heun y RK4?

## Modelo matemático

```
dy/dt = r · y · (1 − y/K),    y(0) = y₀
```

| Símbolo | Significado | Unidad | Valor por defecto |
|---|---|---|---|
| t | Tiempo | semanas | 0 ≤ t ≤ 20 |
| y(t) | Familias inscritas acumuladas | familias | — |
| y₀ | Familias iniciales | familias | 10 |
| K | Familias potenciales (capacidad de carga) | familias | 300 |
| r | Tasa de crecimiento por difusión | 1/semana | 0,30 |

> Los parámetros son **hipotéticos**: es una simulación didáctica, no una predicción comprobada con datos reales.

**Solución analítica:**

```
y(t) = K / (1 + A·e^(−rt)),    A = (K − y₀) / y₀
```

La página muestra el despeje por separación de variables y la verificación por sustitución (la EDO y la condición inicial).

## Métodos numéricos

- **Heun (Runge-Kutta de orden 2):** error global O(h²).
- **Runge-Kutta clásico de orden 4 (RK4):** error global O(h⁴).

Ambos usan los mismos parámetros, condición inicial, intervalo y tamaño de paso h.
Errores calculados frente a la solución analítica: error absoluto `Eₐ = |y_exacta − y_aprox|` y error relativo porcentual `E% = 100·Eₐ/|y_exacta|`.

## Funciones de la aplicación

- Entrada editable de y₀, K, r, meta, T y dos tamaños de paso (h₁ y h₂).
- Validación de entradas (campos numéricos, 0 < y₀ < K, r > 0, h ≤ T, meta entre y₀ y K, máximo 2000 pasos).
- Tabla por pasos con solución exacta, Heun, RK4, error absoluto y error relativo porcentual.
- Gráfica de la solución analítica, Heun y RK4, y gráfica del error absoluto.
- Comparación de dos tamaños de paso.
- Interpretación automática del resultado (tiempo para alcanzar la meta y método con menor error).

## Cómo ejecutarlo

No requiere instalación ni servidor. Hay dos opciones:

1. Abrir `index.html` en el navegador (doble clic).
2. En VS Code, usar la extensión **Live Server** → *Open with Live Server*.

Necesita conexión a internet para cargar las librerías por CDN: Bootstrap 5, Chart.js y MathJax.

## Estructura

```
.
├── index.html   # Aplicación completa (HTML + CSS + JavaScript)
└── README.md
```

## Tecnologías

HTML, CSS y JavaScript, con Bootstrap 5 (estilos), Chart.js (gráficas) y MathJax (fórmulas).
