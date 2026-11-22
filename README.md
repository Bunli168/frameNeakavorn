# frameNeakavorn

Telegram Frame Bot ដែលទទួលរូបភាព (១ សន្លឹក ឬ Album) ហើយបំពាក់ស៊ុម (`កឋិន.png`) ជូនអ្នកប្រើប្រាស់វិញ។

## Deploy នៅលើ Render (Free Tier)

### វិធីទី ១: Deploy តាម Blueprint (`render.yaml`) — ណែនាំ
1. ចូលទៅកាន់ [Render Dashboard](https://dashboard.render.com) → **New +** → **Blueprint**។
2. ភ្ជាប់ GitHub repository `Bunli168/frameNeakavorn` (branch `main`)។
3. Render នឹងអាន `render.yaml` ដោយស្វ័យប្រវត្តិ — ពេលសួរ Environment Variable សូមបញ្ចូល `TELEGRAM_BOT_TOKEN` របស់អ្នក ហើយចុច **Deploy Blueprint**។

### វិធីទី ២: បង្កើត Web Service ដោយផ្ទាល់ (Manual)
- **Service Type**: Web Service (`Free` plan)
- **Runtime**: `Python 3` (pin ដោយ `.python-version` = `3.13`)
- **Build Command**: `pip install -r requirements.txt`
- **Start Command**: `python -u main.py`
- **Health Check Path**: `/health`
- **Environment Variables**:
  - `TELEGRAM_BOT_TOKEN` = `<your_bot_token>` (ចាំបាច់)
  - `FRAME_PATH` = `កឋិន.png` (ជា default ស្រាប់)
  - `ALBUM_TIMEOUT` = `2.0`
  - `JPEG_QUALITY` = `90`
  - *(មិនបាច់កំណត់ `PORT` ទេ — Render បញ្ចូលឱ្យស្វ័យប្រវត្តិ)*

### ការពារកុំឱ្យ Free Service Sleep (Keep-Alive)
សេវាកម្ម Free Web Service នៅលើ Render នឹង sleep ក្រោយគ្មាន HTTP traffic រយៈពេល 15 នាទី។
ដើម្បីឱ្យ Bot ដំណើរការ 24/7 សូមបង្កើត monitor នៅលើ **UptimeRobot** ឬ **cron-job.org** ឱ្យ ping ទៅ `https://<your-service>.onrender.com/health` រៀងរាល់ **10–14 នាទី** ម្តង។

## Run នៅលើម៉ាស៊ីនផ្ទាល់ (Local)
```bash
cp .env.example .env
# បញ្ចូល TELEGRAM_BOT_TOKEN ក្នុង .env
pip install -r requirements.txt
python main.py
```
