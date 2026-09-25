# 🤖 Trabajo Práctico N° 3: Búsqueda Informada y Exploración (Búsqueda Heurística)
## Cátedra: Laboratorio I &bull; Área de Inteligencia Artificial y Robótica
### Universidad Católica de Santiago del Estero (UCSE) &bull; Departamento Académico San Salvador (DASS)
**Carrera:** Tecnicatura Universitaria en Automatización y Robótica / Informática  
**Docente / Jefe de Trabajos Prácticos:** Ing. Fabio D. Argañaraz  
**Ciclo Lectivo:** 2026 &bull; **Modalidad:** Individual &bull; Autoevaluativo  

---

## 🎯 Objetivos de Aprendizaje

Al completar este Trabajo Práctico, el estudiante será capaz de:
1. **Comprender el rol del conocimiento del dominio** mediante funciones heurísticas $h(n)$ que estiman el costo restante hacia la meta para evitar la ineficiencia de la exploración a ciegas en el espacio de estados.
2. **Analizar la Búsqueda Voraz Primero el Mejor (Greedy Best-First Search)**:
   - Evaluación guiada exclusivamente por $f(n) = h(n)$.
   - Uso de la heurística de distancia en línea recta ($h_{\text{DLR}}$ / SLD) hacia el objetivo.
   - Evaluación crítica de su miopía local, falta de optimalidad e incompletitud en búsqueda en árboles (análisis del contraejemplo Iasi &rarr; Fagaras y el callejón sin salida de Neamt).
3. **Formalizar y ejecutar el algoritmo $A^*$ (A-Estrella)**:
   - Función de evaluación canónica $f(n) = g(n) + h(n)$, interpretada como el costo total estimado más barato de una solución completa a través del nodo $n$.
   - Criterio de test de meta tardío (al extraer de la cola de prioridad para expansión, nunca al generar).
   - Trazabilidad rigurosa en el mapa de Rumania (Arad a Bucarest), demostrando la selección de Pitesti ($f=417$) sobre Bucarest ($f=450$) para hallar la ruta óptima de 418 km.
4. **Dominar las Condiciones Matemáticas de Optimalidad para $A^*$**:
   - **Heurística Admisible:** $h(n) \le h^*(n)$ y $h(\text{meta}) = 0$. Garantiza la optimalidad en búsqueda en árboles.
   - **Heurística Consistente (Monótona):** Desigualdad triangular $h(n) \le c(n, a, n') + h(n')$. Garantiza la optimalidad en búsqueda en grafos sin requerir reabrir estados ya cerrados.
   - Demostración de que la consistencia implica admisibilidad.
5. **Diagnosticar el cuello de botella de memoria de $A^*$ y aplicar técnicas de memoria acotada**:
   - Comprensión de por qué $A^*$ agota la memoria RAM ($O(b^d)$) mucho antes de agotar el tiempo de CPU.
   - **IDA* ($A^*$ de Profundidad Iterativa):** Cortes basados en el $f$-coste ($g+h$) en lugar de profundidad entera, actualización dinámica del umbral al menor $f$ excedido y memoria lineal $O(b \cdot d)$.
6. **Comprender la Búsqueda Recursiva del Primero Mejor (RBFS / BRPM)**:
   - Simulación de búsqueda primero el mejor con espacio lineal $O(b \cdot d)$.
   - Uso del parámetro `f_limit` para rastrear la mejor alternativa disponible desde cualquier antepasado.
   - Mecanismo de respaldo (*backed-up value*) al desenrollar la recursión y análisis del riesgo de oscilación/regeneración repetida de nodos.
7. **Diseñar e inventar heurísticas mediante problemas relajados**:
   - Caso del 8-puzzle: análisis formal de $h_1$ (piezas fuera de lugar) y $h_2$ (distancia de Manhattan).
   - Demostración de dominancia matemática ($h_2 \ge h_1$) y su impacto en la reducción de nodos expandidos.
   - Creación de heurísticas admisibles dominantes mediante el operador $\max(h_1, \dots, h_k)$.
8. **Evaluar y sintetizar comparativamente las estrategias informadas** en la matriz de completitud, optimalidad y consumo espacial.

---

## 📚 Mapa Bibliográfico Obligatorio

| Ejercicio | Tema Principal | Capítulo [Russell & Norvig (AIMA 2da/3ra Ed.)](http://jdelagarza.fime.uanl.mx/IA/Libros/inteligencia-artificial-un-enfoque-moderno-stuart-j-russell.pdf) | Diapositivas de Cátedra |
|---|---|---|---|
| **Ej 1** | Fundamentos de Búsqueda Informada y Heurísticas | Cap. 4.1 (*Estrategias de búsqueda con información*, pp. 98-101) | Diapositivas 1 a 5 (*Búsqueda informada y primero el mejor*) |
| **Ej 2** | Búsqueda Voraz Primero el Mejor (Greedy Best-First) | Cap. 4.1.1 (*Búsqueda voraz primero el mejor*, pp. 101-104) | Diapositivas 6 a 11 (*Búsqueda voraz y distancias a Bucarest*) |
| **Ej 3** | Trampas de la Búsqueda Voraz: Caso Iasi &rarr; Fagaras | Cap. 4.1.1 (*Ventajas falsas*, pp. 102-104) | Diapositivas 12 y 13 (*Ventajas falsas / Callejón Neamt*) |
| **Ej 4** | Algoritmo de Búsqueda $A^*$ ($f = g + h$) | Cap. 4.1.2 (*Búsqueda A\**, pp. 104-106) | Diapositivas 14 a 16 (*Búsqueda A\* y función f(n)*) |
| **Ej 5** | Trazabilidad Paso a Paso de $A^*$ en Rumania | Cap. 4.1.2 (Figura 4.4, pp. 104-106) | Diapositivas 17 a 23 (*Traza de Arad a Bucarest con A\**) |
| **Ej 6** | Heurísticas Admisibles y Consistentes | Cap. 4.1.3 (*Condiciones de optimalidad*, pp. 106-110) | Diapositiva 16 (*Condiciones de optimalidad*) |
| **Ej 7** | Desventaja de Memoria de $A^*$ y Algoritmo IDA* | Cap. 4.2.1 (*A\* de profundidad iterativa*, pp. 110-112) | Diapositivas 24 a 26 (*Desventaja de memoria y A\*PI / IDA\**) |
| **Ej 8** | Búsqueda Recursiva del Primero Mejor (RBFS / BRPM) | Cap. 4.2.2 (*Búsqueda recursiva del primero mejor*, pp. 112-115) | Diapositivas 27 a 32 (*BRPM / RBFS y valores respaldados*) |
| **Ej 9** | Diseño e Invención de Heurísticas (8-Puzzle y Relajación) | Cap. 4.3 (*Funciones heurísticas*, pp. 116-121) | Russell & Norvig Cap. 4.3 (*8-puzzle, Manhattan y relajación*) |
| **Ej 10** | Matriz Comparativa de Búsquedas Informadas | Cap. 4.1, 4.2 y 4.4 (pp. 101-115, 122) | Diapositivas 6 a 32 (*Comparación de estrategias informadas*) |

---

## 🚀 Flujo de Trabajo del Estudiante (Paso a Paso)

### 1. Bifurcar y Clonar el Repositorio
1. Ingresa al repositorio oficial de cátedra:  
   [`https://github.com/UCSE-Laboratorio-I/TP3`](https://github.com/UCSE-Laboratorio-I/TP3)
2. Haz clic en el botón superior derecho **Fork** (o **Use this template**) para generar una copia en tu cuenta personal de GitHub.
3. Clona tu repositorio bifurcado en tu computadora:
   ```bash
   git clone https://github.com/TU_USUARIO_GITHUB/TP3.git
   cd TP3
   ```

### 2. Resolver la Guía Interactiva
1. Abre el archivo `index.html` con doble clic en tu navegador web preferido (Chrome, Firefox, Edge, Safari).
2. Completa tus datos personales en la cabecera (Nombre, DNI, Email, Comisión, Usuario de GitHub).
3. Resuelve los 10 ejercicios interactivos. Puedes apoyarte en los paneles desplegables de bibliografía de cada consigna.
4. El progreso se guarda automáticamente en tu navegador (`localStorage`).
5. Al llegar al 100%, haz clic en el botón **📥 Generar y Descargar respuestas_tp3.json** y guárdalo en la raíz del repositorio (`TP3/respuestas_tp3.json`).

### 3. Autoevaluación en Terminal Local
Abre una consola o terminal en la carpeta del repositorio y ejecuta el evaluador oficial en Python:
```bash
python autograder_tp3.py respuestas_tp3.json
```
* El script evaluará tus respuestas mediante firmas criptográficas **SHA-256** salteadas, sin exponer las soluciones correctas en texto claro.
* Si obtienes menos de 100 puntos, te indicará exactamente en qué ítem tuviste discrepancias y qué sección bibliográfica consultar para corregirlo antes de la entrega final.

### 4. Entrega Oficial por Git
Una vez que hayas alcanzado tu puntaje deseado (aprobación: &ge; 4.0 / 10.0; promoción: &ge; 7.0 / 10.0), registra tus cambios y súbelos a tu GitHub:
```bash
git add respuestas_tp3.json
git commit -m "Entrega Trabajo Práctico N° 3 - [Tu Nombre y Apellido]"
git push origin main
```
Luego, comparte el enlace de tu repositorio de GitHub con el equipo docente de **Laboratorio I**.

---

## 🔒 Integridad Académica y Evaluación Segura

* La rúbrica pública `rubric_tp3.json` implementa un esquema de evaluación **Zero-Knowledge** basado en firmas SHA-256 salteadas (`LAB1_IA_2026_CatedraArganaraz_SecretSalt`).
* El script `autograder_tp3.py` evalúa de forma fidedigna y objetiva cada submission sin revelar las claves del docente.
* Se prohíbe el plagio y la copia no autorizada entre estudiantes. Toda entrega está sujeta a auditoría docente.

---
&copy; 2026 Universidad Católica de Santiago del Estero &bull; DASS &bull; Cátedra de Laboratorio I (Ing. Fabio D. Argañaraz)
