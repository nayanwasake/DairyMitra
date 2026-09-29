# DairyMitra (डेयरीमित्र / डेअरीमित्र) 🌾
### AI-Powered Feed & Silage Quality Screening & Management Platform for Indian Dairy Farmers
**Smart India Hackathon 2026 | Problem Statement: SIH26111**  
**Team Nexora | Team ID: CS002 | Theme: Agriculture, FoodTech & Rural Development**

---

## 🌟 Executive Overview
In Indian dairy farming, **feed accounts for 65–70% of total milk production costs**. Subclinical mycotoxicosis (from moldy corn silage or damp hay) and clostridial acidosis cause silent daily milk drops of **1.5 to 3.0 Litres per cow**, chronic infertility, and acute cattle mortality.

Traditional lab testing is **prohibitively expensive (₹2,000–₹4,000 per sample)** and takes **7–14 days** — far too slow for smallholders.

**DairyMitra** delivers an instant, barn-side screening solution directly in the hands of farmers:
1. **Photo Capture**: Analyzes color, moisture texture, kernel integrity, and surface mold with client-side image brightness/blur verification.
2. **pH Strip Scanner**: Scans affordable 50-paise paper litmus strips against a calibrated color chart with a manual fallback slider.
3. **Dual-Layer AI + Veterinary Safety Engine**: Combines Google Gemini multimodal vision with a deterministic safety layer (`safetyRules.ts`) that enforces strict veterinary thresholds (e.g. silage pH > 4.8 or foul smell immediately flags high risk/quarantine).
4. **Live Weather Hazard Integration**: Free Open-Meteo API checks local temperature, humidity, and rainfall to predict monsoon spoilage on unsealed pits and bunkers.
5. **Multilingual Voice Guidance**: Recites feeding directives and ration advice aloud in **English, Hindi, and Marathi** via the Web Speech API.
6. **Batch & Trend Tracking**: Tracks fermentation stability over time with interactive Recharts timelines and smart recheck reminders.
7. **Offline-First PWA**: Service Worker caching of the app shell and local queueing ensure uninterrupted field usage even in rural sheds with intermittent connectivity.

---

## 🚀 Live Localhost Access

The development server is actively running at:
```bash
http://localhost:5173/
```
Network access (mobile devices on same Wi-Fi):
```bash
http://<your-ip>:5173/
```

---

## 🛠️ Tech Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 18, Vite 6, TypeScript, Tailwind CSS, Lucide Icons |
| **Data Visualizations** | Recharts (Fermentation quality score trends) |
| **i18n Localization** | react-i18next (English, हिन्दी, मराठी) |
| **Voice / TTS** | Web Speech API (`SpeechSynthesis` with regional voice tags) |
| **Backend & Database** | Supabase (PostgreSQL with Row Level Security, Storage Buckets) |
| **Edge Function AI** | Supabase Edge Function (`analyze-feed-quality`) invoking Google Gemini Vision API |
| **Weather API** | Open-Meteo REST API (free, real-time temperature, humidity, precipitation) |
| **Safety Logic** | Deterministic agronomic rule overrides (`src/config/safetyRules.ts`) |

---

## 💻 Quick Start & Setup

### 1. Prerequisites
- Node.js (v18+)
- npm / pnpm

### 2. Installation
```bash
git clone https://github.com/nexora/dairymitra.git
cd dairymitra
npm install
```

### 3. Environment Configuration
Create `.env` based on `.env.example`:
```env
# Optional Supabase credentials for cloud persistence
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key

# Demo Mode: Set to true for 1-click evaluation without external keys
VITE_DEMO_MODE=true

# Google Gemini API Key (multimodal vision screening)
GEMINI_API_KEY=your_gemini_api_key_here
```

### 4. Run Development Server
```bash
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## 🛡️ Deterministic Safety Rules Engine (`safetyRules.ts`)

| Parameter | Threshold | Safety Override Action |
|---|---|---|
| **Silage pH** | `> 4.8` | Overrides risk to **MEDIUM**; warns of clostridial risk; limits ration to &lt;25%. |
| **Critical Silage pH** | `> 5.2` | Overrides risk to **HIGH RISK / QUARANTINE**; "DO NOT FEED" directive issued. |
| **Visible Mold** | Detected | Minimum **MEDIUM RISK**; if coupled with foul smell or slime, triggers **HIGH RISK**. |
| **Core Temperature** | `> 40°C` | Aerobic yeast deterioration alert; advises shaving vertical face by 30cm daily. |
| **Extreme Heat** | `> 48°C` | High risk thermal browning & protein denaturation warning. |
| **Hay Moisture** | `> 20%` | Warning for spontaneous heating & aspergillus mold risk. |
| **Open Heap Storage** | `> 7 days` | Elevated spoilage warning due to rain and unsealed air exposure. |

---

## 🧪 Hackathon Evaluator Quick Walkthrough

1. **Landing Page**: View SIH 2026 problem overview, 4-step interactive flow, and Team Nexora details. Switch between **EN / हिन्दी / मराठी** in the top header.
2. **Dashboard**: Observe the live **Open-Meteo** weather widget for Kolhapur, active batch metrics, and high-risk hazard warnings.
3. **Run a New Scan**:
   - **Step 1**: Choose a feed type (e.g. Corn Silage) and select a sample photo.
   - **Step 2**: Test the calibrated pH slider or tap sample pH strip buttons.
   - **Step 3**: Adjust moisture %, temperature, and toggle sensory flags (e.g., visible mold).
   - **Step 4**: Confirm summary with local weather attached and click **"Run AI Quality Screening"**.
4. **Result Screen**: Inspect the 0–100 quality gauge, click **"Listen to Voice Summary"** to hear audio readout, review contributing factors, and print/export the PDF report.
5. **Batches & Trends**: Explore "Pit Silo #1" and view the Recharts quality score trend line over time.

---

**Built with pride for Smart India Hackathon 2026 by Team Nexora (CS002)**
