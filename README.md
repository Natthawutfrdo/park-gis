# 🌿 ระบบ BigData GIS กรมอุทยานแห่งชาติ สัตว์ป่า และพันธุ์พืช

ระบบแสดงผลข้อมูล Shapefile ขนาดใหญ่ผ่านเว็บ  
**Stack**: ArcGIS → GitHub → Supabase → MapLibre GL JS

---

## 📁 โครงสร้างโปรเจกต์

```
park-gis/
├── .github/
│   └── workflows/
│       └── convert.yml          ← CI/CD แปลงข้อมูลอัตโนมัติ
├── data/
│   ├── shapefiles/              ← วางไฟล์ .shp ที่นี่
│   ├── geojson/                 ← ผลลัพธ์ที่แปลงแล้ว (auto)
│   └── pmtiles/                 ← Map tiles (auto)
├── scripts/
│   ├── convert.py               ← แปลง SHP → GeoJSON
│   ├── upload_supabase.py       ← อัปโหลดขึ้น Supabase
│   └── requirements.txt         ← Python dependencies
├── web/
│   └── index.html               ← Web Viewer (deploy บน GitHub Pages)
├── docs/
│   └── setup.md                 ← คู่มือติดตั้งละเอียด
└── README.md
```

---

## 🚀 วิธีเริ่มต้นใช้งาน (Quick Start)

### ขั้นตอนที่ 1: สร้าง Repository บน GitHub

```bash
# Clone หรือสร้างใหม่
git clone https://github.com/YOUR_ORG/park-gis.git
cd park-gis

# ติดตั้ง Git LFS (สำหรับไฟล์ขนาดใหญ่)
git lfs install
git lfs track "*.shp" "*.dbf" "*.prj" "*.shx" "*.pmtiles"
git add .gitattributes
git commit -m "setup: git lfs tracking"
```

### ขั้นตอนที่ 2: ตั้งค่า Supabase

1. ไปที่ https://supabase.com → สร้าง Project ใหม่
2. เปิด SQL Editor แล้วรัน SQL จากไฟล์ `docs/setup.md`
3. ไปที่ Settings → API → คัดลอก `URL` และ `anon key`

### ขั้นตอนที่ 3: ตั้งค่า GitHub Secrets

ไปที่ GitHub Repository → Settings → Secrets → Actions → New secret:

| Secret Name | ค่า |
|------------|-----|
| `SUPABASE_URL` | URL จาก Supabase |
| `SUPABASE_KEY` | Service role key จาก Supabase |

### ขั้นตอนที่ 4: วาง Shapefile และ Push

```bash
# วางไฟล์ shapefile ใน data/shapefiles/
cp /path/to/your/park_boundary.shp data/shapefiles/
cp /path/to/your/park_boundary.dbf data/shapefiles/
cp /path/to/your/park_boundary.prj data/shapefiles/
cp /path/to/your/park_boundary.shx data/shapefiles/

# Push → GitHub Actions จะทำงานอัตโนมัติ
git add .
git commit -m "data: add park boundary shapefile"
git push
```

### ขั้นตอนที่ 5: เปิด GitHub Pages

ไปที่ Repository → Settings → Pages → Source: `main` branch, folder `/web`

เว็บแผนที่จะพร้อมใช้งานที่:  
`https://YOUR_ORG.github.io/park-gis/`

---

## 📖 ดูรายละเอียดเพิ่มเติม

→ `docs/setup.md` — คู่มือติดตั้งทีละขั้นตอนพร้อมภาพประกอบ
