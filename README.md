# VTA Mini-Challenge 2: Fouriertransformation

Herbstsemester 2025 - FHNW Data Science

## Überblick

Dieses Repository enthält die Lösungen für die Mini-Challenge 2 im Modul "Vertiefende Themen der Analysis". Die Challenge besteht aus vier Aufgaben zur Fouriertransformation mit praktischen Anwendungen in der Signalverarbeitung.

## Aufgaben

### Aufgabe 1: Eigene DFT-Implementierung (40%)

Implementierung einer eigenen diskreten Fouriertransformation mit zwei Methoden:

1. **Reihenapproximation**: Verwendung der Euler-Formel 
   - $e^{ix} = \cos(x) + i\sin(x)$
   
2. **Numerische Integration**: Berechnung der Fourierkoeffizienten
   - $a_k = \frac{2}{T} \int_0^T f(t) \cos(k \cdot \frac{2\pi}{T} \cdot t) \, dt$
   - $b_k = \frac{2}{T} \int_0^T f(t) \sin(k \cdot \frac{2\pi}{T} \cdot t) \, dt$

**Testsignal**: $s(t) = 2 + 5\sin(t) + 3\cos(3t)$ im Intervall $[0, 2\pi]$ mit 64 Messwerten

**Vergleich**: Beide Implementierungen werden mit `numpy.fft` verglichen (Korrektheit und Performance)

**Datei**: `aufgabe1_fourier.py`

---

### Aufgabe 2: Tram-Vibrationsanalyse (20%)

Analyse von Tramvorbeifahrten zur Qualitätskontrolle der Gleisisolation.

**Aufgabenstellung**:
- Darstellung des Vibrationssignals (z-Richtung, lotrecht zum Gleis)
- Berechnung des Amplitudenspektrums zwischen 4 Hz und 400 Hz
- Schätzung des Schwellenabstands aus:
  - Fahrgeschwindigkeit: 50 km/h
  - Dominanten Frequenzen im Spektrum
  - Formel: $d = \frac{v}{f}$

**Daten**: 
- Datei: `tramdaten_fourier_vta_mc2_hs25.csv`
- 60'075 Datenpunkte über 10 Sekunden
- Vibrationsgeschwindigkeiten in mm/s

**Datei**: `aufgabe2_tramvibrationen.py`

---

### Aufgabe 3: 2D-Fouriertransformation (20%)

Visualisierung des Amplitudenspektrums von drei 2D-Funktionen:

1. **Quadrat**: 
   $$f(x,y) = \begin{cases} 1 & |x| \leq 1 \land |y| \leq 1 \\ 0 & \text{sonst} \end{cases}$$

2. **Kreis**: 
   $$f(x,y) = \begin{cases} 1 & \sqrt{x^2 + y^2} \leq 1 \\ 0 & \text{sonst} \end{cases}$$

3. **2D-Gauß**: 
   $$f(x,y) = \frac{1}{2\pi} e^{-\frac{\sqrt{x^2 + y^2}}{2}}$$

**Parameter**: Bereich $[-2, 2] \times [-2, 2]$ mit $64 \times 64$ Datenpunkten

**Datei**: `aufgabe3_2d_fourier.py`

---

### Aufgabe 4: Bildfilterung (20%)

Fourier-basierte Bildfilterung mit Tiefpass- und Hochpassfiltern.

**Methodik**:
1. 2D-Fouriertransformation des Bildes
2. Anwendung von Filtern im Frequenzraum:
   - **Tiefpassfilter**: Entfernt hohe Frequenzen (Glättung/Weichzeichnung)
   - **Hochpassfilter**: Entfernt niedrige Frequenzen (Kantendetektion)
3. Inverse Fouriertransformation für rekonstruiertes Bild

**Eingabe**: `img_a2_mc2_vta_hs25.bmp`

**Datei**: `aufgabe4_bildfilterung.py`

---

## Installation

### Voraussetzungen
```bash
pip install numpy scipy matplotlib pandas pillow
```

### Verwendete Bibliotheken

- `numpy`: Numerische Berechnungen und FFT
- `scipy`: Wissenschaftliche Funktionen (FFT, Integration)
- `matplotlib`: Visualisierung
- `pandas`: Datenverarbeitung (CSV)
- `pillow`: Bildverarbeitung

---

## Verwendung

### Aufgabe 1: DFT-Implementierung
```python
python aufgabe1_fourier.py
```

**Ausgabe**:
- Konsolen-Output mit gefundenen Frequenzkomponenten
- Performance-Vergleich
- Zwei Plots: Performance-Vergleich und Amplitudenspektren

---

### Aufgabe 2: Tram-Vibrationen

**Wichtig**: Passe den Dateipfad in Zeile 12 an:
```python
datei = r'DEIN_PFAD\tramdaten_fourier_vta_mc2_hs25.csv'
```
```python
python aufgabe2_tramvibrationen.py
```

**Ausgabe**:
- Datenübersicht und dominante Frequenzen
- Geschätzter Schwellenabstand
- Zwei Plots: Vibrationssignal und Amplitudenspektrum (4-400 Hz)

---

### Aufgabe 3: 2D-Fouriertransformation
```python
python aufgabe3_2d_fourier.py
```

**Ausgabe**:
- Plot mit 3×3 Grid:
  - Spalte 1: Originalfunktionen
  - Spalte 2: Amplitudenspektren
  - Spalte 3: Log-Amplitudenspektren

---

### Aufgabe 4: Bildfilterung

**Wichtig**: Bild muss im selben Verzeichnis liegen oder Pfad anpassen (Zeile 16)
```python
python aufgabe4_bildfilterung.py
```

**Ausgabe**:
- Zwei Plots:
  - 3×3 Grid: Original, FFT, Filter-Ergebnisse
  - 1×3 Vergleich: Original, Tiefpass, Hochpass

---

## Ergebnisse

### Aufgabe 1: DFT-Implementierung

✅ **Korrektheit**: Beide Methoden finden alle Frequenzkomponenten korrekt
- DC (f=0): 2.0
- f=1: 5.0
- f=3: 3.0

📊 **Performance** (relativ zu NumPy FFT):
- Reihenapproximation: ~600-700× langsamer
- Numerische Integration: ~40-50× langsamer
- NumPy FFT: Referenz (optimierte C-Implementierung)

---

### Aufgabe 2: Tram-Vibrationen

📍 **Dominante Frequenzen**:
- f₁ = 16.00 Hz → Schwellenabstand ≈ **87 cm**
- f₂ = 71.20 Hz → Schwellenabstand ≈ 20 cm (Harmonische)

✅ **Interpretation**: Der geschätzte Schwellenabstand von ~87 cm liegt im typischen Bereich für Tramgleise (60-80 cm)

---

### Aufgabe 3: 2D-Fouriertransformation

🔍 **Beobachtungen**:

1. **Quadrat**: 
   - Scharfe Kanten → viele hohe Frequenzen
   - Sinc-Funktion Muster im Frequenzraum
   
2. **Kreis**: 
   - Rotationssymmetrisches Spektrum
   - Airy-Disk Muster (Bessel-Funktion)
   
3. **2D-Gauß**: 
   - Glatte Funktion → konzentriert bei niedrigen Frequenzen
   - Gauß bleibt Gauß unter Fouriertransformation

---

### Aufgabe 4: Bildfilterung

🎯 **Filter-Effekte**:

- **Tiefpassfilter**: 
  - Entfernt Details und Rauschen
  - Weichzeichnung/Glättung
  
- **Hochpassfilter**: 
  - Hebt Kanten und Details hervor
  - Kantendetektion

---

## Projektstruktur
```
.
├── aufgabe1_fourier.py              # Eigene DFT-Implementierung
├── aufgabe2_tramvibrationen.py      # Tram-Vibrationsanalyse
├── aufgabe3_2d_fourier.py           # 2D-Fouriertransformation
├── aufgabe4_bildfilterung.py        # Bildfilterung
├── tramdaten_fourier_vta_mc2_hs25.csv  # Vibrationsdaten
├── img_a2_mc2_vta_hs25.bmp          # Testbild
└── README.md                         # Diese Datei
```

---

## Technische Details

### Implementierte Konzepte

- Diskrete Fouriertransformation (DFT)
- Euler-Formel: $e^{-ix} = \cos(x) - i\sin(x)$
- Numerische Integration (Trapezregel)
- 2D-FFT für Bilder
- Frequenzbereichsfilterung
- Signalanalyse und -verarbeitung

### Performance-Optimierung

Die eigenen Implementierungen sind für **Lernzwecke** optimiert (Verständnis der Mathematik), während NumPy FFT den **Fast Fourier Transform (FFT)** Algorithmus nutzt:
- Komplexität DFT: O(N²)
- Komplexität FFT: O(N log N)

---

## Autor

Studentin: Mila Brutenic, Data Science & AI, FHNW  
Modul: Vertiefende Themen der Analysis (VTA)  
Semester: Herbstsemester 2025  
Dozent: Roger Burkhardt

---

## Lizenz

Dieses Projekt wurde für akademische Zwecke erstellt.
