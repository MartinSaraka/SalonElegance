# 🚀 Návod na nasadenie projektu

## Rýchly štart - Deploy na Vercel za 5 minút

### Krok 1: Príprava projektu

```bash
cd salon-demo
npm install
```

### Krok 2: Otestovanie lokálne

```bash
npm run dev
```

Otvorte `http://localhost:3000` a skontrolujte, či všetko funguje.

### Krok 3: Vytvorenie Git repozitára

```bash
git init
git add .
git commit -m "Initial commit - Salon website"
```

### Krok 4: Nahratie na GitHub

1. Vytvorte nový repozitár na [GitHub.com](https://github.com/new)
2. **Nepridávajte** README, .gitignore ani licenciu (už ich máme)
3. Skopírujte URL repozitára
4. Vykonajte:

```bash
git remote add origin <URL_VÁŠHO_REPOZITÁRA>
git branch -M main
git push -u origin main
```

### Krok 5: Deploy na Vercel

#### Varianta A: Cez Vercel Dashboard (Odporúčané pre začiatočníkov)

1. Navštívte [vercel.com](https://vercel.com)
2. Prihláste sa (môžete použiť GitHub účet)
3. Kliknite na **"Add New..."** → **"Project"**
4. Importujte váš GitHub repozitár
5. Vercel automaticky detekuje Nuxt 3:
   - Framework Preset: **Nuxt.js** ✅
   - Root Directory: **salon-demo** (ak je v podpriečinku)
   - Build Command: `npm run build`
   - Output Directory: `.output/public`
6. Kliknite **"Deploy"**
7. Počkajte 2-3 minúty
8. **Hotovo!** 🎉

#### Varianta B: Cez Vercel CLI (Pre pokročilých)

```bash
# Nainštalovať Vercel CLI
npm install -g vercel

# Prihlásiť sa
vercel login

# Deploy
vercel

# Pre produkčný deployment
vercel --prod
```

## 📝 Pred deploymentom - Checklist

### ✅ Povinné úpravy

- [ ] **Kontaktné údaje** - `components/ContactSection.vue`, `components/Footer.vue`
- [ ] **Telefón a email** - Nahraďte všetky výskyty `+421 901 234 567` a `info@salonelegance.sk`
- [ ] **Názov salónu** - `nuxt.config.ts`, všetky komponenty
- [ ] **Adresa** - `components/ContactSection.vue`, `components/Footer.vue`
- [ ] **Otváracie hodiny** - `components/ContactSection.vue`
- [ ] **Služby a ceny** - `components/ServicesSection.vue`
- [ ] **Google Maps** - `components/ContactSection.vue` (nahraďte iframe src vašou adresou)

### 🎨 Odporúčané úpravy

- [ ] **Obrázky** - Nahraďte Unsplash linky vašimi fotografiami
- [ ] **Logo** - Pridajte vlastné logo do `public/logo.svg`
- [ ] **Favicon** - Nahraďte `public/favicon.svg`
- [ ] **Farby** - Upravte farby v `tailwind.config.js`
- [ ] **Galéria** - Pridajte vlastné fotografie do `components/GallerySection.vue`
- [ ] **Referencie** - Aktualizujte `components/TestimonialsSection.vue`

### 🔧 Technické nastavenia

- [ ] **Vlastná doména** - Nastavte v Vercel Dashboard
- [ ] **Environment Variables** - Ak používate API (Vercel → Settings → Environment Variables)
- [ ] **Analytics** - Google Analytics, Facebook Pixel (voliteľné)
- [ ] **SEO** - Meta descriptions, Open Graph images

## 🌐 Nastavenie vlastnej domény

1. V Vercel Dashboard kliknite na váš projekt
2. Prejdite na **Settings** → **Domains**
3. Pridajte vašu doménu (napr. `www.vasesalon.sk`)
4. Vercel vám poskytne DNS záznamy
5. Pridajte tieto záznamy do vášho DNS providera:

```
Type: A
Name: @
Value: 76.76.21.21

Type: CNAME
Name: www
Value: cname.vercel-dns.com
```

6. Počkajte 24-48 hodín na propagáciu DNS
7. SSL certifikát sa nastaví automaticky ✅

## 🔄 Automatické deploymenty

Po prvom deploymenti:
- Každý **push do main** vetvy = automatický deployment
- Pull requesty vytvárajú **preview deployments**
- Žiadna manuálna práca potrebná!

## 📧 Nastavenie rezervačného systému

### Možnosť 1: EmailJS (Zadarmo, jednoduché)

1. Vytvorte účet na [emailjs.com](https://www.emailjs.com/)
2. Vytvorte email službu a template
3. Získajte: Service ID, Template ID, Public Key
4. V Vercel → Settings → Environment Variables pridajte:
   ```
   NUXT_PUBLIC_EMAIL_SERVICE_ID=your_service_id
   NUXT_PUBLIC_EMAIL_TEMPLATE_ID=your_template_id
   NUXT_PUBLIC_EMAIL_PUBLIC_KEY=your_public_key
   ```
5. Aktualizujte `components/BookingForm.vue`

### Možnosť 2: Formspree (Najjednoduchšie)

1. Vytvorte účet na [formspree.io](https://formspree.io/)
2. Vytvorte nový formulár
3. Získajte Form ID
4. Upravte form action v `components/BookingForm.vue`:
   ```vue
   <form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```

### Možnosť 3: Vlastné API

Vytvorte `server/api/booking.post.ts`:

```typescript
export default defineEventHandler(async (event) => {
  const body = await readBody(event)
  
  // Tu môžete:
  // - Poslať email
  // - Uložiť do databázy
  // - Integrovať s kalendárom
  
  return { success: true, message: 'Rezervácia prijatá' }
})
```

## 🔍 SEO Optimalizácia

### Google Search Console

1. Navštívte [search.google.com/search-console](https://search.google.com/search-console)
2. Pridajte vašu stránku
3. Overte vlastníctvo (Vercel to uľahčuje)
4. Odošlite sitemap: `https://vasadomena.sk/sitemap.xml`

### Google Analytics

1. Vytvorte účet na [analytics.google.com](https://analytics.google.com)
2. Získajte Measurement ID (G-XXXXXXXXXX)
3. Pridajte do Vercel Environment Variables:
   ```
   NUXT_PUBLIC_GOOGLE_ANALYTICS_ID=G-XXXXXXXXXX
   ```
4. Pridajte do `nuxt.config.ts`:
   ```typescript
   app: {
     head: {
       script: [
         {
           src: `https://www.googletagmanager.com/gtag/js?id=${process.env.NUXT_PUBLIC_GOOGLE_ANALYTICS_ID}`,
           async: true
         }
       ]
     }
   }
   ```

## 🐛 Riešenie problémov

### Build Error: "Cannot find module"

```bash
rm -rf node_modules package-lock.json
npm install
```

### Stránka sa nenačíta po deploymenti

- Skontrolujte Vercel logs: Deployment → View Function Logs
- Overte, či sú všetky dependencies v `package.json`

### Obrázky sa nezobrazujú

- Použite relatívne cesty alebo cesty z `public/` priečinka
- Pre externé obrázky: pridajte do `nuxt.config.ts`:
  ```typescript
  nitro: {
    prerender: {
      crawlLinks: true
    }
  }
  ```

### 404 Error pri navegácii

Vercel automaticky podporuje Nuxt routing, ale skontrolujte:
- `pages/` priečinok obsahuje všetky potrebné súbory
- Názvy súborov sú správne (kebab-case)

## 📊 Monitoring a Analytics

### Vercel Analytics

Automaticky dostupné v Vercel Dashboard:
- Page views
- Unique visitors
- Performance metrics
- Geographic data

### Pridanie Google Analytics

1. V `nuxt.config.ts` pridajte do `head`:
```typescript
script: [
  {
    src: 'https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX',
    async: true
  },
  {
    innerHTML: `
      window.dataLayer = window.dataLayer || [];
      function gtag(){dataLayer.push(arguments);}
      gtag('js', new Date());
      gtag('config', 'G-XXXXXXXXXX');
    `
  }
]
```

## 🎉 Po úspešnom deploymenti

1. **Otestujte všetky funkcie**
   - Navigácia medzi stránkami
   - Rezervačný formulár
   - Responzívnosť na mobile
   - Všetky linky

2. **Zdieľajte vašu stránku**
   - Sociálne médiá
   - Google My Business
   - Vizitky

3. **Monitorujte výkon**
   - Vercel Analytics
   - Google Analytics
   - User feedback

---

**Potrebujete pomoc?** Vytvorte issue na GitHube alebo kontaktujte podporu.

**Všetko funguje?** Gratulujeme! 🎉 Máte profesionálnu webovú stránku! 🚀

