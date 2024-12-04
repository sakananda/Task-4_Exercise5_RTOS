# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)

- **Diva Sakananda (3222600013)**  
- **Billy Lukito Danuharja (3222600027)**  

# Task 4 Exercise 5 - Demonstrate access contention problems when using shared resources in a multitasking system.

## Deskripsi Projek
Proyek ini bertujuan untuk mendemonstrasikan **masalah kontensi akses (access contention)** yang terjadi ketika dua task mencoba menggunakan **sumber daya bersama** dalam sistem multitasking. Masalah ini menunjukkan risiko data korupsi atau kegagalan task jika tidak ada mekanisme proteksi yang tepat. 

Proyek ini menggunakan STM32 untuk:
- **GreenLedTask**: Menghidupkan dan mematikan LED hijau secara berkala, serta mengakses sumber daya bersama.
- **RedLedTask**: Menghidupkan dan mematikan LED merah lebih sering dengan prioritas lebih tinggi, juga mengakses sumber daya bersama.
- **AccessSharedData**: Fungsi yang mensimulasikan akses ke sumber daya bersama dengan **indikasi LED biru** jika terjadi kontensi akses.


### Detail Task
1. **GreenLedTask (Prioritas: Normal)**  
   - Task ini menghidupkan LED hijau, mengakses sumber daya bersama melalui fungsi `AccessSharedData`, mematikan LED hijau, lalu menunggu selama 0,5 detik sebelum mengulangi proses.  
   - Karena prioritasnya normal, task ini sering ditunda jika task dengan prioritas lebih tinggi aktif.  
   - Waktu total periodik = akses sumber daya (500 ms) + osDelay (500 ms) ≈ 1 detik.  

2. **RedLedTask (Prioritas: Above Normal)**  
   - Task ini menghidupkan LED merah, mengakses sumber daya bersama, mematikan LED merah, lalu menunggu selama 0,1 detik sebelum mengulangi proses.  
   - Dengan prioritas lebih tinggi, task ini lebih sering mempreemp task lain, meningkatkan kemungkinan kontensi akses.  
   - Waktu total periodik = akses sumber daya (500 ms) + osDelay (100 ms) ≈ 600 ms.  

3. **AccessSharedData**  
   - Fungsi ini menggunakan `Start_Flag` untuk mengelola akses sumber daya bersama:
     - Jika `Start_Flag == 1`, task diperbolehkan mengakses sumber daya, dan `Start_Flag` diatur ke 0.  
     - Jika `Start_Flag == 0`, terjadi kontensi akses, dan LED biru menyala.  
   - Proses simulasi akses dilakukan dengan `HAL_Delay(500)`.

---

### Hubungan Antara Task
- **GreenLedTask** dan **RedLedTask** saling berbagi sumber daya bersama melalui `AccessSharedData`.  
- Jika dua task mencoba mengakses secara bersamaan, task dengan prioritas lebih tinggi akan berjalan lebih dulu, sementara task dengan prioritas lebih rendah hanya mendeteksi kontensi dan tetap menjalankan delay simulasi.  

---

## Foto Hardware
![foto hardware task 5](https://github.com/user-attachments/assets/ad0a5332-fcf2-4d59-aa9c-bd828a499cbf)


## Short Video Hardware


https://github.com/user-attachments/assets/840a88a2-9ee4-4675-892b-4888558521e6


