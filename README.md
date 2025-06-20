# Transisi Energi Hijau 2025 di Indonesia

Nama : Farhan Fadillah

Batch : 9

No.Absen : 9.008.DB2025

Indonesia mengejar target ambisius: 23% energi terbarukan pada 2025 untuk bumi yang lestari! Pemerintah menerapkan pajak karbon untuk kurangi emisi industri, seperti di sektor tekstil Jawa Barat. Tapi, tantangannya besar! Banyak perusahaan melakukan greenwashing, mengklaim ramah lingkungan padahal emisinya tinggi, menyesatkan investor. 

Di Jawa Tengah dan Sulawesi Selatan, proyek PLTS sering memicu konflik lahan dengan petani dan masyarakat adat. Data Kementerian ESDM menunjukkan kita baru mencapai 12% energi terbarukan pada 2023, jauh dari target. Kita butuh solusi cerdas! Pakai Python, kita akan hitung pajak karbon, deteksi greenwashing, dan analisis risiko konflik lahan. Proyek ini bukan sekadar coding, tapi menghasilkan usulan nyata untuk pemerintah agar investasi energi hijau lancar dan konflik minim.

Poin Utama:
- Target 23% energi terbarukan 2025, baru 12% tercapai.
- Pajak karbon dorong pengurangan emisi industri.
- Greenwashing menipu publik, perlu verifikasi emisi.
- Konflik lahan PLTS berdampak sosial, butuh evaluasi.
- Python bantu usulkan solusi keberlanjutan ke pemerintah.

# PROBLEM ISSUE

Transisi energi hijau 2025 di Indonesia menghadapi tiga masalah utama. Pertama, data emisi perusahaan sering tidak akurat, menyulitkan penerapan pajak karbon, terutama di industri tekstil Jawa Barat. Kedua, greenwashing merajalela. Banyak perusahaan mengklaim hijau, tapi emisinya melebihi batas. 

KLHK melaporkan 25% klaim hijau tidak terverifikasi. Ketiga, konflik lahan menghambat proyek PLTS. Di Jawa Tengah, lahan sawah petani diambil untuk PLTS, memicu 800 konflik lahan pada 2023, menurut WALHI. Ini menghalangi investasi energi hijau dan merugikan komunitas lokal. Tanpa analisis data yang solid, pemerintah kesulitan membuat kebijakan efektif. Kita akan pakai Python untuk menghitung pajak karbon, mendeteksi greenwashing, dan mengevaluasi risiko lahan. Solusi ini membantu capai Net Zero Emission 2060 dan mengurangi konflik sosial. 

Poin Utama:
- Data emisi tidak akurat hambat pajak karbon.
- Greenwashing (25% klaim tak valid) menyesatkan publik.
- Konflik lahan (800 kasus 2023) ganggu proyek PLTS.
- Analisis Python dukung kebijakan energi hijau.
- Solusi bantu capai Net Zero Emission 2060.

# APA TUJUAN KITA?

Membangun alat analisis data dengan Python untuk transisi energi hijau 2025! Pertama, kita menghitung pajak karbon agar perusahaan mematuhi regulasi, seperti di sektor industri Jawa Barat. Kedua, kita mendeteksi greenwashing, memverifikasi klaim hijau perusahaan agar publik tidak tertipu. Ketiga, kita menganalisis konflik lahan di proyek PLTS untuk meminimalkan dampak sosial, terutama di Jawa Tengah. Menggunakan data CSV realistis (30 baris, 5 kolom), kita mulai dari logika sederhana (if-else) hingga modul canggih, menghasilkan program rapi.

Tujuannya? Memberikan usulan konkret ke pemerintah, seperti verifikasi emisi wajib dan mediasi lahan. Portofolio ini akan menunjukkan kemampuan kita menyelesaikan masalah nyata, mendukung target 23% energi terbarukan 2025 dan Net Zero Emission 2060.

Poin Utama:
- Hitung pajak karbon untuk kepatuhan regulasi.
- Deteksi greenwashing berdasarkan data emisi.
- Analisis risiko lahan untuk kurangi konflik sosial.
- Gunakan Python dari if-else hingga modul.
- Hasilkan portofolio dengan usulan ke pemerintah.

Sebagai catatan, kita akan implementasi hasil logic program ke dataframe untuk keperluan Audit Reporting jika di butuhkan report outputnya

# Import Modul yang dibutuhkan

Pada Bagian ini kita akan terlebih dahulu import modul yang dibutuhkan untuk membangun projek kita, yaitu:
- Pandas
- Matplotlib
- Numpy


```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

emisi_df = pd.read_csv("emisi_perusahaan.csv")
konflik_lahan = pd.read_csv("konflik_lahan.csv")
tren_df = pd.read_csv('tren_emisi.csv')
```

# BAGIAN 1 : CEK KEPATUHAN PAJAK KARBON

#### Tujuan : Mengecek apakah emisi perusahaan dari CSV melebihi dari batas pajak karbon (CO2) dan melihat distribusi perusahaan yang kena pajak karbon dan bebas pajak karbon

#### Konsep : If-else, Pandas untuk baca data CSV serta menggunakan modul matplotlib untuk pembuatan chart analisa

### Output : List Perusahaan serta status kepatuhannya dan analisa chart kepatuhan pajak karbon


```python
# 1. Fungsi Cek Kepatuhan Emisi
def cek_kepatuhan_pajak(emisi_df, batas_emisi=50):
    results = []
    for _, row in emisi_df.iterrows():
        status = "Bebas Pajak Karbon" if row['Emisi_2024'] <= batas_emisi else "Kena Pajak Karbon"
        results.append({
            'Nama_Perusahaan': row['Nama_Perusahaan'],
            'Emisi_2024': row['Emisi_2024'],
            'Status_Kepatuhan': status
        })
    return pd.DataFrame(results)

hasil_df = cek_kepatuhan_pajak(emisi_df)

## Save to file excel bila perlu
## hasil_df.to_excel("Emision_rule_report_and_action.xlsx")

## Pie Chart Distribusi Kepatuhan Pajak Karbon
status_counts = hasil_df['Status_Kepatuhan'].value_counts()
colors = ['green', 'red']

plt.figure(figsize=(6, 6))
plt.pie(status_counts, labels=[f"{label} ({count})" for label, count in zip(status_counts.index, status_counts)],
        colors=colors, autopct='%1.1f%%')
plt.title(f"Distribusi Kepatuhan Pajak Karbon (Total: {status_counts.sum()} perusahaan)")
plt.show()
```


    
![image](https://github.com/user-attachments/assets/fc17fb27-eb82-4557-9af6-0f063ca71ea8)

    


## Tampilkan List Data hasil


```python
hasil_df
```



![image](https://github.com/user-attachments/assets/9f98cbc9-bcff-490f-9974-12d870231cb3)




### Kesimpulan 
Dari data diatas kita mengetahui bahwa jumlah perusahaan yang kena pajak karbon sebesar 66,7 % lebih dari setengah dari total perusahaan. Tentu pemerintah tidak bisa diam terkait masalah ini diperlukan ketegasan dari pihak penegak hukum untuk lebih tegas menindak untuk efek jera dengan solusi seperti:
- Kenaikan tarif pajak serta sanksi yang lebih berat
- Peringatan keras kepada perusahaan yang melanggar

# BAGIAN 2 : KALKULATOR PAJAK KARBON & HASIL ANALISA

### TUJUAN : Menghitung pajak karbon berdasarkan kelebihan emisi karbon, penentuan intensitas kelebihan dan analisa intensitas kelebihan karbon dan solusinya

### KONSEP: If-else, Iterasi, dan penggunaan modul matplotlib untuk analisa distribusi dan nominal pajak karbon

### OUTPUT : Informasi Nominal Pajak karbon, status intensitas kelebihan emisi karbon dan chart distribusi status kategori intensitas kelebihan karbon


```python
# 2. Kalkulator Pajak Karbon
def hitung_pajak_karbon(hasil_df, batas_emisi=50, tarif=20000):
    results = []
    for _, row in hasil_df.iterrows():
        kelebihan = max(0, row['Emisi_2024'] - batas_emisi)
        pajak = kelebihan * tarif

        # Penentuan kategori intensitas
        if kelebihan == 0:
            intensitas = "Tidak Berlebih"
            tindakan = "Tidak ada tindakan diperlukan"
        elif kelebihan <= 10:
            intensitas = "Rendah"
            tindakan = "Lakukan audit energi internal dan optimasi proses operasional"
        elif kelebihan <= 30:
            intensitas = "Sedang"
            tindakan = "Audit lingkungan eksternal dan implementasi teknologi rendah karbon"
        else:
            intensitas = "Tinggi"
            tindakan = (
                "Investigasi lingkungan, pengenaan sanksi, dan kewajiban mitigasi emisi"
            )

        results.append({
            'Nama_Perusahaan': row['Nama_Perusahaan'],
            'Emisi_2024': row['Emisi_2024'],
            'Kelebihan_Emisi': kelebihan,
            'Pajak_Karbon': pajak,
            'Intensitas_Emisi_Berlebih': intensitas,
            'Tindakan_Direkomendasikan': tindakan
        })
    return pd.DataFrame(results)

hasil_df_pajak = hitung_pajak_karbon(hasil_df)
hasil_df_pajak.head(5)

## Save to file excel bila perlu
## hasil_df_pajak.to_excel("Carbon_tax_report_and_action.xlsx")

## Pie Chart Distribusi Intensitas Emisi Berlebih
intensity_counts = hasil_df_pajak['Intensitas_Emisi_Berlebih'].value_counts()
colors = ['blue', 'green','yellow','red']

plt.figure(figsize=(6, 6))
plt.pie(intensity_counts, labels=[f"{label} ({count})" for label, count in zip(intensity_counts.index, intensity_counts)],
        colors=colors, autopct='%1.1f%%')
plt.title(f"Distribusi Intensitas Emisi Berlebih (Total: {status_counts.sum()} perusahaan)")
plt.show()
```


    
![image](https://github.com/user-attachments/assets/452c4424-50e5-48ee-a755-32923e31ead0)

    


Tampilkan data hasil perhitungan


```python
hasil_df_pajak
```




![image](https://github.com/user-attachments/assets/ec3333bc-84df-4edf-804a-5fe27b79f001)




### Bar Chart untuk analisa perusahaan yang kena pajak karbon


```python
# Filter hanya perusahaan yang kena pajak
kena_pajak_df = hasil_df_pajak[hasil_df_pajak['Pajak_Karbon'] > 0]

# Urutkan berdasarkan Emisi (terbesar ke terkecil)
kena_pajak_df = kena_pajak_df.sort_values(by='Pajak_Karbon', ascending=False)

plt.figure(figsize=(10,6))
plt.bar(kena_pajak_df['Nama_Perusahaan'], kena_pajak_df['Pajak_Karbon'], color='orange')
plt.xticks(rotation=45)
plt.ylabel('Pajak Karbon (Rp)')
plt.xlabel('Perusahaan')
plt.title('Nominal Pajak Karbon (Hanya Perusahaan yang Kena Pajak)')
plt.tight_layout()
plt.show()

```


    
![image](https://github.com/user-attachments/assets/6581e583-8813-4f91-a7c4-d1d26c0a4c07)

    


### Kesimpulan
Berdasarkan dari data di atas dari 30 Perusahaan hanya 10 perusahaan yang emisinya tidak berlebih (> 50 Ton) untuk perusahaan yang emisi nya lebih dari 50 Ton kita membagi status intensitas kelebihan karbon

Selain itu kita bisa mengetahui nominal pajak karbon untuk perusahaan yang terdapat kelebihan emisi dan memvisualisasikan dalam bentuk chart dengan mengurutkan nominal pajak dari yang terbesar ke terkecil

kita membuat klasifikasi intensitas yang kriterianya sebagai berikut:
- Jika batas karbon tidak melebihi standard maka dikategorikan sebagai "Tak Berlebihan"
- Jika batas karbon berada di rentang > 0 sampai <= 10 maka masuk dalam kategori "Kategori Rendah"
- Jika batas karbon berada di rentang > 10 sampai <= 30 maka masuk dalam kategori "Kategori Sedang"
- Jika batas karbon berada di rentang > 30 maka masuk dalam kategori "Kategori Tinggi"

kenapa di buat klasifikasi intensitas? Karena setiap intensitas kelebihan karbon solusi dan follow up actionnya bisa berbeda dengan detail seperti berikut:
1. Kategori Rendah

Lakukan audit energi internal dan optimasi proses operasional

2. Kategori Sedang

Audit lingkungan eksternal dan implementasi teknologi rendah karbon

3. Kategori Tinggi

Investigasi lingkungan, pengenaan sanksi, dan kewajiban mitigasi emisi

4. Tak Berlebihan

Tidak ada tindakan diperlukan, bisa diberikan insentif atau prioritas dalam program bantuan hijau

# BAGIAN 3 : Deteksi Greenwashing dan Follow Up Suggestion

### Tujuan : Validasi status greenwashing klaim dari perusahaan dan memberikan action suggestion 

### Konsep : If-else, Iterrows dan matplotlib untuk chart analisa

### Output : Status Greenwashing untuk setiap perusahaan


```python
# Fungsi untuk deteksi greenwashing
def deteksi_greenwashing(emisi_df, batas_emisi=50):
    results = []
    for _, row in emisi_df.iterrows():
        is_greenwashing = (row['Klaim_Hijau'] == 'ya') and (row['Emisi_2024'] > batas_emisi)
        status = "Greenwashing" if is_greenwashing else "Valid"
        
        if is_greenwashing:
            saran = "Tindakan: Audit lingkungan wajib, denda administratif, dan publikasi pelanggaran"
        else:
            saran = "Insentif: Keringanan pajak atau prioritas dalam program bantuan hijau"
            
        results.append({
            'Nama_Perusahaan': row['Nama_Perusahaan'],
            'Klaim_Hijau': row['Klaim_Hijau'],
            'Emisi_2024': row['Emisi_2024'],
            'Status_Klaim': status,
            'Saran_Tindakan': saran
        })
    return pd.DataFrame(results)

hasil_df_greenwash = deteksi_greenwashing(emisi_df)
hasil_df_greenwash.head()

## Save to file excel bila perlu
## hasil_df_greenwash.to_excel("Greenwash_report_and_action.xlsx")
```




![image](https://github.com/user-attachments/assets/7f836fae-2260-4661-bf00-44503c924a23)




### Pie Chart untuk distribusi kepatuhan pajak karbon


```python
## Pie Chart Distribusi Kepatuhan Pajak Karbon
greenwash_counts = hasil_df_greenwash['Status_Klaim'].value_counts()
colors = ['green','red']

# Pembentukan plot
plt.figure(figsize=(6, 6))
plt.pie(greenwash_counts, labels=[f"{label} ({count})" for label, count in zip(greenwash_counts.index, greenwash_counts)],
        colors=colors, autopct='%1.1f%%')
plt.title(f"Distribusi Status Klaim Greenwash (Total: {status_counts.sum()} perusahaan)")
plt.show()
```


    
![image](https://github.com/user-attachments/assets/f542df50-5f6d-4588-8470-8836b153fc36)

    


### Kesimpulan
56.7 % Perusahaan terdeteksi Greenwashing, lebih dari setengah total data yang dimana pemerintah perlu melakukan tindakan tegas dengan suggestion:
- Jika terdeteksi Greenwashing, Tindakan: Audit lingkungan wajib, denda administratif, dan publikasi pelanggaran
- Jika tidak terdeteksi Greenwashing, Insentif: Keringanan pajak atau prioritas dalam program bantuan hijau

# BAGIAN 4 : Analisa Konflik Tanah dan Solusinya

### TUJUAN : Identifikasi Status Resiko konflik, analisa chart dan solusinya

### KONSEP : If-else, function, itteration, matplotlib untuk pembuatan chart

### Output: Analisa risiko dan saran pemecahan masalah


```python
# Fungsi untuk analisa konflik tanah
def analisis_konflik_lahan(konflik_lahan, batas_luas=500):
    results = []
    for _, row in konflik_lahan.iterrows():
        risiko = "Rendah"
        if row['Status_Konflik'] == 'ya' or row['Luas_Lahan'] > batas_luas:
            risiko = "Tinggi"
        results.append({
            'Nama_Proyek': row['Nama_Proyek'],
            'Luas_Lahan': row['Luas_Lahan'],
            'Status_Konflik': row['Status_Konflik'],
            'Risiko_Konflik': risiko,
            'Saran': "Mediasi masyarakat" if risiko == "Tinggi" else "Lanjutkan dengan monitoring"
        })
    return pd.DataFrame(results)

hasil_df_lahan = analisis_konflik_lahan(konflik_lahan)
hasil_df_lahan

## Save to file excel bila perlu
## hasil_df_lahan.to_excel("Conflict_risk_report_and_action.xlsx")
```




![image](https://github.com/user-attachments/assets/d67fdc64-53cb-48a0-b952-a1e762765a97)




### Pie Chart analisa distribusi risiko konflik lahan


```python
## Pie Chart Distribusi Konflik Lahan
risiko_counts = hasil_df_lahan['Risiko_Konflik'].value_counts()
colors = ['green','red']

plt.figure(figsize=(6, 6))
plt.pie(risiko_counts, labels=[f"{label} ({count})" for label, count in zip(risiko_counts.index, risiko_counts)],
        colors=colors, autopct='%1.1f%%')
plt.title(f"Distribusi Risiko Konflik Lahan PLTS (Total: {status_counts.sum()} PLTS)")
plt.show()
```


    
![image](https://github.com/user-attachments/assets/957e461a-e03e-4584-a471-4326c62437e6)

    


### Bar Chart untuk analisa luas lahan dengan resiko konflik tinggi


```python
# Bar Chart Luas Lahan PLTS
hasil_df_lahan_1 = hasil_df_lahan[hasil_df_lahan['Risiko_Konflik'] == "Tinggi"]

# Urutkan berdasarkan Emisi (terbesar ke terkecil)
hasil_df_lahan_1 = hasil_df_lahan_1.sort_values(by='Luas_Lahan', ascending=False)

plt.figure(figsize=(10,6))
plt.bar(hasil_df_lahan_1['Nama_Proyek'], hasil_df_lahan_1['Luas_Lahan'], color='orange')
plt.xticks(rotation=45)
plt.ylabel('Luas Lahan')
plt.xlabel('PLTS')
plt.title('Luas Lahan PLTS Dengan Risiko Konflik Tinggi')
plt.tight_layout()
plt.show()
```


    
![image](https://github.com/user-attachments/assets/b3f82e59-8746-4ab7-a048-acbfc4300387)

    


### Kesimpulan

70 % PLTS memiliki risiko konflik tinggi, angka ini sangat riskan mengingat pasti akan ada masalah lebih besar jika hal ini dibiarkan, oleh karena itu kita perlu solusi jika status konflik tinggi maka perlu dilakukan mediasi dengan pihak terkait agar tidak terjadi masalah yang lebih besar, namun jika risiko konflik rendah maka kita hanya perlu monitoring projek dengan pihak-pihak yang terlibat

# BAGIAN 5 : Analisa Emisi Perusahaan Dengan Chart

### Tujuan : Analisa Emisi Perusahaan dengan bar chart dengan analisa secara secara data global dan data filter

### Konsep : Bar Chart dengan modul Matplotlib

### Output : Bar Chart Emisi Perusahaan secara global dan analisa perusahaan dengan emisi Ton > 50 Ton


```python
## Bar Chart Emisi Perusahaan

# Urutkan berdasarkan Emisi (terbesar ke terkecil)
emisi_df = emisi_df.sort_values(by='Emisi_2024', ascending=False)

#Plot
plt.figure(figsize=(10, 6))
plt.bar(emisi_df['Nama_Perusahaan'], emisi_df['Emisi_2024'], color='green')
plt.axhline(y=50, color='red', linestyle='--', label='Batas Emisi 50 ton')
plt.xticks(rotation=45)
plt.ylabel('Emisi (ton CO2)')
plt.title('Emisi Karbon per Perusahaan')
plt.legend()
plt.tight_layout()
plt.show()

```


    
![image](https://github.com/user-attachments/assets/c9ebe16e-b8d0-4fa9-82c6-d4a25fd9ba3b)

    


### Bar Chart Emisi Perusahaan untuk perusahaan dengan Emisi lebih dari 50 Ton


```python
## Bar Chart Emisi Perusahaan (Emisi lebih dari 50 Ton)
# Filter data
emisi_df_1 = emisi_df[emisi_df['Emisi_2024'] > 50]

# Urutkan berdasarkan Emisi (terbesar ke terkecil)
emisi_df_1 = emisi_df_1.sort_values(by='Emisi_2024', ascending=False)

# Hitung jumlah perusahaan
jumlah_perusahaan = len(emisi_df_1)

# Plot
plt.figure(figsize=(10, 6))
plt.bar(emisi_df_1['Nama_Perusahaan'], emisi_df_1['Emisi_2024'], color='red', label='Emisi > 50 ton')
plt.xticks(rotation=45)
plt.ylabel('Emisi (ton CO2)')
plt.title(f'Emisi Karbon per Perusahaan (>{50} Ton) - {jumlah_perusahaan} Perusahaan')
plt.legend()
plt.tight_layout()
plt.show()
```


    
![image](https://github.com/user-attachments/assets/dc79cc3d-3da1-41cb-8053-6aea87369e9b)

    


### Kesimpulan
Dari chart diatas kita bisa mengetahui list perusahaan beserta nominal emisi karbonnya, data ditampilkan secara global dan filtered by Emisi > 50 Ton

# ANALISA TREN EMISI PERUSAHAAN

### Tujuan : Analisa tren emisi perusahaan dari 2020 - 2023 dengan chart

### Konsep : Function plot, modul matplotlib untuk pembuatan chart

### Output : Analisis trend dengan Line Chart dan Bar Chart


```python
# Definisikan fungsi untuk membuat line chart tren emisi
def plot_tren_emisi(emisi_dict):
    # Definisikan tahun untuk sumbu x
    tahun = [2020, 2021, 2022, 2023]
    # Iterasi dictionary untuk plot setiap perusahaan
    for perusahaan, emisi_list in emisi_dict.items():
        plt.plot(tahun, emisi_list, marker='o', label=perusahaan)
    plt.xlabel('Tahun')
    plt.ylabel('Emisi (ton CO2)')
    plt.title('Tren Emisi Karbon Perusahaan 2020-2023')
    plt.axhline(y=50, color='red', linestyle='--', label='Batas Pajak (50 ton)')
    plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
    plt.tight_layout()
    # Tampilkan grafik
    plt.show()

# Baca file CSV tren_emisi.csv dari folder proyek
df = pd.read_csv('tren_emisi.csv')

# Inisiasi dictionary kosong untuk menyimpan tren emisi
emisi_dict = {}

# Iterasi setiap baris di dataframe untuk simpan ke dictionary
for index, row in df.iterrows():
    perusahaan = row['Nama_Perusahaan']
    # Simpan emisi tahunan dalam list
    emisi_list = [row['Emisi_2020'], row['Emisi_2021'], row['Emisi_2022'], row['Emisi_2023']]
    # Simpan ke dictionary
    emisi_dict[perusahaan] = emisi_list

# Panggil fungsi untuk membuat line chart
plot_tren_emisi(emisi_dict)
```


    
![image](https://github.com/user-attachments/assets/0bdc2279-7b3d-41f1-abf3-87bf54498e63)

    


### Analisa dengan metode Stacked Bar Chart


```python
# Siapkan data untuk stacked bar chart
tahun = ['Emisi_2020', 'Emisi_2021', 'Emisi_2022', 'Emisi_2023']
colors = ['#4caf50', '#2196f3', '#ff9800', '#9c27b0']

import numpy as np

x = np.arange(len(df['Nama_Perusahaan']))
bar_width = 0.6

bottom = np.zeros(len(df))

plt.figure(figsize=(12,6))
for i, year in enumerate(tahun):
    plt.bar(x, df[year], bottom=bottom, width=bar_width, label=year.replace('Emisi_', ''), color=colors[i])
    bottom += df[year].values

plt.xticks(x, df['Nama_Perusahaan'], rotation=45)
plt.ylabel('Emisi (ton)')
plt.title('Emisi Tahunan (2020–2023) per Perusahaan')
plt.legend(title='Tahun')
plt.tight_layout()
plt.show()
```


    
![image](https://github.com/user-attachments/assets/657928d1-caa2-429c-88f3-d1d7cf8520d7)

    


### Analisa dengan Grouped Bar Chart 


```python
# Daftar tahun dan warna
tahun = ['Emisi_2020', 'Emisi_2021', 'Emisi_2022', 'Emisi_2023']
colors = ['#4caf50', '#2196f3', '#ff9800', '#9c27b0']
labels = [t[-4:] for t in tahun] 

# Lebar bar dan posisi
barWidth = 0.2
x = np.arange(len(df['Nama_Perusahaan']))

# Hitung posisi tiap bar
positions = [x + i * barWidth for i in range(len(tahun))]

# Buat plot
plt.figure(figsize=(14, 7))
for i, year in enumerate(tahun):
    plt.bar(positions[i], df[year], color=colors[i], width=barWidth,
            edgecolor='grey', label=labels[i])

# Label x-axis
plt.xlabel('Perusahaan', fontweight='bold', fontsize=12)
plt.ylabel('Emisi (ton)', fontweight='bold', fontsize=12)
plt.title('Emisi Tahunan (2020–2023) per Perusahaan')

# Set posisi dan label untuk xticks
mid_pos = x + barWidth * (len(tahun) - 1) / 2
plt.xticks(mid_pos, df['Nama_Perusahaan'], rotation=45)

plt.legend(title='Tahun')
plt.tight_layout()
plt.show()
```


    
![image](https://github.com/user-attachments/assets/c4fc50eb-ff8c-4404-a757-63f5b8bc0668)

    


### Bagaimana kalau kita mau lihat data terpisah per tahun
kita bisa membuat bar chart dengan memisahkan Y Label per chart terpisah sehingga lebih mudah untuk analisa di setiap tahunnya

### Analisa Bar Chart Trend Emisi 2020


```python
# Data
x = np.arange(len(df['Nama_Perusahaan']))
bar_width = 0.6

# Urutkan berdasarkan Emisi (terbesar ke terkecil)
df_1 = df.sort_values(by='Emisi_2020', ascending=False)

plt.figure(figsize=(12,6))
plt.bar(x, df_1['Emisi_2020'], color='#4caf50', width=bar_width, edgecolor='grey')

plt.xticks(x, df_1['Nama_Perusahaan'], rotation=45)
plt.xlabel('Perusahaan', fontweight='bold', fontsize=12)
plt.ylabel('Emisi 2020 (ton)', fontweight='bold', fontsize=12)
plt.title('Emisi Tahun 2020 per Perusahaan')

plt.tight_layout()
plt.show()
```


    
![image](https://github.com/user-attachments/assets/bae3cf60-0b3e-4fae-a186-0c2c74b6b400)

    


### Analisa Bar Chart Trend Emisi 2021


```python
# Data
x = np.arange(len(df['Nama_Perusahaan']))
bar_width = 0.6

# Urutkan berdasarkan Emisi (terbesar ke terkecil)
df_1 = df.sort_values(by='Emisi_2021', ascending=False)

plt.figure(figsize=(12,6))
plt.bar(x, df_1['Emisi_2021'], color= '#2196f3', width=bar_width, edgecolor='grey')

plt.xticks(x, df_1['Nama_Perusahaan'], rotation=45)
plt.xlabel('Perusahaan', fontweight='bold', fontsize=12)
plt.ylabel('Emisi 2021 (ton)', fontweight='bold', fontsize=12)
plt.title('Emisi Tahun 2021 per Perusahaan')

plt.tight_layout()
plt.show()
```


    
![image](https://github.com/user-attachments/assets/e2627104-4106-46e6-b26c-fbcb28180ce2)

    


### Analisa Bar Chart Trend Emisi 2022


```python
# Data
x = np.arange(len(df['Nama_Perusahaan']))
bar_width = 0.6

# Urutkan berdasarkan Emisi (terbesar ke terkecil)
df_1 = df.sort_values(by='Emisi_2022', ascending=False)

plt.figure(figsize=(12,6))
plt.bar(x, df_1['Emisi_2022'], color= '#ff9800', width=bar_width, edgecolor='grey')

plt.xticks(x, df_1['Nama_Perusahaan'], rotation=45)
plt.xlabel('Perusahaan', fontweight='bold', fontsize=12)
plt.ylabel('Emisi 2022 (ton)', fontweight='bold', fontsize=12)
plt.title('Emisi Tahun 2022 per Perusahaan')

plt.tight_layout()
plt.show()
```


    
![image](https://github.com/user-attachments/assets/e017a0c9-0489-4bb4-af20-fb3f1c119a39)

    


### Analisa Bar Chart Trend Emisi 2023


```python
# Data
x = np.arange(len(df['Nama_Perusahaan']))
bar_width = 0.6

# Urutkan berdasarkan Emisi (terbesar ke terkecil)
df_1 = df.sort_values(by='Emisi_2023', ascending=False)

plt.figure(figsize=(12,6))
plt.bar(x, df_1['Emisi_2023'], color= '#9c27b0', width=bar_width, edgecolor='grey')

plt.xticks(x, df_1['Nama_Perusahaan'], rotation=45)
plt.xlabel('Perusahaan', fontweight='bold', fontsize=12)
plt.ylabel('Emisi 2023 (ton)', fontweight='bold', fontsize=12)
plt.title('Emisi Tahun 2023 per Perusahaan')

plt.tight_layout()
plt.show()
```


    
![image](https://github.com/user-attachments/assets/3fefe349-93f5-4c63-906e-ba53ad0f8c18)

    


## Kesimpulan
Kita sudah membuat chart untuk mengetahui trend emisi pada tahun 2020-2023 dengan menggunakan line chart, bar chart, grouped bar chart, dan stacked bar chart sehingga memberikan banyak opsi bagi user untuk analisa trend emisi perusahaan emisi pada tahun 2020-2023

# KESIMPULAN PROJEK

#### Latar Belakang dan Masalah Utama
Indonesia menargetkan 23% energi terbarukan pada 2025, namun hingga 2023 baru mencapai 12%.
Tiga masalah utama menghambat transisi energi hijau:
- Data emisi perusahaan yang tidak akurat, menyulitkan penerapan pajak karbon.
- Praktik greenwashing yang merajalela, dengan 56% klaim hijau tidak valid.
- Konflik lahan yang signifikan, terutama di proyek Pembangkit Listrik Tenaga Surya (PLTS), yang mengganggu investasi dan merugikan masyarakat lokal.
Masalah ini menuntut solusi berbasis data yang cerdas dan terintegrasi.

#### Tujuan Proyek
Membangun alat analisis data menggunakan Python untuk:
- Menghitung pajak karbon secara akurat agar perusahaan mematuhi regulasi.
- Mendeteksi dan memverifikasi klaim greenwashing untuk melindungi publik dan investor.
- Menganalisis risiko konflik lahan pada proyek PLTS untuk meminimalkan dampak sosial.
- Menggunakan data realistis dan metode pemrograman yang sistematis, dari logika sederhana hingga modul canggih.

#### Metodologi dan Implementasi
Penggunaan Python sebagai alat utama untuk analisis data dan pemodelan.
Pemrosesan data CSV yang mencakup emisi, klaim hijau, dan konflik lahan.
Algoritma deteksi greenwashing berdasarkan perbandingan klaim dan data emisi aktual.
Perhitungan pajak karbon berdasarkan emisi yang terverifikasi.
Analisis konflik lahan dengan data kasus dan dampak sosial.
Hasil program yang rapi dan dapat digunakan sebagai dasar rekomendasi kebijakan.

#### Hasil dan Temuan
Pajak karbon dapat dihitung dengan lebih akurat, mendorong kepatuhan industri.
Greenwashing dapat dideteksi secara efektif, mengurangi risiko penipuan informasi.
Risiko konflik lahan dapat diidentifikasi dan dianalisis untuk mitigasi yang lebih baik.
Proyek ini memberikan alat bantu yang konkret untuk pemerintah dalam pengambilan keputusan.

Proyek ini berhasil mengembangkan sebuah sistem analisis data berbasis Python yang mampu mengatasi tiga tantangan utama dalam transisi energi hijau di Indonesia: ketidakakuratan data emisi, greenwashing, dan konflik lahan. Dengan pendekatan yang sistematis dan data-driven, proyek ini tidak hanya memberikan solusi teknis, tetapi juga menyediakan dasar yang kuat untuk kebijakan yang lebih efektif dan berkelanjutan.

Keyakinan bahwa proyek ini sangat berguna untuk Indonesia:
- Relevansi Tinggi : Proyek ini langsung menjawab masalah nyata yang dihadapi Indonesia dalam mencapai target energi terbarukan 2025 dan Net Zero Emission 2060.
- Dukungan Kebijakan : Alat analisis ini dapat menjadi referensi penting bagi pemerintah dalam merancang dan mengimplementasikan kebijakan pajak karbon dan regulasi lingkungan.
- Pengurangan Risiko Sosial : Dengan menganalisis konflik lahan, proyek ini membantu mengurangi potensi konflik sosial yang dapat menghambat investasi energi hijau.
- Transparansi dan Akuntabilitas : Deteksi greenwashing meningkatkan transparansi perusahaan dan melindungi publik serta investor dari klaim palsu.
- Skalabilitas dan Adaptabilitas : Metode yang digunakan dapat dikembangkan lebih lanjut dan diterapkan di sektor lain atau wilayah lain di Indonesia.


Created by Farhan Fadillah
Batch : 9
No.Absen : 9.008.DB2025
