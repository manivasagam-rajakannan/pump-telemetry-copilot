# Pump Telemetry Copilot

Predictive maintenance for a simulated industrial pump. The Streamlit operator screen scores vibration, temperature, pressure, and motor current. FastAPI stores the scored readings in PostgreSQL, and Power BI Desktop displays alerts through DirectQuery.

## Try the demo on Windows

1. Extract or clone the repository. Open `pump-telemetry/OPEN_OPERATOR_SCREEN.cmd` and keep the terminal open.
2. In **Upload pump readings**, select `samples/pump-readings.xlsx` and click **Score and send to live feed**. The workbook contains one normal reading and one overheating alert. **Run sample CSV** opens the same demo with built-in readings.
3. Open `pump-telemetry/Pump_Maintenance_Live.pbip` in Power BI Desktop. Use **Database** authentication and the read-only connection details printed by the launcher. On **Live Monitor**, find the overheating alert by its IST timestamp.

The app accepts tabular sensor readings from CSV, Excel, JSON, XML, Parquet, Word tables, and PDFs with selectable text. The sample workbook shows the required headings and units.

## How the project works

The Random Forest model scores each reading. Sensor rules suggest a fault type, and the operator can open the corresponding training-manual checklist. Both the operator screen and Power BI query the same stored event.

In the chronological synthetic holdout, the model flagged 32 of 33 injected faults and produced zero false alerts among 967 nominal readings. [Evaluation metrics](pump-telemetry/data/model_metrics.json)

See the [Pump setup and project files](pump-telemetry/README.md) and the [combined deployment with Maintenance Watch](https://github.com/manivasagam-rajakannan/industrial-predictive-maintenance/tree/portfolio-apps).
