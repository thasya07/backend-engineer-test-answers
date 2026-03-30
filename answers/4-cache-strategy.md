# 4. Cache Strategy

**Skenario:** Service traffic tinggi, query DB mahal

## a) Kapan cache di-invalidate:
- Setelah update/delete di DB → hapus cache  
- TTL otomatis  

## b) Cache sebagai source of truth?
- **Tidak boleh**, DB tetap sumber utama  

## c) Mencegah cache stampede:
- **Lock per key:** hanya satu request rebuild cache  
- **Random TTL / jitter:** supaya banyak key tidak expire bersamaan