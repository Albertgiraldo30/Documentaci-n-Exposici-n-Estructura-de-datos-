# 📊 Análisis de Estructuras de Datos en Bases de Datos
> **Proyecto para la asignatura de Estructura de Datos - ITM (2026-1)**

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white" alt="SQLite" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas" />
</p>

## 📝 Descripción
[cite_start]Este proyecto analiza la eficiencia de las estructuras de datos aplicadas a bases de datos a gran escala[cite: 44]. [cite_start]Comparamos el rendimiento de una **búsqueda lineal** frente a una **búsqueda indexada mediante B-Trees** utilizando un dataset de salud estudiantil con 1,000,000 de registros[cite: 11, 21].

## 📂 Dataset
* [cite_start]**Fuente:** [Student Health Dataset - Kaggle](https://www.kaggle.com/datasets/ayeshasiddiqa123/student-health)[cite: 24].
* **Descripción:** Contiene información sobre salud física y mental de estudiantes, incluyendo niveles de estrés, actividad física y métricas de salud en 1 millón de filas y 21 columnas.

## ⚙️ Tecnologías
* [cite_start]**Lenguaje:** Python 3.x[cite: 26].
* [cite_start]**Librerías:** `pandas` para manejo de datos, `sqlite3` para el motor de base de datos y `time` para métricas de rendimiento[cite: 27].

---

## 🛠️ Implementación

<details>
<summary><b>Click para ver detalles técnicos (Algoritmia y Matemáticas)</b></summary>

### Fundamentos del B-Tree
Para optimizar la recuperación de información, implementamos un índice en SQLite que utiliza un **B-Tree**. [cite_start]Esta estructura permite una complejidad de búsqueda de $O(\log n)$[cite: 9, 29, 61].

**Comparativa de Complejidad:**
| Método | Estructura | Complejidad | Pasos (n=1M) |
| :--- | :--- | :--- | :--- |
| **Secuencial** | Lista Plana | $O(n)$ | ~1,000,000 |
| **Indexado** | B-Tree | $O(\log n)$ | ~3 - 5 |

</details>

## 🚀 Ejecución
Para replicar los resultados, clona este repositorio y ejecuta:
```bash
python main.py
