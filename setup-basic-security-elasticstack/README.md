#Setup security for Elasticsearch stack

Production mode ต้องทำ **TSL/SSL** เพื่อ ensure ว่าจะไม่มี unauthorized nodes เข้ามา join cluster

### Elasticsearch Ports (Default)
1. **Transport** มีไว้ให้ nodes คุยกัน **9300**
2. **REST** มีไว้ให้เรียกใช้ APIs **9200**
   
---

##Generate CA (Certificat Authority)

ทุก nodes ใน cluster ต้องคุยกันได้
ต้องทำให้ internode encrypted and verified
ใน secure cluster, Elasticsearch จะใช้ CA เพื่อยืนยันตัวตนตอนคุยกับ node อื่นๆ
cluster ต้อง validate จาก cert พวกนี้

**Recommended Approach**
> ให้ trust CA สักที่นึง เมื่อมี node ใหม่ join เข้า cluster จะต้องใช้ cert ที่ signed ด้วย CA ที่เดียวกัน

**Recommended for Transport layer**
> ใช้ CA ที่ separate, dedicated แทน CA เดิมที่มีอยู่ (อาจจะ share CA ให้ node ที่เรา tightly controlled)
> Use the `elasticsearch-certutil` tool to generate a CA for cluster.