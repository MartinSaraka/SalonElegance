# ⚡ Rýchly štart

## 3 jednoduché kroky k vašej stránke

### 1️⃣ Nainštalujte závislosti

```bash
cd salon-demo
npm install
```

### 2️⃣ Spustite vývojový server

```bash
npm run dev
```

Otvorte `http://localhost:3000` v prehliadači.

### 3️⃣ Upravte obsah

#### Kontaktné údaje (POVINNÉ):

1. **Telefón a email** - Vyhľadajte a nahraďte vo všetkých súboroch:
   - `+421 901 234 567` → váš telefón
   - `info@salonelegance.sk` → váš email

2. **Názov salónu** - Nahraďte "Salon Elegance" v:
   - `nuxt.config.ts` (riadok 8)
   - `components/Navigation.vue` (riadok 9)
   - `components/Footer.vue` (riadok 5)

3. **Adresa** - Upravte v:
   - `components/ContactSection.vue` (riadky 20-22)
   - `components/Footer.vue` (riadok 46)

#### Služby a ceny:

Upravte v `components/ServicesSection.vue` (riadky 50-97):
```typescript
const services = [
  {
    title: 'Názov služby',
    description: 'Popis služby',
    price: '25',  // ← Zmeňte cenu
    duration: '60 min',
    icon: 'mdi:content-cut',
    image: 'url-obrazku'
  }
]
```

## 🚀 Deploy na Vercel

### Najrýchlejší spôsob:

```bash
# 1. Nainštalujte Vercel CLI
npm install -g vercel

# 2. Prihláste sa
vercel login

# 3. Deploy
vercel --prod
```

**Hotovo!** Za 2 minúty máte stránku online! 🎉

### Alternatíva - cez GitHub:

1. Vytvorte repozitár na GitHub
2. Push kódu:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <url>
   git push -u origin main
   ```
3. Importujte na [vercel.com](https://vercel.com)
4. Deploy sa spustí automaticky

## 📋 Checklist pred spustením

- [ ] Zmenené kontaktné údaje (telefón, email, adresa)
- [ ] Upravený názov salónu
- [ ] Aktualizované ceny služieb
- [ ] Zmenené otváracie hodiny
- [ ] Nahradené ukážkové obrázky (voliteľné)
- [ ] Pridané vlastné logo (voliteľné)
- [ ] Upravená Google Maps adresa

## 🆘 Potrebujete pomoc?

Prečítajte si:
- `README.md` - Kompletná dokumentácia
- `DEPLOYMENT.md` - Detailný návod na deployment

---

**Trvanie celého setupu: 15-30 minút** ⏱️

**Ťažkosť: Začiatočník friendly** ✅

