# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 10 | 10 | 3 | 3 | 7 | 7 |
| mid | 6 | 6 | 0 | 0 | 3 | 3 |
| edge | 1 | 1 | 0 | 0 | 0 | 0 |

## Findings action=rework

Khong co dong nao trong findings.csv mang action=rework va severity=P0/P1, nen khong sua nhan nao trong CVAT o buoc nay. So matched/missing/spurious truoc va sau giong het nhau vi ban khoa lai dung ban da lock r1_craft, khong doi noi dung. Cac khac biet da ghi nhan deu o muc keep_with_reason hoac mot ca escalate (adasind_086220.jpg R4), khong phai loi can rework ngay.