# 5. Internal Communication & Security

**Skenario:** HTTP antar microservice

## a) Apakah API key cukup?
- Tidak cukup → API key bisa dicuri  

## b) Mencegah service palsu:
- Mutual TLS (mTLS) antar service  
- JWT dengan signature rahasia internal  

## c) Risiko JWT tanpa expiry pendek:
- Jika token leak → bisa dipakai lama  
- Tidak bisa revoke cepat → security risk