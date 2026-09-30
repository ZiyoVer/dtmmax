# DTMMax

**O‘zbek tilida imtihonlarga tayyorlanish uchun AI va ta’lim vositalarini birlashtirgan veb platforma.**

DTMMax o‘quvchi, o‘qituvchi va administrator uchun alohida ish jarayonlarini taqdim etadi. Repozitoriyda AI suhbat, test topshiriqlari, flashcardlar, bilimlar bazasi va natijalarni kuzatish modullari mavjud.

[Platforma](https://www.dtmmax.uz) · [Backend](backend/src) · [Frontend](frontend/src) · [Baza sxemasi](backend/prisma/schema.prisma)

## Asosiy imkoniyatlar

- O‘zbek tilidagi AI suhbat va oqim orqali javob berish.
- Test yaratish, topshirish, natijalarni hisoblash va tahlil qilish.
- Flashcardlar va o‘quv jarayonidagi natijalarni kuzatish.
- Hujjatlar hamda bilimlar bazasi bilan ishlash.
- O‘qituvchi paneli va administrator boshqaruvi.
- Email, obyekt saqlash xizmati va to‘lov provayderlari uchun integratsiya modullari.

## Arxitektura

```text
React interfeysi
       ↓ /api
Express + TypeScript
       ├── Prisma → PostgreSQL
       ├── AI provayderlari → suhbat va materiallar bilan ishlash
       ├── S3-compatible storage → fayllar
       └── Email va billing integratsiyalari
```

| Qism | Texnologiyalar |
| --- | --- |
| Interfeys | React 19, TypeScript, Vite, Tailwind CSS, Zustand |
| Server | Node.js, Express 5, TypeScript |
| Ma’lumotlar | PostgreSQL, Prisma, S3-compatible storage |
| AI | OpenAI SDK orqali provayder integratsiyalari, DeepSeek va Gemini sozlamalari |
| Kontent | Markdown, KaTeX, PDF va hujjatlarni qayta ishlash |

## Lokal ishga tushirish

Node.js, npm va alohida lokal PostgreSQL bazasi kerak. AI, email va saqlash funksiyalari uchun o‘zingizning xizmat hisoblaringizni sozlang.

```bash
git clone https://github.com/ZiyoVer/dtmmax.git
cd dtmmax
npm --prefix backend ci
npm --prefix frontend ci
cp backend/.env.example backend/.env
```

`backend/.env` ichida kamida `DATABASE_URL`, `JWT_SECRET`, `FRONTEND_URL` va `ALLOWED_ORIGINS` ni lokal muhitga moslang. Vite odatda `http://localhost:5173`, backend esa `http://localhost:8080` orqali ishlaydi. Kerakli AI provayderi kalitlarini ham shu faylda sozlang.

**Yangi, bo‘sh lokal baza** uchun Prisma sxemasini yarating:

```bash
cd backend
npx prisma generate
npx prisma db push
npm run dev
```

Boshqa terminalda, loyiha ildizidan:

```bash
npm --prefix frontend run dev
```

Server holati: `http://localhost:8080/api/health`.

Mavjud yoki production baza bilan ishlashdan oldin [migratsiyalar qo‘llanmasini](backend/MIGRATIONS.md) o‘qing. Yuqoridagi baza yaratish qadami yangi lokal muhit uchun yozilgan.

## Repozitoriy xaritasi

| Manzil | Vazifasi |
| --- | --- |
| `frontend/src/pages/Student/` | O‘quvchi suhbati, test va o‘quv interfeyslari |
| `frontend/src/pages/Teacher/` | O‘qituvchi paneli |
| `frontend/src/pages/Admin/` | Boshqaruv va billing vositalari |
| `backend/src/routes/` | API modullari |
| `backend/src/utils/` | AI, baholash, saqlash va boshqa yordamchi modullar |
| `backend/prisma/` | Baza sxemasi va migratsiyalar |
| `mcp-server/` | Lokal dasturlash vositalari uchun MCP server |

## Loyiha holati

Bu faol ishlab chiqilayotgan ilova repozitoriysi. Ishlaydigan muhit uchun tashqi xizmatlar va konfiguratsiya zarur; foydalanuvchi ma’lumotlari yoki production bazasi taqdim etilmaydi. [Platforma spetsifikatsiyasi](PLATFORM_SPEC.md) mahsulot yo‘nalishini tasvirlaydi; amaldagi imkoniyatlarni tegishli kod modullaridan tekshirish mumkin.

**Muallif:** [O‘ktam Ziyodullayev](https://github.com/ZiyoVer)
