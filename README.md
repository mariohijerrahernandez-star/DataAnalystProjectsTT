# Proyecto ConnectaTel: Segmentación de clientes por uso y edad

## Objetivo

Analizar el comportamiento de los usuarios de ConnectaTel (llamadas, mensajes, minutos, edad y plan) para detectar problemas de calidad en los datos, segmentar a los clientes y proponer recomendaciones comerciales: mejoras a los planes actuales y posibles planes nuevos.

## Datasets utilizados

| Dataset | Descripción | Columnas principales |
|---|---|---|
| `users` | 4,000 usuarios registrados | `user_id`, `age`, `city`, `plan`, `reg_date` |
| `usage` | 40,000 registros de uso (llamadas y mensajes) | `id`, `user_id`, `type`, `duration`, `length`, `date` |
| `plans` | Descripción de los planes (solo 2 filas: Basico y Premium) |

Notas:
- `type` toma los valores `call` (llamada) y `text` (mensaje).
- `duration` solo aplica a llamadas y `length` solo a mensajes, por eso tienen muchos nulos estructurales.
- Los datos están registrados hasta el año 2024.

## Etapas del análisis

1. **Carga y exploración inicial** de los datasets.
2. **Detección de valores inválidos y sentinels:**
   - `age` con el valor `-999`.
   - `city` con `"?"` y formatos mezclados.
   - Fechas imposibles (año 2026, posterior al límite de 2024).
   - Nulos en `duration` y `length` (patrón MAR según `type`).
3. **Limpieza:**
   - `-999` en `age` reemplazado por la mediana.
   - `"?"` en `city` reemplazado por nulos.
   - Fechas fuera de rango marcadas como nulas.
4. **Construcción de la tabla por usuario (`user_profile`):** agregación de `usage` por `user_id` (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`) y unión con `users`.
5. **Resumen estadístico** de las variables numéricas y distribución del plan.
6. **Visualización de distribuciones:** histogramas por plan.
7. **Detección de outliers:** boxplots y método IQR.
8. **Segmentación de clientes:**
   - `grupo_uso`: Bajo uso, Uso medio, Alto uso.
   - `grupo_edad`: Joven, Adulto, Adulto Mayor.
9. **Insight ejecutivo:** conclusiones y recomendaciones para el negocio.

## Cómo ejecutar el notebook

### Opción A: Google Colab

1. Entra a [colab.research.google.com](https://colab.research.google.com).
2. Ve a **Archivo → Subir cuaderno** y selecciona `S7 Version-Estudiante-Project-ConnectaTel.ipynb` (o abre el notebook desde GitHub con **Archivo → Abrir cuaderno → GitHub**).
3. Sube los archivos de datos al entorno de Colab (panel de archivos de la izquierda) o móntalos desde Google Drive.
4. Ajusta las rutas de lectura (por ejemplo `pd.read_csv('/content/users.csv')`) a donde hayas guardado los archivos.
5. Ejecuta **Entorno de ejecución → Ejecutar todo**.

### Opción B: Jupyter local

```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook
```

Abre el notebook y ajusta las rutas de los datasets a tu carpeta local.

## Guía de reproducción

1. Clona o descarga este repositorio: `[URL del repositorio]`.
2. Coloca los datasets (`users`, `usage`, `plans`) en la ruta que usa el notebook.
3. Instala las dependencias: `pandas`, `numpy`, `matplotlib`, `seaborn`.
4. Ejecuta el notebook **de arriba hacia abajo y en orden**, porque cada celda depende de las anteriores (por ejemplo, `user_profile` se crea a partir de `usage_agg`).
5. Si aparece un `NameError`, reinicia el kernel y usa **Restart & Run All**.

## Estructura del repositorio

├── README.md
├── S7 Version-Estudiante-Project-ConnectaTel.ipynb


## Autor

`Mario Hijerra`

## Autor

`[Tu nombre]`
