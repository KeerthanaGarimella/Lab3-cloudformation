# Monolith Analysis App with OpenTelemetry – Keerthana Garimella

📌 **Overview**  
This is a Flask-based monolithic web application that simulates a dice roll and demonstrates observability using **OpenTelemetry**. The application is instrumented to export **traces**, **metrics**, and **logs** to **SigNoz** via OTLP over HTTP, making it easy to monitor errors and performance in real-time.

---

## 🚀 Features

- 🎯 Dice Roll Simulation via `/` or `/rolldice` endpoint
- 📈 Automatic and manual **OpenTelemetry Tracing**, **Metrics**, and **Logging**
- ⚠️ Exception Logging when dice roll results in a 6
- 📡 Seamless integration with **SigNoz** (using OTLP HTTP Exporter)
- 🧪 Demonstrates observability for errors and system behavior

---

## 🛠️ Prerequisites

- Python 3.12+
- Docker installed and running
- GitHub Codespace or local terminal
- SigNoz running (OTLP endpoint default: `http://localhost:4318`)
- Python packages:
  - `flask`
  - `opentelemetry-distro`
  - `opentelemetry-exporter-otlp`
  - `opentelemetry-instrumentation-flask`

---

## 📦 Installation & Setup

### 1. Clone Keerthana’s Repository

```bash
git clone https://github.com/KeerthanaGarimella/InclassTask-3.git
cd InclassTask-3
2. Install Dependencies
bash
pip install flask opentelemetry-distro opentelemetry-exporter-otlp opentelemetry-instrumentation-flask
3. Start SigNoz (if not already running)
bash
git clone https://github.com/SigNoz/signoz.git
cd signoz/deploy/docker
docker-compose -f docker-compose.yaml up -d
SigNoz UI: http://localhost:3301
OTLP Receiver: http://localhost:4318

▶️ Running the App
🔹 Option 1: Manual Instrumentation (from app.py)
bash
cd monolith
python app.py
Open in browser:

ruby
http://localhost:3000/?player=Keerthana
🔹 Option 2: Auto-Instrumentation with CLI
bash
export OTEL_PYTHON_LOGGING_AUTO_INSTRUMENTATION_ENABLED=true
opentelemetry-instrument \
  --logs_exporter otlp \
  --metrics_exporter otlp \
  --traces_exporter otlp \
  --service_name flask-otel \
  flask run -p 8081
Open:
Edit
http://localhost:8081/rolldice?player=Keerthana
🌐 Usage
Each time the route is accessed, a dice roll is simulated and:

Metrics are recorded using roll_counter

Traces and attributes are exported to SigNoz

If the dice roll is 6, an exception is raised and logged in SigNoz

🧪 Testing Exceptions
To simulate and track exceptions:

python
def roll():
    number = randint(1, 6)
    if number == 6:
        raise Exception("Simulated dice roll failure!")
    return number
Refresh the route until a 6 is rolled. Then, check SigNoz’s Traces and Exceptions tabs for the logged error.

🔍 Observability in SigNoz
📊 Metrics: roll.value counter

🧵 Traces: /rolldice span with attributes like player, roll.value

❗ Exceptions: Simulated dice roll failure!

📁 Repository Info
GitHub Link:
https://github.com/KeerthanaGarimella/InclassTask-3

Author:
Keerthana Garimella
Monolith Observability Task – INFO8985