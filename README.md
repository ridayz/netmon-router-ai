# NetMon Router AI — Network Monitoring + Router AI (Dummy)

Dashboard monitoring perangkat jaringan gaya pastel biru awan + putih.

## Isi dummy v1
- `index.html` / `netmon-dummy.html`: dashboard dummy full frontend
  - Sidebar: pilih Router A/B/C → list interface
  - Kartu: Download / Upload / Latency / Packet Loss
  - Grafik traffic realtime (simulasi 1 detik, Chart.js)
  - Panel Router AI + tombol Analisa & Perbaiki (simulasi log)

## Cara jalanin
Buka `index.html` langsung di browser, atau:
```bash
npx serve netmon-router-ai
```

## Roadmap ke asli
1. Backend collector SNMP / MikroTik API → WebSocket (1-2 dtk)
2. AI 2 level: analisa anomali → suggest → approve → eksekusi
3. Auth + multi-user + histori traffic (SQLite/Postgres)

Status: dummy UI untuk validasi tampilan.
