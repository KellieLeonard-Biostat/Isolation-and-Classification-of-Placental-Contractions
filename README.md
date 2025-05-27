# Isolation and Classification of Placental Contractions from Composite Uterine Signals Using Signal Processing and Random Forest

**Abstract**
Accurate identification of placental contractions (Type A) from uterine activity signals is critical for monitoring fetal well-being during pregnancy. The raw abdominal recordings often contain mixed signals from placental contractions, fetal kicks (Type B), maternal movements (Type C), and noise. This study proposes a signal processing pipeline to isolate Type A contractions from composite signals by applying detrending, bandpass filtering, smoothing, normalization, segmentation, and feature extraction. A Random Forest classifier trained on these features achieved perfect precision, recall, and F1-score on the test set, demonstrating effective classification capability. This approach provides a promising tool for non-invasive fetal monitoring.

**1. Introduction**
Monitoring uterine contractions is essential in prenatal care to assess fetal health and detect complications. Placental contractions (Type A) indicate uterine activity related to placental blood flow, while fetal kicks (Type B) and maternal movements (Type C) introduce artifacts that complicate signal interpretation. Accurately isolating Type A contractions from noisy abdominal recordings remains challenging.

Previous approaches often use simple filtering or manual annotation, which may lack robustness. This study presents an automated preprocessing and classification pipeline combining classical signal processing methods with machine learning to isolate and classify placental contractions in synthetic composite signals.

**2. Materials and Methods**

**2.1 Data Generation**
Synthetic signals simulating three contraction types and noise were generated over an 8-hour recording at 20 Hz sampling frequency.

Type A (Placental contractions): Modeled as low-frequency sinusoidal bursts (0.05–0.1 Hz) modulated by a Hanning window to mimic real contraction shapes.

Type B (Fetal kicks): Short bursts of higher-frequency signals (0.8–2.0 Hz) with durations of 0.5–2 seconds.

Type C (Maternal movements): Slow sinusoidal drifts at ultra-low frequencies (0.005–0.01 Hz) representing baseline shifts.

Noise: Gaussian white noise simulating measurement variability.

The combined raw signal included all components to replicate physiological recording complexity.

**2.2 Preprocessing Pipeline**
The raw signal was processed in the following sequence:

Detrending: Baseline drift removed using a Savitzky-Golay filter (window size=1001, polynomial order=3).

Bandpass Filtering: A 4th order Butterworth filter retained frequencies between 0.05 and 0.5 Hz to isolate placental contraction band.

Smoothing: Savitzky-Golay smoothing (window=301, order=2) was applied to reduce residual noise.

Normalization: Signal amplitude normalized for consistency across segments.

Segmentation: Signal divided into contraction candidate windows based on amplitude thresholds and timing criteria.

Feature Extraction: Extracted time-domain and frequency-domain features including peak amplitude, duration, power spectral density metrics.

![image](https://github.com/user-attachments/assets/cfa62405-7f63-4bcf-aec0-9263267757b4)


**2.3 Classification**
A Random Forest classifier was trained on the extracted features to classify contraction windows as Type A (placental) or non-Type A (fetal kicks, maternal movement, noise). The model was evaluated using precision, recall, F1-score, and accuracy metrics.

**3. Results**
The RF classifier achieved the following metrics on a test set of 96 segments:

Class	Precision	Recall	F1-Score	Support
0 (non-Type A)	1.00	1.00	1.00	88
1 (Type A)	1.00	1.00	1.00	8

Overall Accuracy: 100%
Macro Average: Precision = Recall = F1 = 1.00
Weighted Average: Precision = Recall = F1 = 1.00

These results demonstrate perfect classification performance on this synthetic dataset.

**4. Discussion**
The preprocessing pipeline successfully isolated the placental contraction frequency band, removing confounding fetal kicks and maternal movements. The extracted features were highly discriminative, enabling the Random Forest model to classify contractions with perfect accuracy. Although the synthetic dataset provides controlled conditions, results are promising for real-world applications.

Limitations include reliance on simulated data; future work will focus on validating the method with clinical uterine recordings and investigating robustness to inter-subject variability and noise. Additionally, integration with deep learning models could further improve classification.

**5. Conclusion**
This study presents a robust signal processing and machine learning approach to isolate and classify placental contractions from composite uterine signals. The method achieved perfect classification on synthetic data, indicating potential for enhancing non-invasive fetal monitoring technologies.



