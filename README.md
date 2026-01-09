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





## Sätze für Bericht - chatty
Sensor data from the smartphone are provided in individual CSV files and are imported separately to allow individual preprocessing and synchronization later.

All sensor timestamps are normalized to seconds and shifted to a common start time in order to ensure consistent time handling and comparability between sensors.

The sampling frequency of the accelerometer is estimated from the mean time difference between consecutive measurements and defines how many sensor samples are recorded per second. It is required for the correct design of digital filters and for converting time-based parameters, such as minimum step duration, into sample-based values, ensuring that walking-related signals are processed correctly.


The total acceleration magnitude is computed to obtain an orientation-independent signal that clearly reflects the human gait cycle.

To prepare the accelerometer data for step detection, the total acceleration magnitude is first computed from the x, y, and z axes. This produces an orientation-independent signal that captures the overall motion of the pedestrian. A band-pass filter with cut-off frequencies of 0.7 Hz and 3 Hz is then applied to isolate walking-related acceleration, removing the effects of gravity and high-frequency sensor noise. Finally, the filtered signal is smoothed using a Savitzky–Golay filter with a window length of 0.5 seconds, which reduces residual noise while preserving the shape of the step peaks for accurate detection.

Steps are detected by identifying peaks in the smoothed total acceleration signal. A simple threshold is set as the mean acceleration plus 0.5 m/s², so only peaks corresponding to actual foot strikes are counted. Additionally, a minimum distance of 0.4 seconds between peaks is enforced to match typical human walking cadence. The detected peaks are converted to step times, and the intervals between consecutive steps are calculated. A visualization of the smoothed signal with detected peaks and threshold is provided to verify step detection.

To detect stair steps, we use barometer-derived relative height interpolated to the timestamps of detected steps. A vertical displacement threshold of 0.06 m per step was chosen to reliably identify stairs while accounting for sensor noise and indoor pressure variations; higher thresholds (e.g., 0.12 m) failed to detect any stairs. To avoid false positives from isolated spikes, only sequences of two or more consecutive steps exceeding this threshold are considered stair segments. Detected stair steps are assigned a reduced step length of 0.3 m compared to 0.8 m for flat walking, reflecting the smaller horizontal displacement during stair climbing or descending. This approach ensures realistic step length correction and accurate vertical movement representation in the PDR trajectory.


- Possible Errors:
-- Heading biases and noise
-- Constant step length model
-- Misalignment between step times and heading / height
-- Barometer‑based stair detection imperfections
-- Magnetic disturbances and environment
-- No loop‑closure or external corrections
-- What you can realistically say in the report



## Ideen für Bericht

Visualisierung: 
- Barometer
- Step detection (Acc) -> maybe nur Ausschnitt?