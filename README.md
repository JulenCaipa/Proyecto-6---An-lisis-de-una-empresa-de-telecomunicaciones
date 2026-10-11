# Análisis ConnectaTel 📱

Análisis exploratorio del comportamiento de uso de los clientes de **ConnectaTel**, una empresa de telecomunicaciones con operaciones en México y Colombia. El proyecto identifica patrones de consumo de llamadas y mensajes, detecta comportamientos atípicos y segmenta a los clientes para proponer mejoras en la oferta comercial.

## 🎯 Objetivo del proyecto

Responder a las siguientes preguntas de negocio:

- ¿Qué segmentos de clientes muestran mayor o menor uso de llamadas y mensajes?
- ¿Qué usuarios presentan valores atípicos que puedan indicar comportamientos inusuales, fraude o errores de registro?
- ¿Cómo varía el uso según la edad y el tipo de plan contratado?
- ¿Qué patrones pueden ayudar a diseñar mejores planes y mejorar la satisfacción del cliente?

## 📂 Datasets utilizados

| Archivo | Descripción | Tamaño |
|---|---|---|
| `plans.csv` | Catálogo de planes (Básico y Premium): precio mensual, minutos, mensajes y GB incluidos, y costo por excedente. | 2 filas, 8 columnas |
| `users_latam.csv` | Información de los clientes: edad, ciudad, fecha de registro, plan contratado y fecha de cancelación. | 4,000 filas, 8 columnas |
| `usage.csv` | Registro de uso real durante 2024: llamadas (duración en minutos) y mensajes (longitud en caracteres). | 40,000 filas, 6 columnas |

## 🔄 Etapas del análisis

1. **Carga y exploración:** revisión de la estructura, tipos de datos y primeras filas de cada dataset.
2. **Identificación de problemas de calidad:** conteo de nulos, detección de sentinels (`-999` en edad, `"?"` en ciudad) y fechas imposibles (año 2026).
3. **Limpieza básica:** reemplazo de sentinels, conversión de fechas y verificación de que los nulos de `duration` y `length` son MAR (dependen del tipo de registro).
4. **Resumen estadístico:** agregación del uso por usuario (mensajes, llamadas y minutos) y combinación con los datos de clientes.
5. **Visualización y outliers:** histogramas por plan, boxplots y cálculo de límites con el método IQR.
6. **Segmentación:** clasificación de clientes por nivel de uso (Bajo, Medio, Alto) y por grupo de edad (Joven, Adulto, Adulto Mayor).
7. **Insight ejecutivo:** conclusiones y recomendaciones comerciales.

## 💡 Principales hallazgos

- El **73.6%** de los clientes tiene un uso medio, el **19.5%** un uso bajo y solo el **7%** un uso alto.
- Los clientes Básico y Premium tienen patrones de consumo muy similares: el plan Premium **no se traduce en mayor uso**.
- La mayoría de clientes consume muy por debajo de lo que incluye su plan.
- La edad casi no influye en el nivel de uso, por lo que las ofertas deberían diseñarse según el consumo.
- Se detectó un grupo de usuarios, principalmente Premium, con entre 120 y 155 minutos de llamadas, que conviene investigar.

## 🛠️ Herramientas

- Python 3.9
- pandas, numpy
- matplotlib, seaborn
- Jupyter Notebook

## ▶️ Cómo ejecutar el notebook

### Opción 1: Google Colab

1. Abre [Google Colab](https://colab.research.google.com/).
2. Ve a **Archivo → Abrir notebook → GitHub** y pega la URL de este repositorio.
3. Sube los tres archivos CSV a la sesión de Colab (ícono de carpeta en el panel izquierdo).
4. Ajusta las rutas de carga en el paso 1.1 para que apunten a los archivos subidos, por ejemplo:
   ```python
   plans = pd.read_csv('plans.csv')
   users = pd.read_csv('users_latam.csv')
   usage = pd.read_csv('usage.csv')
   ```
5. Ejecuta todo con **Entorno de ejecución → Ejecutar todas**.

### Opción 2: Jupyter local

1. Clona el repositorio:
   ```bash
   git clone <URL-de-este-repositorio>
   ```
2. Instala las dependencias:
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
3. Coloca los archivos CSV en una carpeta y ajusta las rutas del paso 1.1.
4. Abre el notebook con `jupyter notebook` y ejecuta **Kernel → Restart & Run All**.

## 🔁 Guía de reproducción

- Ejecuta las celdas **en orden, de arriba hacia abajo**. La limpieza del paso 3 debe aplicarse antes de crear `user_profile` en el paso 4; si se ejecuta fuera de orden, los sentinels permanecen en los datos.
- Si vuelves a cargar los CSV, repite todos los pasos desde la limpieza.
- La forma más segura de reproducir los resultados es **Restart & Run All**.

## 📁 Estructura del repositorio

```
├── README.md
└── ConnectaTel_analisis.ipynb
```
