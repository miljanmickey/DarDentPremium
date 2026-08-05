# Dar Dent — sajt stomatološke ordinacije

Višejezični statični sajt (srpski, ruski, engleski) za ordinaciju **Dar Dent**, Milovana Glišića 3, Novi Sad.

Bez build procesa, bez zavisnosti, bez backend-a. Ceo sajt su dva dela: jedan HTML fajl i folder sa slikama.

## Struktura

```
index.html          ceo sajt — HTML, CSS i JavaScript u jednom fajlu
assets/             logo, favikon, fotografije
robots.txt          uputstvo pretraživačima
sitemap.xml         mapa sajta sa jezičkim verzijama
UPUTSTVO.md         detaljno objašnjenje za onoga ko održava sajt
```

## Pokretanje

Dupli klik na `index.html` i sajt radi. Nema šta da se instalira.

Jedina razlika u odnosu na pravi sajt: kad se otvara kao lokalni fajl, jezik se ne upisuje u adresu (pregledač to zabranjuje), i Google mapa u sekciji Kontakt zahteva internet.

Ako želiš lokalni server, dovoljno je bilo šta od ovoga:

```bash
python3 -m http.server 5173     # pa otvori http://localhost:5173
npx serve .
```

## Objavljivanje

Repozitorijum ima GitHub Actions workflow koji na svaki `push` na granu `main` objavljuje sajt na GitHub Pages.

1. **Settings → Pages → Source:** izaberi *GitHub Actions*.
2. Za sopstveni domen: **Settings → Pages → Custom domain**, pa u `index.html` i `sitemap.xml` zameni `https://www.dardent.rs` pravom adresom.

Sajt radi i na bilo kom običnom hostingu — dovoljno je iskopirati sadržaj repozitorijuma u `public_html`.

## Šta je u sajtu

- **Tri jezika** — prebacuje se u zaglavlju, bez ponovnog učitavanja, sa upisom u adresu (`?lang=ru`) da bi Google indeksirao svaku verziju
- **Usluge na dva nivoa** — sedam kartica sa oblastima, klik otvara akordeon sa svih 47 intervencija i objašnjenjem svake, prevedeno na sva tri jezika
- **Kontakt forma → WhatsApp** — ne šalje mejl i ne čuva podatke, otvara WhatsApp sa već sastavljenom porukom
- **SEO** — hreflang, Open Graph, `Dentist` schema podaci, sitemap sa jezičkim varijantama
- **Prilagođeno telefonima** — provereno od 320px naviše

## Održavanje

Sve izmene se rade u `index.html`. Najčešće tražene stvari:

| Šta menjaš | Gde |
|---|---|
| Tekstovi na bilo kom jeziku | objekat `I18N` |
| Nazivi i opisi intervencija | objekat `SERVICES` |
| WhatsApp broj | `WA_NUMBER` |
| Boje | CSS promenljive na vrhu `<style>` |
| Adresa i radno vreme | `addrVal`, `hoursVal` + JSON-LD u `<head>` |

Detaljnije, sa objašnjenjima zašto je nešto urađeno tako kako jeste, stoji u [UPUTSTVO.md](UPUTSTVO.md).

## Čeka podatke od klijenta

- ime, biografija i fotografija drugog stomatologa
- fotografije ordinacije (pet pripremljenih mesta u galeriji + polje u hero sekciji)
- potvrda da je prvi pregled besplatan
- tačne koordinate ordinacije za schema podatke
- vektorski original logotipa, ako postoji (`.ai`, `.eps`, `.svg`)

---

© Dar Dent. Sva prava zadržana.
