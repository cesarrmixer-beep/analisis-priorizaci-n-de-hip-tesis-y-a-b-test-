# 🧪 Priorización de Hipótesis y Análisis de A/B Test para E-commerce

> ¿Qué ideas de marketing probar primero para no quemar presupuesto y cómo validar con estadística que realmente aumentan los ingresos?

📊 **Datasets:** `hypotheses_us.csv` | `orders_us.csv` | `visits_us.csv`
🐍 **Stack:** Python | Pandas | Matplotlib | SciPy | Estadística Inferencial

---

### [priorizacion_hipotesis.ipynb]

---

### 🎯 Contexto de Negocio

Eres analista en una gran tienda online. Marketing tiene 9 hipótesis para aumentar ingresos, pero solo hay recursos para probar 2-3.

**Mi rol:** 
1. Priorizar qué hipótesis probar primero (que no se desperdicie dinero).
2. Analizar un A/B Test real y decir si paramos, seguimos o declaramos ganador.

---

### 🔍 Parte 1: Priorización de Hipótesis (ICE vs RICE)

**Problema:** 9 hipótesis con Reach, Impact, Confidence, Effort.

**Qué hice:**

**1. Framework ICE Score = (Impact * Confidence) / Effort**
Ordené de mayor a menor. ICE premia lo fácil y rápido de implementar.

**2. Framework RICE Score = (Reach * Impact * Confidence) / Effort**
Ordené de mayor a menor. RICE premia lo que impacta a MÁS usuarios.

**3. Hallazgo Clave - Cómo cambia la priorización:**
> Cuando usamos RICE en lugar de ICE, 2 hipótesis que estaban en top 3 caen al lugar 6 y 7. ¿Por qué? Porque tenían alto Impact pero bajo Reach (afectaban a muy pocos usuarios). ICE las inflaba porque eran fáciles. RICE las castiga correctamente porque aunque son fáciles, no escalan.
> 
> **Decisión:** Usar RICE para roadmap trimestral (pensar en escala) e ICE para sprints semanales (quick wins).

---

### 🧪 Parte 2: Análisis de A/B Test

Realicé un A/B Test con datos de órdenes y visitas. Detecté y corregí errores críticos antes de analizar.

**Limpieza previa (Preprocesamiento):**
- Detecté usuarios duplicados que entraron tanto en grupo A como en B (error de asignación). Los eliminé del análisis.
- Validé fechas y conversión diaria.

**Análisis Exploratorio que realicé:**

1.  **Ingreso acumulado por grupo:** Gráfico de líneas acumuladas. El grupo B toma ventaja desde el día 12.
2.  **Ticket promedio acumulado:** B es 8% superior a A de forma consistente.
3.  **Diferencia relativa ticket B vs A:** Se estabiliza en +8% después del día 15.
4.  **Tasa de conversión diaria:** B convierte 2.3% vs A 1.9% diario. Diferencia sostenida, no pico de un día.
5.  **Pedidos por usuario (scatter):** Detecté usuarios con 15+ pedidos (posibles bots / testers).
6.  **Anomalías - Percentiles 95 y 99 pedidos/usuario:** P95=3 pedidos, P99=7 pedidos. Defino anomalía >7 pedidos.
7.  **Precios de pedidos (scatter):** Órdenes con precio >$1000 USD (anomalías).
8.  **Anomalías - Percentiles 95 y 99 precio:** P95=$450, P99=$890. Defino anomalía >$890.

**Validación Estadística:**

**Con datos en bruto (sin filtrar):**
- Conversión: p-value = 0.12 (NO significativo, contaminado por anomalías)
- Ticket promedio: p-value = 0.08 (NO significativo)

**Con datos filtrados (sin anomalías y sin usuarios duplicados):**
- Conversión: p-value = 0.003 (<0.05) -> **SÍ significativo**
- Ticket promedio: p-value = 0.01 (<0.05) -> **SÍ significativo**

> **Por qué cambia:** Las anomalías (pedidos de $1000 y usuarios con 15 órdenes) inflaban la varianza y escondían el efecto real. Al filtrar, el efecto se vuelve claro.

---

### 💼 Decisión Final del Experimento

**Decisión: OPCIÓN 1 - Parar la prueba, considerar al Grupo B como líder con el 15.3% de mejor conversion.**

**Justificación:**
### Se tomarón en cuenta los datos crudos y tratados, y en ambas condiciones el grupo B lidereo, tenemos evidencia solida y no es necessario extender mas la prueba, se recomienda impulsar al grupo B con mas acciones de publicidad o marketing, ya que sus picos fueron en dias muy especificos, pero durantre el periodo de tiempo, se mantubo con paso firme y constante.

---

### 📈 Visualizaciones Clave
[priorizacion_hipotesis.ipynb

### 👨‍💻 Autor
Cesar R. | Data Analyst Jr. | GDL

