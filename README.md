# 📊 Análisis de Estructuras de Datos en Bases de Datos
> **Proyecto para la asignatura de Estructura de Datos - ITM (2026-1)**

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white" alt="SQLite" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas" />
</p>

## 📝 Descripción
Este proyecto analiza la eficiencia de las estructuras de datos aplicadas a bases de datos a gran escala. Comparamos el rendimiento de una **búsqueda lineal** frente a una **búsqueda indexada mediante B-Trees** utilizando un dataset de salud estudiantil con 1,000,000 de registros.

## 📂 Dataset
* **Fuente:** [Student Health Dataset - Kaggle](https://www.kaggle.com/datasets/ayeshasiddiqa123/student-health).
* **Descripción:** Contiene información sobre salud física y mental de estudiantes, incluyendo niveles de estrés, actividad física y métricas de salud en 1 millón de filas y 21 columnas.

## ⚙️ Tecnologías
* **Lenguaje:** Python 3.x.
* **Librerías:** `pandas` para manejo de datos, `sqlite3` para el motor de base de datos y `time` para métricas de rendimiento.

---

## 🛠️ Implementación

<details>
<summary><b>Click para ver detalles técnicos (Algoritmia y Matemáticas)</b></summary>

### Fundamentos del B-Tree
Para optimizar la recuperación de información, implementamos un índice en SQLite que utiliza un **B-Tree**. Esta estructura permite una complejidad de búsqueda de $O(\log n)$.

**Comparativa de Complejidad:**
| Método | Estructura | Complejidad | Pasos (n=1M) |
| :--- | :--- | :--- | :--- |
| **Secuencial** | Lista Plana | $O(n)$ | ~1,000,000 |
| **Indexado** | B-Tree | $O(\log n)$ | ~3 - 5 |

</details>

## 🚀 Ejecución
Para ejecutar el proyecto y replicar la demostración de rendimiento, primero se debe descargar el dataset student_mental_health_burnout_1M.csv y ubicarlo en el entorno de trabajo. Luego, es necesario actualizar la ruta del archivo en el script, dentro de la función pd.read_csv(), apuntando a la ubicación exacta, y ejecutar el código en su totalidad. El programa se encargará automáticamente de procesar el millón de registros, generar las dos bases de datos físicas (una con escaneo secuencial y otra indexada) y realizar la búsqueda de prueba. Finalmente, el script imprimirá directamente en la consola los tiempos de respuesta de ambos métodos junto con el cálculo exacto de mejora, evidenciando numéricamente la eficiencia de la estructura B-Tree.
```bash
import pandas as pd
import sqlite3
import time
import matplotlib.pyplot as plt

data = pd.read_csv("/content/student_mental_health_burnout_1M.csv")

data.insert(0,"estudiante_id", range(1, len(data) + 1))

Db_desordenada=sqlite3.connect("Db_desordenada.db")
data.to_sql("estudiante",Db_desordenada, index=False, if_exists="replace")
Db_desordenada.close()


Db_ordenada=sqlite3.connect("Db_ordenada.db")
data.to_sql("estudiante",Db_ordenada, index=False, if_exists="replace")
cursor = Db_ordenada.cursor()
cursor.execute("CREATE INDEX idx_estudiante ON estudiante(estudiante_id);")
Db_ordenada.close()

print("Bases de datos creada correctamente")


def busqueda(db_fila,e):
  conn = sqlite3.connect(db_fila)
  cursor = conn.cursor()

  inicio= time.time()
  cursor.execute("SELECT *FROM estudiante WHERE estudiante_id = ?",(e,))
  resultado = cursor.fetchone()
  fin = time.time()
  conn.close()
  tiempo_ms = (fin-inicio)*1000

  return resultado , tiempo_ms

buscar = 999999

res1, tiempo_caos = busqueda("Db_desordenada.db", buscar)
print(f"el tioempo de ejecucion sin {tiempo_caos:.4F}")

res2, tiempo_idx = busqueda("Db_ordenada.db", buscar)
print(f"el tioempo de ejecucion con {tiempo_idx:.4F}")


mejora = tiempo_caos/tiempo_idx

print(f"Tiempo de mejor es {mejora}")


## 📝 Autores
Alber Dubian Ramirez Giraldo
Samuel Isaac Acevedo Gómez
Nauer Suaza Isaza

