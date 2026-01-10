# Math Generative Art Lab - Documentación Técnica

## Descripción

El **Math Generative Art Lab** contiene **7 simulaciones** de arte algorítmico visual que exploran modelos matemáticos emergentes: reacción-difusión, L-Systems, flow fields, atractores caóticos, phyllotaxis, fractales IFS y teselaciones aperiódicas.

## Simulaciones (7 Total)

1. **Reacción-Difusión** - Sistema Gray-Scott (PDEs)
2. **L-Systems** - Gramáticas de Lindenmayer (10 presets)
3. **Flow Fields** - Perlin Noise 3D
4. **Strange Attractors** - Caos determinista (8 atractores)
5. **Phyllotaxis** - Ángulo áureo (Fibonacci)
6. **Fractales IFS** - Juego del caos (8 fractales)
7. **Teselaciones Aperiódicas** - Penrose (kite & dart)

## Algoritmos Generativos

### 1. Reacción-Difusión (Gray-Scott)

**Ecuaciones PDEs:**
```
∂u/∂t = Dᵤ∇²u - uv² + F(1-u)    [Sustrato A]
∂v/∂t = Dᵥ∇²v + uv² - (k+F)v    [Catalizador B]
```

**Parámetros:**
- Du = 0.2097, Dv = 0.105 (difusión)
- F = feed rate (0.01-0.1)
- k = kill rate (0.03-0.07)

**8 Patrones predefinidos:**
- Coral (F=0.0545, k=0.062)
- Mitosis (F=0.0367, k=0.0649)
- Laberinto (F=0.029, k=0.057)
- Espirales, Ondas, Agujeros, Manchas, Gusanos

**Método:** Diferencias finitas explícitas (FTCS)
**Laplaciano:** ∇²u = u[left] + u[right] + u[up] + u[down] - 4·u[idx]

**Interactividad:** Click+drag añade químico V (u=0.5, v=0.25)

### 2. L-Systems (Lindenmayer)

**Gramática:** Axioma → Aplicar reglas^n → Interpretar gráficamente

**Símbolos Turtle Graphics:**
- **F/G**: avanzar (dibujando/sin dibujar)
- **+/-**: girar derecha/izquierda
- **[/]**: push/pop estado (stack)

**10 Presets:**
1. **Arbusto** - `FF+[+F-F-F]-[-F+F+F]` (4 iter, 22°)
2. **Planta** - Estructura orgánica (5 iter, 25°)
3. **Koch** - Copo de nieve (4 iter, 60°)
4. **Sierpinski** - Triángulo fractal (6 iter, 120°)
5. **Dragón** - Curva de Heighway (12 iter, 90°)
6. **Hilbert** - Space-filling curve (5 iter, 90°)
7. **Isla, Cristal, Hierba, Árbol**

**Renderizado:**
- Auto-scaling y centrado
- Colores: Monocromo, Gradiente (verde → amarillo), 5 opciones
- Grosor variable (taper): líneas base → puntas finas

### 3. Flow Fields (Perlin Noise)

**Función de Campo:**
```
θ(x,y,t) = noise3D(x·scale, y·scale, t·timeScale) · 2π
v(x,y) = (cos(θ), sin(θ))
```

**Implementación Perlin 3D:**
- Permutation table: 256 elementos shuffleados
- Fade function: f(t) = t³(10t² - 15t + 6) [Hermite]
- Lerp: interpolación lineal

**3,000-8,000 Partículas:**
- Edad de vida: 50-150 frames
- Reinicio al morir o salir de bounds
- Trace rendering con fade

**4 Presets:**
- Suave (scale 0.005, speed 2)
- Turbulento (scale 0.02, speed 3)
- Van Gogh (scale 0.008, speed 1, fade 0.01)
- Tormenta (scale 0.015, speed 4, 8000 partículas)

**4 Paletas:** Cyan, Fire, Aurora, Monochrome

### 4. Strange Attractors (Caos)

**8 Atractores:**

**Lorenz:**
```
dx/dt = σ(y - x)
dy/dt = x(ρ - z) - y
dz/dt = xy - βz

σ=10, ρ=28, β=8/3
```

**Rössler, Aizawa, Thomas, Halvorsen, Dadras, Chen, Sprott**

**Método:** Euler/RK4 dependiendo del atractor
**Renderizado 2D:** Proyección ortográfica con rotación 3D interactiva
**Trail:** Últimos 5,000-20,000 puntos

**4 Paletas:** Purple, Rainbow, Fire, Ice

### 5. Phyllotaxis (Fibonacci)

**Modelo:**
```
θₙ = n · α
rₙ = c · √n

α = 360° / φ² = 137.507764°  [Ángulo Áureo]
φ = (1 + √5) / 2 ≈ 1.618
```

**8 Presets angulares:**
- Girasol (137.507764°) - Ángulo áureo perfecto
- Casi áureo (137.3°)
- Piña (99.5°)
- Cruz (90°), Triángulo (120°), Pentágono (144°)

**4 Formas:** Circle, Square, Petal, Seed
**4 Paletas:** Sunflower, Succulent, Rose, Rainbow

### 6. Fractales IFS (Iterated Function System)

**Algoritmo del Juego del Caos:**
```
Seleccionar transformación aleatoria según probabilidades
(x,y) ← T(x,y) = [a b; c d](x,y) + (e,f)
Iterar 10,000 puntos warmup, luego renderizar
```

**8 Fractales:**
1. **Helecho de Barnsley** (4 transformaciones)
2. **Árbol** (ramificación binaria)
3. **Sierpinski** (3 contracciones)
4. **Alfombra** (8 transformaciones, grid 3×3)
5. **Dragón de Heighway** (2 rotaciones)
6. **Copo de Koch** (4 transformaciones)
7. **Hoja Maple** (4 transformaciones orgánicas)
8. **Espiral Logarítmica** (φ en escalas)

**Renderizado:** 500-2,000 puntos/frame
**4 Paletas:** Green, Autumn, Ice, Fire

### 7. Teselaciones Aperiódicas (Penrose)

**Geometría:** φ = (1 + √5) / 2 ≈ 1.618

**Representación Triangular:**
- Triángulos rojos (Kite) y azules (Dart)
- Subdivisión recursiva con razón áurea

**Reglas de Subdivisión:**

**Triángulo Rojo:**
```
P = A + (B - A) / φ
Nuevo rojo: (C, P, B)
Nuevo azul: (P, C, A)
```

**Triángulo Azul:**
```
Q = B + (A - B) / φ
R = B + (C - B) / φ
Azul₁: (R, C, A)
Azul₂: (Q, R, B)
Rojo:  (R, Q, A)
```

**Convergencia:** Kites:Darts → φ

**3 Variantes:**
1. Penrose P3 (Kite & Dart) - Simetría 5-fold
2. Penrose P2 (Rhombus)
3. Ammann-Beenker - Simetría 8-fold

**Interactividad:** Pan, zoom, subdividir (límite 50,000 triángulos)

## Métodos de Rendering

### Canvas 2D

**Device Pixel Ratio:**
```javascript
canvas.width = width * 2
ctx.scale(2, 2)  // Retina
```

**Técnicas:**
- **Image Data Buffer:** Reacción-Difusión (`putImageData()`)
- **Trail Rendering:** Strange Attractors (polyline últimos N puntos)
- **Fade Effect:** Flow Fields (rectángulo semi-transparente)
- **Pixel-Perfect:** IFS (puntos 1px)

## Parámetros Configurables

| Simulación | Parámetro | Rango |
|------------|-----------|-------|
| Reacción-Difusión | Feed (F) | 0.01-0.1 |
| | Kill (k) | 0.03-0.07 |
| L-Systems | Iteraciones | 1-8 |
| | Ángulo | 5-180° |
| Flow Fields | Escala Noise | 0.001-0.03 |
| | Partículas | 500-10000 |
| Strange Attractors | Velocidad | 10-200 steps/frame |
| | Trail | 1000-20000 puntos |
| Phyllotaxis | Ángulo | 0-360° |
| | Semillas | 50-2000 |
| Fractales IFS | Puntos/Frame | 100-2000 |
| Teselaciones | Tamaño Inicial | 100-400 px |

## Características Únicas

1. **Reacción-Difusión:** Interactividad directa (click+drag), simulación PDE genuina
2. **L-Systems:** Editor parametrizable, 10 presets clásicos, animación progresiva
3. **Flow Fields:** Perlin 3D desde cero, 5 parámetros independientes
4. **Strange Attractors:** 8 atractores distintos, rotación 3D en tiempo real
5. **Phyllotaxis:** Ángulo áureo exacto (137.507764°), demuestra imperfecciones
6. **Fractales IFS:** Juego del caos, 8 fractales clásicos
7. **Teselaciones:** Estructura no-periódica, subdivisión recursiva

## Referencias

**Total:** 7 simulaciones, ~3,876 líneas de código

**Complejidad Algorítmica:**

| Simulación | Time/Frame | Space |
|-----------|-----------|-------|
| Reacción-Difusión | O(grid²) | O(grid²) |
| L-Systems | O(segments) | O(maxLength) |
| Flow Fields | O(particles) | O(particles) |
| Strange Attractors | O(speed) | O(trail) |
| Phyllotaxis | O(seeds) | O(seeds) |
| Fractales IFS | O(points) | O(maxPoints) |
| Teselaciones | O(triangles) | O(triangles) |

---

**Última actualización:** 2026-01-10
