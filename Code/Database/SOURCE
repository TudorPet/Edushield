PRAGMA foreign_keys = ON;


--  TABLES


CREATE TABLE School (
    school_id INTEGER PRIMARY KEY,
    name TEXT,
    city TEXT
);

CREATE TABLE Zone (
    zone_id INTEGER PRIMARY KEY,
    zone_name TEXT,
    school_id INTEGER,
    FOREIGN KEY (school_id) REFERENCES School(school_id)
);

CREATE TABLE User (
    user_id INTEGER PRIMARY KEY,
    name TEXT,
    role TEXT,
    has_training BOOLEAN
);

CREATE TABLE Attack_Type (
    attack_type_id INTEGER PRIMARY KEY,
    name TEXT,
    description TEXT
);

CREATE TABLE Incident (
    incident_id INTEGER PRIMARY KEY,
    incident_date DATE,
    severity TEXT,
    impact TEXT,
    school_id INTEGER,
    zone_id INTEGER,
    attack_type_id INTEGER,
    FOREIGN KEY (school_id) REFERENCES School(school_id),
    FOREIGN KEY (zone_id) REFERENCES Zone(zone_id),
    FOREIGN KEY (attack_type_id) REFERENCES Attack_Type(attack_type_id)
);

CREATE TABLE Incident_User (
    incident_id INTEGER,
    user_id INTEGER,
    PRIMARY KEY (incident_id, user_id),
    FOREIGN KEY (incident_id) REFERENCES Incident(incident_id),
    FOREIGN KEY (user_id) REFERENCES User(user_id)
);

CREATE TABLE Detection_Method (
    method_id INTEGER PRIMARY KEY,
    method_name TEXT
);

CREATE TABLE Incident_Detection (
    incident_id INTEGER,
    method_id INTEGER,
    PRIMARY KEY (incident_id, method_id),
    FOREIGN KEY (incident_id) REFERENCES Incident(incident_id),
    FOREIGN KEY (method_id) REFERENCES Detection_Method(method_id)
);

CREATE TABLE Prevention_Measure (
    measure_id INTEGER PRIMARY KEY,
    measure_name TEXT,
    type TEXT
);

CREATE TABLE Incident_Prevention (
    incident_id INTEGER,
    measure_id INTEGER,
    PRIMARY KEY (incident_id, measure_id),
    FOREIGN KEY (incident_id) REFERENCES Incident(incident_id),
    FOREIGN KEY (measure_id) REFERENCES Prevention_Measure(measure_id)
);

CREATE TABLE Incident_Response_Time (
    response_id INTEGER PRIMARY KEY,
    incident_id INTEGER UNIQUE,
    reported_time DATETIME,
    resolved_time DATETIME,
    FOREIGN KEY (incident_id) REFERENCES Incident(incident_id)
);

CREATE TABLE Training_Session (
    training_id INTEGER PRIMARY KEY,
    training_type TEXT,
    training_date DATE,
    target_role TEXT
);

CREATE TABLE Incident_Recommendation (
    recommendation_id INTEGER PRIMARY KEY,
    incident_id INTEGER,
    recommendation_text TEXT,
    priority_level TEXT,
    FOREIGN KEY (incident_id) REFERENCES Incident(incident_id)
);


--  INDEXES 


CREATE INDEX idx_incident_school ON Incident(school_id);
CREATE INDEX idx_incident_severity ON Incident(severity);
CREATE INDEX idx_incident_date ON Incident(incident_date);
CREATE INDEX idx_incident_attack ON Incident(attack_type_id);

CREATE INDEX idx_incident_user_incident ON Incident_User(incident_id);
CREATE INDEX idx_incident_user_user ON Incident_User(user_id);

CREATE INDEX idx_incident_detection_incident ON Incident_Detection(incident_id);
CREATE INDEX idx_incident_prevention_incident ON Incident_Prevention(incident_id);


--  VIEWS (reports)


CREATE VIEW vw_incidents_per_school AS
SELECT
    s.school_id,
    s.name AS school_name,
    COUNT(i.incident_id) AS total_incidents
FROM School s
LEFT JOIN Incident i ON s.school_id = i.school_id
GROUP BY s.school_id, s.name;

CREATE VIEW vw_incidents_by_severity AS
SELECT
    severity,
    COUNT(*) AS total_incidents
FROM Incident
GROUP BY severity;

CREATE VIEW vw_attack_type_statistics AS
SELECT
    a.name AS attack_type,
    COUNT(i.incident_id) AS occurrences
FROM Attack_Type a
LEFT JOIN Incident i ON a.attack_type_id = i.attack_type_id
GROUP BY a.name;

CREATE VIEW vw_avg_response_time AS
SELECT
    i.incident_id,
    AVG(
        (julianday(r.resolved_time) - julianday(r.reported_time)) * 24 * 60
    ) AS avg_response_minutes
FROM Incident i
JOIN Incident_Response_Time r ON i.incident_id = r.incident_id
GROUP BY i.incident_id;


--  SAMPLE DATA


-- Schools
INSERT INTO School (school_id, name, city) VALUES
(1, 'Central High School', 'Bucharest'),
(2, 'Westside School', 'Cluj'),
(3, 'North Academy', 'Iasi');

-- Zones
INSERT INTO Zone (zone_id, zone_name, school_id) VALUES
(1, 'Computer Lab', 1),
(2, 'Administration Office', 1),
(3, 'Science Lab', 2),
(4, 'Library', 3);

-- Users
INSERT INTO User (user_id, name, role, has_training) VALUES
(1, 'Alice', 'Student', 0),
(2, 'Bob', 'IT Staff', 1),
(3, 'Carol', 'Teacher', 1),
(4, 'David', 'Student', 0);

-- Attack Types
INSERT INTO Attack_Type (attack_type_id, name, description) VALUES
(1, 'Phishing', 'Credential stealing emails'),
(2, 'Malware', 'Malicious software infection'),
(3, 'Ransomware', 'Encrypts files for ransom');

-- Detection Methods
INSERT INTO Detection_Method (method_id, method_name) VALUES
(1, 'Antivirus'),
(2, 'Firewall Logs'),
(3, 'Manual Report');

-- Prevention Measures
INSERT INTO Prevention_Measure (measure_id, measure_name, type) VALUES
(1, 'User Training', 'Administrative'),
(2, 'Firewall', 'Technical'),
(3, 'Regular Backups', 'Technical');

-- Incidents
INSERT INTO Incident (incident_id, incident_date, severity, impact, school_id, zone_id, attack_type_id) VALUES
(1, '2026-01-10', 'High', 'Severe', 1, 1, 1),
(2, '2026-01-11', 'Medium', 'Moderate', 1, 2, 2),
(3, '2026-01-12', 'Low', 'Minor', 2, 3, 3),
(4, '2026-01-13', 'High', 'Severe', 3, 4, 1);

-- Incident  Users
INSERT INTO Incident_User (incident_id, user_id) VALUES
(1, 1),
(1, 2),
(2, 2),
(2, 3),
(3, 3),
(4, 4);

-- Incident  Detection
INSERT INTO Incident_Detection (incident_id, method_id) VALUES
(1, 1),
(2, 2),
(3, 3),
(4, 1);

-- Incident Prevention
INSERT INTO Incident_Prevention (incident_id, measure_id) VALUES
(1, 1),
(1, 2),
(2, 2),
(3, 3),
(4, 1);

-- Incident Response Times
INSERT INTO Incident_Response_Time (response_id, incident_id, reported_time, resolved_time) VALUES
(1, 1, '2026-01-10 09:00:00', '2026-01-10 11:00:00'),
(2, 2, '2026-01-11 10:30:00', '2026-01-11 13:00:00'),
(3, 3, '2026-01-12 08:00:00', '2026-01-12 09:00:00'),
(4, 4, '2026-01-13 07:45:00', '2026-01-13 10:15:00');

-- Incident Recommendations
INSERT INTO Incident_Recommendation (recommendation_id, incident_id, recommendation_text, priority_level) VALUES
(1, 1, 'Increase phishing awareness training', 'High'),
(2, 2, 'Update antivirus definitions', 'Medium'),
(3, 3, 'Backup files regularly', 'Low'),
(4, 4, 'Monitor high-risk zones more frequently', 'High');
