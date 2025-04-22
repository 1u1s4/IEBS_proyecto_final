# Determinantes Socioeconómicos de la Pobreza en Guatemala  
**Selección de características con Boruta + XGBoost**

> Proyecto final del **Posgrado en Big Data – IEBS**  
> **Alumno:** Luis Alfredo Alvarado Rodríguez

---

## Resumen

A partir del microdato de la **ENCOVI 2014**, este proyecto identifica los factores que mejor explican la condición de pobreza de los hogares guatemaltecos.  
Se construye una base consolidada de 31 variables socioeconómicas y se aplica el algoritmo **Boruta** (con un clasificador **XGBoost**) para contrastar la importancia real de cada variable frente a sus versiones aleatorias (“sombras”).  
El procedimiento conservó **14 variables** verdaderamente relevantes—entre ellas alfabetización, tiempo de traslado a centros educativos y acceso a servicios básicos—y descartó otras (p. ej. uso de crédito), ofreciendo evidencia para la focalización de políticas públicas.

---

## Estructura del repositorio

```
IEBS_proyecto_final
├── data/                      # Archivos .sav y base integrada db.csv
├── extraccion.ipynb           # Integración y limpieza del microdato
├── boruta.ipynb               # Selección de variables y modelado
├── requirements.txt           # Dependencias de Python
├── TF_Luis_Alvarado_210425.*  # Informe final (PDF / DOCX)
└── Pautas...docx              # Material de apoyo
```

---

## Instalación rápida

```bash
# 1. Crear entorno virtual
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# 2. Instalar dependencias
pip install -r requirements.txt
```

> **Nota:** *Boruta* < 0.4.4 requiere un pequeño arreglo para alias deprecados de NumPy; ya está cubierto en los notebooks.

---

## Guía de uso

| Paso | Archivo | Descripción |
|------|---------|-------------|
| 1 | `extraccion.ipynb` | Integra los `.sav` de ENCOVI en `data/db.csv` usando agrupaciones vectorizadas y limpieza de *NaN*. |
| 2 | `boruta.ipynb` | Escala los datos, ejecuta BorutaPy + XGBClassifier, muestra el ranking de variables y evalúa el modelo con F1 y AUC‑ROC macro. |

### Ejecución vía CLI (opcional)

```bash
jupyter nbconvert --execute --inplace extraccion.ipynb
jupyter nbconvert --execute --inplace boruta.ipynb
```

---

## Principales resultados

| Métrica (modelo final) | Valor |
|------------------------|-------|
| **Accuracy**           | 0.608 |
| **F1 macro**           | 0.549 |
| **AUC‑ROC macro**      | 0.772 |

Variables más influyentes según Boruta (⊕ = retenida):

* ⊕ `P06B01` – Alfabetización (leer / escribir)  
* ⊕ `P06B10B` – Minutos hasta el centro educativo  
* ⊕ `P09F09B/C` – Horas / minutos de entretenimiento (TV, Internet)  
* ⊕ `P11A05B` / `P11A06B` – Ayudas internas y remesas externas  
* ⊕ `P13A02A` – Nº de negocios del hogar  

(Consulta **boruta.ipynb** para la lista completa y rangos de importancia.)

---

## Reproducibilidad

* Todos los pasos están documentados; basta con los notebooks y la carpeta `data/`.
* Los hiperparámetros clave permanecen fijados (`random_state=42`) para reproducir los resultados.

---

## Licencia

Este repositorio se publica bajo la **MIT License** salvo indicación contraria.

---

## Referencias

* Narciso Cruz, J. (2014). **ENCOVI 2014**. Instituto Nacional de Estadística – Guatemala.  
* Kursa, M. B., & Rudnicki, W. R. (2010). *Feature Selection with the Boruta Package.* Journal of Statistical Software.  
* Chen, T., & Guestrin, C. (2016). *XGBoost: A Scalable Tree Boosting System.* KDD’16.

---

**¿Dudas o sugerencias?**  
Abre un *issue* o contacta a **@LuisAlvarado** en GitHub.

