# BRAIN — NetMon Router AI (otak projek, selalu diingat AI)

> File ini + AGENTS.md root = memori permanen projek. Setiap sesi baru, AI wajib baca file ini dulu.

## 1. Apa ini
Network Monitoring + Router AI — dashboard monitoring perangkat jaringan + AI diagnosa.
Status: **dummy v1** (frontend only, data simulasi). Repo: `ridayz/netmon-router-ai` (public).
Live file: `index.html` (alias `netmon-dummy.html`), single-file, Chart.js via CDN.

## 2. Gaya visual (wajib dipertahankan)
- Pastel biru awan + putih: `#e0f2fe`, `#bae6fd`, `#7dd3fc`, aksen `#0284c7`, teks `#0c4a6e`.
- Rounded 12–18px, kartu putih border pastel, gaya archify bersih.
- Diagram statis archify: `archify-output/topologi-netmon.html` (9/9 showcase pass, spec sha `2def28…`).

## 3. Fitur dummy v1 (jangan dihapus tanpa izin user)
1. Sidebar: pilih Router A/B/C → list interface (klik = monitor, **klik kanan** = disable/enable + simulasi cabut kabel).
2. Kartu DL/UL/latency/loss + grafik realtime 1 detik.
3. Layer 1 copper TDR: OPEN/SHORT + estimasi jarak fault + PoE + speed.
4. Layer 1 SFP DDM: TX/RX dBm, redaman = TX−RX, temp/volt/bias, LOS alarm.
5. Error counter: CRC/FCS/collision/flap/last-change.
6. **Router AI full-driven** (prinsip inti): alur = `Diagnosa → 1 arahan → Jalankan Arahan AI` + toggle auto-resolve.
   DILARANG tambah tombol aksi manual (flap/PoE/100M/enable manual) — semua physical action hanya atas arahan AI.
7. Tab Topologi: SVG pastel, node draggable, **klik kanan node = ganti icon** (internet 🌐 / router vector ala MikroTik pastel / switch 🔀 / PC 🖥 / server 🗄 / firewall 🧱), tambah/hapus node, IP publik via `api.ipify.org` fallback dummy `203.0.113.10`.
8. Tab 🔔 Log/Alarm: event timestamp + severity (info/warn/crit) + filter + badge merah + bunyi opsional + bersihkan. Otomatis catat: DOWN (crit, throttle 20 dtk/device), loss > 5% (warn), disable manual (crit), hasil diagnosa + eksekusi AI.

## 4. Data fault dummy (skenario uji)
- `ether4-CCTV` = putus-23m (TDR OPEN @23m, PoE 0W) → arahan: PoE cycle + tiket teknisi.
- `ether3-AP` = kabel-jelek (CRC↑, SHORT 41m) → arahan: turun 100M + recabling.
- `sfp1-Fiber` = redaman-tinggi (RX −24.6 dBm) → arahan: bersih konektor + cek bending.
- `sfp1-Uplink` (Router B) = no-light (RX −40 dBm, LOS) → arahan: tiket fiber, JANGAN flap.
- `ether2-Office` (Router B) = disabled-human → arahan: enable + catat aktor (satu-satunya yang boleh auto-enable).
- Sisanya sehat.

## 5. Prinsip AI (kekuatan = diagnosa)
- Korelasi: admin/oper + TDR + DDM + CRC/FCS + flap + PoE + LLDP + syslog + last-change.
- Output: vonis + confidence % + 1 arahan tunggal.
- Layer 1 putus/no-light = INFO + tiket, tidak ada fix remote.
- Auto-enable hanya untuk human-error (port access, catat aktor, ada kill-switch).
- Aturan SFP: RX ≤ −25 dBm kritis; redaman = TX−RX; no-light = jangan flap berulang.
- Roadmap: baseline histori + deteksi anomali pre-DOWN, korelasi multi-port, auto-tiket ke tiket-app + daftar bawaan teknisi.

## 6. Perintah cepat
- Buka: `netmon-router-ai/index.html` (preview).
- Tambah fault baru: edit `DB` di `<script>` + tambah cabang di `aiDiagnose()` + `runAiPlan()`.
- Setelah edit: copy `index.html` → `netmon-dummy.html` + `../netmon-dummy.html`, commit, push `origin main`.
- Diagram archify: edit `archify-output/topologi-netmon.architecture.json` → `validate --quality showcase` → `deliver` (jangan edit pasca-pass).

## 7. Log
- 2026-10-09: dummy dashboard pastel + AI simulasi → repo baru `ridayz/netmon-router-ai`.
- 2026-10-09: +Layer 1 TDR/DDM + full AI-driven (hapus tombol manual) + klik kanan disable.
- 2026-10-09: +Tab Topologi archify-style + icon internet 🌐 + deteksi IP publik.
- 2026-10-10: router jadi vector ala MikroTik pastel (lainnya balik emoji); +Tab 🔔 Log/Alarm (badge + filter + bunyi).
- 2026-10-09: otak disimpan (AGENTS.md + BRAIN.md, BRAIN di-push).
