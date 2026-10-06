# Evaluación Unidad 1 (Hito 1): Flujo de Análisis Reproducible Carga-Deflexión

**Autor:** Luis Angel Broncano Marcelo  
**Carrera:** Ingeniería Civil en Obras Civiles - Universidad de Santiago de Chile (USACH)  
**Caso de estudio:** Viga simplemente apoyada con carga puntual centrada ($L = 4\text{ m}$, sección $0.2\text{ m} \times 0.4\text{ m}$, $E = 25\text{ GPa}$).

---

## 1. Estructura del Repositorio y Justificación

El proyecto se organiza separando estrictamente los datos crudos de entrada (inmutables), el procesamiento numérico, los recursos gráficos y el código fuente del reporte técnico:

```text
.
├── README.md                       # Documentación general e instrucciones de reproducción
├── USO_IA.md                       # Declaración formal y trazabilidad del uso de IA generativa
├── data/                           # Datos primarios inmutables (SOLO LECTURA)
│   ├── datos_viga.csv              # Serie carga aplicada (kN) y deflexión medida (mm)
│   ├── parametros_viga.xlsx        # Parámetros geométricos (L, b, h) y módulo E
│   └── README_datos.md             # Descripción original de los datos proporcionados
├── analysis/                       # Procesamiento y modelo matemático
│   └── analisis_viga.xlsx          # Conversión de unidades, cálculo de I, delta_teo, errores y verificaciones
├── figures/                        # Recursos visuales trazables
│   ├── esquema_viga.png            # Esquema estático original de la viga
│   └── carga_deflexion.png         # Gráfico comparativo exportado desde el análisis (300 DPI)
└── report/                         # Comunicación técnica en LaTeX
    ├── main.tex                    # Código fuente de la nota técnica
    ├── referencias.bib             # Base de datos bibliográfica en formato BibTeX
    └── nota_tecnica.pdf            # Documento compilado final
```

## 2. Flujo de Reproducción Paso a Paso

Para reproducir íntegramente los resultados desde las entradas hasta el documento PDF final:

1. **Verificación de Datos de Entrada (`data/`):**
   Los archivos `data/datos_viga.csv` y `data/parametros_viga.xlsx` se conservan intactos tal como fueron suministrados.
2. **Reproducción del Análisis Numérico (`analysis/analisis_viga.xlsx`):**
   * Abrir `analysis/analisis_viga.xlsx` en Microsoft Excel o LibreOffice Calc.
   * En la hoja `Parametros_y_Conversion`, revisar la conversión explícita al sistema consistente $(\text{N}, \text{mm})$ y el cálculo del segundo momento de área $I = b h^3 / 12 = 1\,066\,666\,666.67\text{ mm}^4$.
   * En la hoja `Calculos_Deflexion`, inspeccionar las fórmulas vinculadas para la carga en Newtons, la deflexión de Euler-Bernoulli ($\delta_{\text{teo}} = P L^3 / 48 E I$), la diferencia relativa porcentual ($\varepsilon_r$) para $P > 0$ y la flexibilidad ($\delta/P$).
   * En la hoja `Verificacion`, revisar el análisis dimensional, la comprobación manual independiente para $P = 20\text{ kN}$ y la estimación por corte de Timoshenko.
3. **Generación de la Figura (`figures/carga_deflexion.png`):**
   La figura proviene directamente de las columnas `carga_kN`, `deflexion_medida_mm` y `delta_teo_mm` de la hoja `Calculos_Deflexion`.
4. **Compilación de la Nota Técnica (`report/`):**
   En Overleaf o mediante una distribución local de TeX Live / MiKTeX, situarse en el directorio `report/` y ejecutar:
   ```bash
   pdflatex main.tex
   bibtex main
   pdflatex main.tex
   pdflatex main.tex
   ```
   El archivo resultante corresponde a `report/nota_tecnica.pdf`.
