### Core Entities
- **School** – Represents educational institutions
- **Zone** – Logical or physical areas within a school (e.g. laboratory, administration, staff areas)
- **Incident** – Reported cybersecurity events
- **Attack_Type** – Classification of cyber attacks
- **User** – Individuals involved in incidents (students, staff, administrators)
- **Incident_User** – Association between incidents and involved users
- **Incident_Detection** – Detection event details
- **Detection_Method** – Methods used to detect incidents
- **Incident_Prevention** – Preventive actions linked to incidents
- **Prevention_Measure** – Defined preventive measures
- **Training_Session** – Cybersecurity training activities
- **Recommendation** – Preventive recommendations generated after incidents


### Indexes and Views

To ensure high performance and scalability, especially when handling millions of records, critical columns such as school_id, incident_date, and zone_id are indexed. These indexes significantly speed up searches, filtering, and join operations, allowing queries to return results almost instantly even on large datasets.

Additionally, several views have been created to provide ready-to-use reports without running complex queries every time. Examples include:

## vw_incidents_per_school – shows the total number of incidents per school

## vw_avg_response_time – calculates the average response time per attack type

## vw_users_in_incidents – lists all users involved in incidents

## vw_high_risk_zones – highlights zones with the highest number of incidents

These views simplify data access for administrators and management, enable fast reporting, and ensure that frequently used queries are pre-optimized, making the system highly efficient and user-friendly.

