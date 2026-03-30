# 2. External Service Reliability

**Skenario:**  
External service sering:
- Timeout  
- Return HTTP 500  
- Kadang lambat tapi berhasil  

---

## a) Kondisi retry **tidak boleh dilakukan**
- **Response sudah sukses** → retry bisa menyebabkan **duplicate effect** atau double operation  
- **Error non-retriable** seperti HTTP 4xx (Bad Request, Unauthorized) → retry tidak berguna  
- **Operasi dengan side-effect kritis** sudah dieksekusi → retry bisa merusak data / state  

---

## b) Perbedaan Retry vs Circuit Breaker

| Aspek | Retry | Circuit Breaker |
|-------|-------|----------------|
| Tujuan | Mencoba request lagi saat gagal (misal network timeout) | Memutus sementara request ke service bermasalah supaya tidak overload |
| Timing | Dilakukan setelah request gagal | Aktif saat service bermasalah terus menerus |
| Risiko | Jika tanpa backoff/jitter → thundering herd | Request langsung gagal saat breaker open, mengurangi risiko overload |
| Implementasi | Loop + exponential backoff | Open/Closed/Half-Open state + failure threshold |

**Ringkasan:**  
- Retry = “coba lagi”  
- Circuit breaker = “stop dulu kalau service bermasalah”  

---

## c) Risiko retry tanpa jitter atau backoff
- **Thundering herd:** banyak request bersamaan membanjiri service → service makin down  
- **Resource exhaustion:** DB, memory, thread pool habis karena semua retry bersamaan  
- **Latency meningkat:** retry bersamaan menyebabkan antrean request memanjang  

**Rekomendasi:**  
- Gunakan **exponential backoff + jitter** → retry terdistribusi, beban service stabil  
- Pisahkan **retriable vs non-retriable errors** → hindari retry sia-sia  

---

**Catatan praktis:**  
- Pastikan operasi yang di-retry bersifat **idempotent** → hasil tetap sama meski dipanggil berkali-kali  
- Kombinasi **retry + circuit breaker + timeout** → pola standar microservice resilient design  