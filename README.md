# 📉 Argentina — Salario Real vs Inflación (2017–2025)

Dashboard de Power BI que analiza la evolución del poder adquisitivo de los trabajadores formales en Argentina, comparando el RIPTE contra el IPC Nacional del INDEC entre enero 2017 y agosto 2025.

---

## 🎯 Pregunta central

> **¿Le ganó el salario a la inflación?**

---

## 📊 Vista previa

![Dashboard](assets/dashboard_preview.png)

---

## 📁 Estructura del repositorio

```
argentina-salario-real-dashboard/
│
├── data/
│   ├── ipc.xlsx                        # Variación mensual IPC Nacional (INDEC)
│   ├── Remuneracion_-_Filtrada.xlsx    # RIPTE mensual (MTEySS)
│   └── cambio_tipo.xlsx                # Tipo de cambio nominal (BCRA)
│
├── docs/
│   ├── PowerBI_Salario_Real_Argentina.docx   # Guía completa de construcción
│   ├── Presentacion_Dashboard.docx           # Explicación del análisis
│   └── Salario_Real_vs_Inflacion.pptx        # Presentación ejecutiva
│
├── assets/
│   └── dashboard_preview.png           # Captura del dashboard final
│
├── README.md
└── requirements.txt
```

---

## 🧱 Modelo de datos

```
dim_Calendario
    │
    ├── 1:* ──► ipc
    ├── 1:* ──► remuneracion
    └── 1:* ──► cambio_tipo
```

La tabla `dim_Calendario` actúa como tabla de fechas central. Todas las relaciones son de uno a muchos con filtro en dirección única.

---

## 📐 Métricas DAX implementadas

| Medida | Descripción |
|--------|-------------|
| `Sal_Nominal` | RIPTE mensual en pesos corrientes |
| `Variacion_Mensual_IPC` | IPC mensual del período |
| `IPC_Acumulado_Index` | Índice de precios acumulado base 100 = Ene 2017 |
| `Inflacion_Interanual_Pct` | Inflación compuesta de los últimos 12 meses |
| `Salario_Real` | Salario deflactado por IPC acumulado |
| `Salario_Real_Index` | Índice de salario real base 100 = Ene 2017 |
| `Salario_Real_YoY_Pct` | Variación interanual del salario real |
| `Variacion_Acumulada_Sal_Real_Pct` | Pérdida o ganancia acumulada desde el año base |
| `Ultimo_Salario_Nominal` | Último valor del RIPTE en el período filtrado |
| `Ultima_Inflacion_Interanual` | Último valor de inflación interanual |
| `Ultimo_Salario_Real_Index` | Último valor del índice de salario real |
| `Ultima_Variacion_Acumulada` | Último valor de variación acumulada |

---

## 🖥️ Layout del dashboard

```
┌─────────────────────────────────────────────────┐
│  ZONA 1 — Título + Slicer de año                │
├──────────┬──────────┬──────────┬────────────────┤
│  KPI 1   │  KPI 2   │  KPI 3   │    KPI 4       │
│  Inflac. │  Sal.Nom │  Índice  │  Var.Acum.     │
├─────────────────────────────────────────────────┤
│  ZONA 3 — Gráfico Combo                         │
│  Columnas: Inflación Interanual %               │
│  Línea:    Salario Real Índice                  │
├──────────────────────┬──────────────────────────┤
│  ZONA 4a             │  ZONA 4b                 │
│  Salario Real YoY %  │  Tabla de datos mensual  │
└──────────────────────┴──────────────────────────┘
```

---

## 📈 Resultados principales

| Período | Salario Real Índice | Resultado |
|---------|-------------------|-----------|
| Ene 2017 (base) | 100,0 | BASE |
| Dic 2017 | 101,7 | ✅ Ganó (+1,7%) |
| Dic 2018 | 89,9 | ❌ Perdió (−10,1%) |
| Dic 2019 | 84,3 | ❌ Perdió (−15,7%) |
| Dic 2020 | 83,6 | ❌ Perdió (−16,4%) |
| Dic 2021 | 85,1 | ❌ Perdió (−14,9%) |
| Dic 2022 | 82,7 | ❌ Perdió (−17,3%) |
| Dic 2023 | ~65 | ❌ Peor momento (shock devaluatorio) |
| Dic 2024 | 75,6 | ❌ Perdió (−24,4%) |
| Ago 2025 | 80,5 | ↗ Recuperando (−19,5%) |

**Conclusión: El salario perdió contra la inflación en 7 de los 8 años analizados. La pérdida acumulada al cierre del período es de −19,5%.**

---

## 🗂️ Fuentes de datos

| Dataset | Fuente | Frecuencia |
|---------|--------|------------|
| IPC Nacional | INDEC | Mensual |
| RIPTE | MTEySS | Mensual |
| Tipo de cambio nominal | BCRA | Mensual |

**Período:** Enero 2017 — Agosto 2025 (104 meses)

---

## 🛠️ Requisitos

Ver `requirements.txt` para las versiones de software utilizadas.

---

## 📄 Licencia

Este proyecto es de uso educativo y académico.
