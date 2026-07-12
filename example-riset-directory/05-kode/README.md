# 05-kode

Penelitian ini berfokus pada domain Human-Computer Interaction (HCI) dengan menggunakan metode Between-Subjects A/B Testing pada sisi antarmuka (frontend). Oleh karena itu, arsitektur backend seperti API Gateway dan pengujian ketahanan server menggunakan k6 tidak relevan. Sebagai gantinya, Tahap 2 dan Tahap 3 diadaptasi menjadi implementasi instrumen purwarupa interaktif dan skrip analitik data pengujian hipotesis.

Tahap 2: Implementasi Instrumen (Pengganti API Gateway)
Sistem direpresentasikan dalam bentuk High-Fidelity Prototype yang memuat skenario tugas simulasi e-commerce (A/B Routing) untuk diobservasi oleh partisipan.

Tautan Purwarupa (Figma): https://www.figma.com/design/BERX4d1E8MyYA2Y6sLjpB6/helloPet?node-id=435-510&t=zjnzdos0mnJRcUrA-1

Tahap 3: Skrip Pengujian Analitik (Pengganti Skrip k6)
Sebagai pengganti skrip stress test (k6) yang menguji server mesin, penelitian ini menggunakan skrip Python (Pandas & SciPy) untuk menguji signifikansi (ketahanan hipotesis) dari interaksi manusia. Skrip ini mengeksekusi Mann-Whitney U Test secara otomatis untuk memvalidasi efek Dark Pattern terhadap Usability dan Trust.

Python
# Snippet Skrip Pengujian Hipotesis (Dieksekusi via Google Colab)
import pandas as pd
from scipy import stats

# Memuat data hasil pengujian purwarupa Figma & Google Forms
df = pd.read_csv('data_mentah.csv')
grup_kontrol = df[df['Kelompok'] == 'KONTROL']
grup_dark_pattern = df[df['Kelompok'] == 'DARK PATTERN']

# Eksekusi Uji Signifikansi (Alpha 0.05)
stat_sus, p_sus = stats.mannwhitneyu(grup_kontrol['Total SUS'], grup_dark_pattern['Total SUS'])
stat_trust, p_trust = stats.mannwhitneyu(grup_kontrol['Rata2 Trust'], grup_dark_pattern['Rata2 Trust'])

print(f"P-Value Usability : {p_sus:.5f}")
print(f"P-Value Trust     : {p_trust:.5f}")
