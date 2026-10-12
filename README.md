# UmiFlow — meditatsiya web-platforma (MVP)

## Ishga tushirish
`index.html` faylini Chrome, Edge, Safari yoki Firefox brauzerida oching. Internet kerak emas. Lokal server orqali ishlatish ham mumkin: `python3 -m http.server 8000` va `http://localhost:8000`.

## Ishlaydigan funksiyalar
- Oldinga (00:00 dan cheksiz sekundomer) va orqaga (tanlangan vaqtgacha) sanaydigan taymer rejimlari.
- Har doim ko‘rinadigan 1000 soatlik shaxsiy umumiy maqsad.
- Kunlik (7 kun), oylik (12 oy, Yan/Fev/Mar/Apr/May/Iyun/Iyul/Avg/Sen/Okt/Noy/Dek) va 2026-yildan boshlangan yillik grafiklar.
- Tun/kunduz dizayn rejimi: yon va mobil menyudan bir bosishda almashtirish.
- Ustoz Umida va o‘quvchilar F.I.Sh.ini tahrirlash.
- Start/pauza/davom etish/yakunlash meditatsiya taymeri (5/10/20/30/60 daqiqa).
- Seanslarni localStorage ga yozish (kamida 60 soniya).
- Bugun, oxirgi 7 kun va umumiy statistika, grafik, haftalik maqsad.
- Seans tarixi va CSV eksport. Tanlangan profilning eng oxirgi seansini tasdiqlab o‘chirish (statistikani qayta hisoblaydi).
- Ustoz/o‘quvchi demo-kabinetlarini almashtirish, demo-o‘quvchi qo‘shish.
- JSON zaxira nusxasini olish, lokal ma’lumotlarni tozalash.
- Mobilga mos premium dark/violet UI.

## Muhim cheklovlar
Bu prototipda real login, parol, server, ma’lumotlar bazasi, rollar bo‘yicha xavfsiz kirish va o‘quvchilarning o‘z qurilmalaridan sinxronlash **yo‘q**. Kabinet tanlash faqat lokal demonstratsiya; hech kimning real shaxsiy ma’lumotlarini saqlamang. Taymer ishlashi uchun sahifa ochiq bo‘lishi lozim; brauzer yopilsa yakunlanmagan seans saqlanmaydi. Vaqt qayd etilishi foydalanuvchi boshlagan taymerga asoslanadi; haqiqiy meditatsiyani tekshirish vositasi emas.

## Keyingi texnik arxitektura
- Frontend: Next.js + React + TypeScript + Tailwind CSS.
- Auth: Supabase Auth (email/password, magic link), teacher/student rollari.
- DB: PostgreSQL (Supabase) + Row Level Security (RLS).
- Jadvallar: profiles(id, display_name, role, teacher_id, consent_at), sessions(id, profile_id, started_at, ended_at, duration_seconds), goals(profile_id, weekly_minutes).
- Kirish: o‘quvchi faqat o‘z ma’lumotlarini ko‘radi; ustoz faqat rozilik bergan, biriktirilgan o‘quvchilarning agregat natijalarini ko‘radi. RLS va server tomondagi tekshiruvlar majburiy.
- Ishonchlilik: yakunlangan seanslarni serverda saqlash, vaqt chegarasi validatsiyasi, takroriy yozuvdan himoya.
- Maxfiylik: rozilik, akkauntni o‘chirish, ma’lumot eksporti, minimal ma’lumot yig‘ish va HTTPS.
- Joylash: Vercel + Supabase, maxsus domen keyinchalik.
