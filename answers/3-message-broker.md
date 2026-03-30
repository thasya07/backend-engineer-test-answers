# 3. Message Broker Handling

**Skenario:** Event `CustomerUpdated` dengan ordering penting dan duplicate tidak bisa dihindari

## a) Agar consumer idempotent:
- Simpan `eventId` terakhir → skip duplicate  
- Operasi harus **stateless / idempotent**  

## b) Ordering dijamin oleh:
- **Broker** (Kafka: partition ordering, RabbitMQ: queue ordering)  
- Consumer hanya memproses urutan yang diterima  

## c) Dampak jika ordering tidak terjaga:
- Data inconsistent → update profile bisa rollback salah  
- Bisa menimbulkan bug/data corrupt