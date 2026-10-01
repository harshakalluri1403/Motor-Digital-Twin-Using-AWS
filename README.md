<div align="center">

# Motor Digital Twin on AWS

### A live, 3D virtual replica of a factory motor — SiteWise ingests, TwinMaker models, Grafana shows it

![AWS IoT SiteWise](https://img.shields.io/badge/AWS-IoT%20SiteWise-232F3E?logo=amazonaws&logoColor=white)
![AWS IoT TwinMaker](https://img.shields.io/badge/AWS-IoT%20TwinMaker-232F3E?logo=amazonaws&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-dashboards-F46800?logo=grafana&logoColor=white)
![Python](https://img.shields.io/badge/python-boto3-3776AB?logo=python&logoColor=white)
![Status](https://img.shields.io/badge/status-demo-lightgrey)
![License](https://img.shields.io/badge/license-MIT-blue)

[Architecture](#architecture) ·
[Data flow](#data-flow) ·
[Dashboards](#dashboards) ·
[Setup](#setup)

</div>

---

A **digital twin** is a live virtual model of a physical thing, fed by that
thing's real sensor data. This project builds one for a factory motor: speed
readings stream into AWS, a 3D model of the motor is wired to them in IoT
TwinMaker, and Grafana renders the whole thing on a dashboard you can watch in
real time.

<p align="center">
<img src="Screenshot%202024-11-03%20020128.png" width="80%" alt="System architecture diagram">
</p>

## Architecture

```
 Factory motor ─▶ AWS IoT SiteWise ─▶ AWS IoT TwinMaker ─▶ Grafana
   (speed data)     models & assets      3D digital twin     live dashboards
```

| Component | Role |
| :--- | :--- |
| **Motor** | The physical asset producing real-time speed data |
| **AWS IoT SiteWise** | Models the motor as an asset and ingests its measurements |
| **AWS IoT TwinMaker** | Binds a 3D model ([`models/motor.glb`](models/motor.glb)) to the live SiteWise data |
| **Grafana** | Visualizes speed and KPIs on real-time panels |

## Data flow

For a working demo without physical hardware,
[`scripts/senddata.py`](scripts/senddata.py) simulates the motor: once a second
it generates a speed between 100–1000 and pushes it to the SiteWise property
alias `/factory/Motor1/Speed` via `boto3`.

```python
client.batch_put_asset_property_value(entries=payload['entries'])
```

Point it at your region and asset alias, run it, and SiteWise → TwinMaker →
Grafana light up with live values.

## Dashboards

<p align="center">
<img src="Screenshot%202024-11-03%20010927.png" width="46%" alt="Grafana motor dashboard">
<img src="Screenshot%202024-11-03%20010941.png" width="46%" alt="Grafana panel view">
</p>
<p align="center">
<img src="Screenshot%202024-11-03%20010951.png" width="46%" alt="TwinMaker 3D scene">
<img src="Screenshot%202024-11-03%20010959.png" width="46%" alt="Grafana KPI panel">
</p>

## Setup

1. **SiteWise** — define the motor as an asset and add a *Speed* property.
2. **TwinMaker** — create a workspace, import the 3D model
   [`models/motor.glb`](models/motor.glb), and bind its component to the
   SiteWise Speed property.
3. **Feed data** — set your region and alias in
   [`scripts/senddata.py`](scripts/senddata.py), then:
   ```bash
   pip install boto3
   aws configure          # credentials with SiteWise write access
   python scripts/senddata.py
   ```
4. **Grafana** — add the AWS IoT TwinMaker data source and build panels for
   motor speed and other KPIs.

## Roadmap

- **Predictive maintenance** — flag likely failures from speed patterns
- **More signals** — temperature, vibration, current
- **Alerting** — Grafana alerts on abnormal behavior

## Tech stack

AWS IoT SiteWise · AWS IoT TwinMaker · Grafana · Python · boto3 · glTF (`.glb`)

## License

Released under the [MIT License](LICENSE).
