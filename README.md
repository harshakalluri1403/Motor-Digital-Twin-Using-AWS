# Motor Digital Twin using AWS
This project demonstrates a digital twin model for monitoring a motor's speed using AWS IoT SiteWise, AWS IoT TwinMaker, and Grafana. The main focus of this project is to capture and visualize real-time speed data from a motor in a factory setting. By leveraging AWS services, we create a digital twin of the motor to provide detailed insights into its operational status.

## Project Overview
### Architecture
The system architecture consists of:
1. Factory Motor: The physical motor in a factory environment, which provides real-time speed data.
2. AWS IoT SiteWise: Used to create and manage models and assets. It captures motor data (speed) and sends it to the AWS cloud.
3. AWS IoT TwinMaker: Enables the creation of a digital twin of the motor. TwinMaker builds a virtual workspace where data from the physical motor is integrated and visualized.
4. Grafana: Used for visualizing motor metrics. Through dashboards and panels, Grafana displays the speed of the motor, along with other key performance indicators.

### Workflow
- Data Collection: Motor speed data is collected and sent to AWS IoT SiteWise.
- Data Modeling: AWS IoT TwinMaker receives the SiteWise data, processes it, and updates the digital twin model.
- Visualization: Grafana retrieves data from TwinMaker and presents it on various panels for real-time monitoring.
## Visual Representation
The following images show the overall architecture and Grafana panels used in this project:

Architecture Diagram:
![](https://github.com/harshakalluri1403/Motor-Digital-Twin-Using-AWS/blob/54ca9557d3fe7a9693dec2dd068f77f63f7052ab/Screenshot%202024-11-03%20020128.png) 

Grafana Dashboard:
![](https://github.com/harshakalluri1403/Motor-Digital-Twin-Using-AWS/blob/54ca9557d3fe7a9693dec2dd068f77f63f7052ab/Screenshot%202024-11-03%20010927.png) 
![](https://github.com/harshakalluri1403/Motor-Digital-Twin-Using-AWS/blob/54ca9557d3fe7a9693dec2dd068f77f63f7052ab/Screenshot%202024-11-03%20010941.png) 
![](https://github.com/harshakalluri1403/Motor-Digital-Twin-Using-AWS/blob/54ca9557d3fe7a9693dec2dd068f77f63f7052ab/Screenshot%202024-11-03%20010959.png) 

## Setup Instructions
1. Create Assets in AWS IoT SiteWise:
   - Define the motor as an asset in AWS IoT SiteWise.
   - Configure asset properties to capture the speed of the motor.
2. Configure AWS IoT TwinMaker:
   - Set up TwinMaker workspace and resources.
   - Link the SiteWise asset to TwinMaker to enable real-time data integration.
3. Visualize in Grafana:
   - Connect Grafana to AWS IoT TwinMaker.
   - Create dashboards and panels to display motor speed and other relevant data.

## Key Features
- Real-Time Monitoring: Track the motor's speed in real time.
- Digital Twin Modeling: Provides a virtual representation of the motor using AWS IoT TwinMaker.
- Customizable Dashboards: Grafana panels can be customized to include additional metrics or different visualization types.
## Future Enhancements
- Predictive Maintenance: Use machine learning to predict motor failures based on speed fluctuations.
- Additional Metrics: Include other motor parameters, like temperature or vibration, for a comprehensive view.
- Alerting System: Integrate alerts in Grafana to notify users of abnormal motor behavior.
