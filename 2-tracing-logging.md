# 2. Tracing & Logging

**Skenario:** User laporan “data hilang”, tapi tidak ada error di log

## a) Minimum log info per service:
- `traceId / correlationId` → untuk link request antar service  
- Timestamp → kapan event/request terjadi  
- `userId / requestId` → siapa yang request  
- Service name & method → asal log  
- Error code/status/message  

## b) Cara trace request:
- Gunakan **distributed tracing** (Jaeger, Zipkin) dengan **traceId** konsisten  
- Filter traceId di semua service → lihat path request dari API gateway → service → DB → external service  

## c) Dampak traceId tidak konsisten:
- Sulit men-debug issue  
- Data bisa “hilang” secara visual karena log tidak bisa dirangkai