# Navi_Lab02_WS25

## Sensoren kurze Erklärung 

Accelerometer (Beschleunigungssensor)
Misst:
Lineare Beschleunigung in X, Y, Z
Einheit: m/s²
Nutzung in PDR:
Schritterkennung (Peaks beim Gehen)
Schrittlänge schätzen
Erkennen von Stillstand / Bewegung
Neigung (g-Vektor)

Gyroscope (Drehratensensor)
Misst:
Winkelgeschwindigkeit um X, Y, Z
Einheit: °/s oder rad/s
Nutzung in PDR:
Erkennen von Drehungen
Kurzfristig sehr genaue Orientierungsänderung
Glättung der Bewegungsrichtung

Magnetometer (Magnetfeldsensor)
Misst:
Magnetfeldstärke X, Y, Z
Einheit: µT
Nutzung in PDR:
Absolute Richtung (Heading / Yaw)
Korrektur des Gyroskop-Drifts

Barometer (Drucksensor)
Misst:
Luftdruck
Einheit: hPa
Nutzung in PDR:
Höhenänderung
Erkennen von:
Treppen
Aufzug
Stockwerkswechsel

Reference Orientation
Was ist das?
Keine Rohsensorik
Ergebnis von Sensorfusion aus:
Accelerometer
Gyroskop

Magnetometer
Nutzung in PDR:
Liefert stabile Roll, Pitch, Yaw
Definiert:
„vorwärts“
„links“
„oben“
Basis für Bewegungsrichtung

Ground Truth
Was ist das?
Referenzdaten, keine Sensoren
„Die wahre Position / Bewegung“
Nutzung in PDR:
Evaluation & Training
Fehlerberechnung:
Positionsfehler
Drift
Schrittfehler

➡️ Nur zum Vergleichen, nicht zum Rechnen

Zusammenspiel in PDR
Sensor	Rolle
Accelerometer	Schritte & Bewegung
Gyroskop	Drehungen
Magnetometer	Absolute Richtung
Barometer	Höhe / Stockwerke
Reference Orientation	Stabile Ausrichtung
Ground Truth	Bewertung

Typischer PDR-Ablauf

Schritte erkennen (Accelerometer)
Schrittlänge schätzen
Richtung bestimmen (Gyro + Magnetometer → Orientation)
Position aktualisieren
Höhe anpassen (Barometer)
Mit Ground Truth vergleichen

Merksätze:

The fourth root is used because the relationship between acceleration amplitude and step length is highly nonlinear and the fourth-root model was empirically shown to best approximate human walking dynamics.

A constant step length is simple but unrealistic,
whereas the Weinberg model adapts the step length
to the walking dynamics and therefore reduces drift.

The scaling factor k of the Weinberg model was calibrated using the known ground‑truth distance.
This ensures that the estimated step lengths are consistent with the actual walked distance.