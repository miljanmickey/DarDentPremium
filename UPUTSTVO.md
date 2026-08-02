# Dar Dent — uputstvo za sajt

> **Gde je šta:** sajt je razdvojen u folder `src/`. Tekstovi su u `src/js/i18n.js`,
> usluge u `src/js/services.js`, stilovi u `src/css/styles.css`, slike u `src/assets/`.
> Posle svake izmene: `npm run check` proverava da ništa nije razbijeno, `npm run build`
> pravi verziju za objavljivanje. Tehnički detalji su u [README.md](README.md).

## Šta je urađeno

- **Jedan fajl `index.html`** — sav HTML, CSS i JS unutra, bez build procesa. Otvori duplim klikom ili okači na hosting.
- **Tri jezika** (SR / RU / EN) — prebacuje se dugmićima u zaglavlju, bez ponovnog učitavanja. Jezik se pamti i upisuje u URL (`?lang=ru`) da bi Google mogao da indeksira svaku verziju.
- **Originalni logo** — uzet je tvoj fajl i uklonjena mu je pozadina, pa se koristi 1:1. Isečen je na tri dela u koren sajta: `logo-full.png` (ceo logotip — hero i sekcija O ordinaciji), `logo-mark.png` (samo znak — zaglavlje i futer) i `logo-wordmark.png` (natpis Dar dent). Iz istog fajla su napravljeni favikon, ikonica za iPhone i slika za deljenje na mrežama.
- **Boje tačno po trećoj slici**: purpurna (transformacija, poverenje), svetloplava (čistoća, osmeh), bela pozadina, suptilni gradijenti bez jakih kontrasta.
- **Kontakt forma → WhatsApp** na `+381 64 1434895`. Ne šalje mejl i ne čuva podatke — otvara WhatsApp sa već sastavljenom porukom na jeziku koji je posetilac izabrao.

## Ako klijentkinja ima originalni fajl od dizajnera

Logo je izvučen iz JPG-a i za sajt je sasvim dovoljan. Ali ako postoji vektorski original (`.ai`, `.eps`, `.pdf` ili `.svg`), pošalji ga — zamena traje minut, a dobija se oštrina na svakom uvećanju i fajl manji desetak puta. Isto važi za belu verziju logotipa, ako je ima, za tamne podloge.

## Signature detalj: svetleći znak

Iz vašeg razgovora sam preuzeo ideju o **3D svetlećem znaku na fasadi**. Na sajtu je to dugme ispod logotipa („Uključi svetleći znak") — hero se prebacuje iz dnevnog u noćni režim, a logo se pali kao svetleća tabla sa purpurnim halom. Na desktopu se logo blago naginje za mišem, pa deluje 3D. To je jedini „efektan" element; sve ostalo je namerno mirno.

## Šta još treba od klijenta

| Šta | Gde u fajlu |
|---|---|
| Fotografije ordinacije i radova | sekcija `<section class="gallery">` — 5 pripremljenih mesta, samo se `<div class="shot">` zameni sa `<img src="foto.jpg" alt="...">` |
| Fotografija drugog stomatologa | `.doc-photo` u sekciji Tim (fotografija dr Vujović je već postavljena) |
| Ime i biografija drugog stomatologa | `dr [Ime Prezime]` + ključevi `bio2` u sva tri jezika |
| Radno vreme po danima | ključ `hoursVal` u `I18N` + `openingHoursSpecification` u JSON-LD |
| Pravi domen | zameni `https://www.dardent.rs/` svuda (canonical, hreflang, OG, sitemap) |

Kada stignu fotografije, ubacujem ih ja — dizajn se ne menja.

## Polje za sliku u hero sekciji

Desna strana prve ekranske slike je rezervisana za fotografiju — logo, naslov, dugmad i prekidač za svetleći znak su svi levo. Kad slika stigne, `<figure class="hero-photo">` se zameni sa:

```html
<figure class="hero-photo">
  <img src="hero.jpg" alt="Ordinacija Dar Dent" width="1200" height="1400">
</figure>
```

Najbolje radi uspravna fotografija (odnos otprilike 4:4,6) — enterijer ordinacije ili dr Vujović u radu. Na telefonu se polje samo prebacuje u vodoravni format ispod teksta.

## Ruski jezik i veličina slova

Cormorant ima nisku x-visinu, a ćirilica nema uzlazne poteze kao latinica, pa na istoj veličini deluje sitnije. Zato je uveden `--disp`: za srpski i engleski je 1, a za ruski 1,075, i množi sve naslove pisane serifom. Ako neko želi da fino podesi, menja se jedna linija u CSS-u:

```css
html[lang="ru"]{--disp:1.075}
```

U zaglavlju su ruske stavke menija skraćene („Процесс" umesto „Как мы работаем", „Записаться" umesto „Записаться на приём") jer su najduže, a meni prelazi na hamburger na 1080px.

## Usluge

Dva nivoa. Prvo sedam kartica sa oblastima — ikonica, naziv, kratak opis i broj intervencija. Klik na karticu skloni mrežu i otvori detaljan prikaz: zaglavlje oblasti sa uvodnom rečenicom, pa akordeon u kome je svaka intervencija zaseban red. Klik na red otvara objašnjenje šta se tačno radi i dugme koje šalje WhatsApp poruku sa već upisanim nazivom te intervencije. Dugme „Sve oblasti" vraća na kartice.

**Sve na tri jezika** — 47 naziva i 47 opisa, plus uvodne rečenice po oblasti. Promena jezika ponovo iscrtava i kartice i otvoreni detalj, tako da se ne gubi mesto gde je posetilac bio. Množina je rešena po pravilima svakog jezika (3 intervencije / 12 intervencija, 4 процедуры / 12 процедур).

**Svaka oblast ima svoju adresu**, pa se može direktno linkovati iz reklame, Instagram bio-a ili poruke:

```
dardent.rs/#protetika
dardent.rs/#oralna-hirurgija
dardent.rs/#decija-stomatologija
```
Ostale: `bolesti-zuba`, `estetika`, `ortodoncija`, `parodontologija`. Dugme „nazad" u pregledaču radi kako se očekuje.

**Opise treba da pregleda dr Vujović pre puštanja u rad.** Pisani su za pacijenta, ne za kolegu, i namerno izbegavaju žargon — ali su medicinski sadržaj i moraju da prođu njenu proveru. Svi stoje na jednom mestu, u `const SERVICES` na dnu fajla.

U padajućem meniju kontakt forme stoji sedam oblasti (ne 47 stavki) — pacijentu je lakše da izabere, a nama na WhatsApp stiže dovoljno informacije.

**Za proveru:** stavka *„Disekcija zuba"* bila je prekinuta na pola u spisku koji sam dobio, pa sam je dopunio kao „uklanjanje korenova zahvaćenih patološkim procesom kod višekorenih zuba".

## Adresa i mapa

Adresa **Milovana Glišića 4, Novi Sad** je uneta na svih pet mesta gde je bitna: u sekciji Kontakt, u futeru, u Google mapi, u `LocalBusiness` schema podacima i u naslovu i opisu stranice za Google. Na ruskom je ulica ostavljena latinicom (`Milovana Glišića 4, Нови-Сад`) namerno — tako ruski pacijent može da je iskopira u navigaciju bez greške.

**Jedno treba proveriti:** koordinate u JSON-LD-u (`45.2517, 19.8369`) su približne za taj deo Novog Sada. Tačne se dobiju tako što se u Google Maps klikne desnim tasterom na ordinaciju i izaberu koordinate, pa se zamene u `"geo"`. Nije kritično jer Google prvenstveno koristi tekstualnu adresu, ali je preciznije.

Ako se adresa ikad promeni, menja se `q=` u `<iframe src=...>`:

```
https://www.google.com/maps?q=Ulica+15,+Grad&z=16&hl=sr&output=embed
```

Isto tako i `query=` u dugmetu „Otvori navigaciju". Mapa se učitava tek kada posetilac doskroluje do nje (`loading="lazy"`), pa ne usporava sajt.

## Cene

Po dogovoru, cene se **ne prikazuju** na sajtu. U sekciji „Kako radimo" stoji da pacijent posle pregleda dobija plan terapije i cenu u pisanoj formi — to pokriva pitanje bez objavljivanja cenovnika.

## SEO — šta je već ugrađeno

- Title, meta description i keywords, **koji se menjaju sa jezikom**
- `hreflang` za sr/ru/en + `x-default`
- Open Graph i Twitter kartice (za lep prikaz linka na Facebook-u, Instagram-u, Viber-u)
- **Schema.org `Dentist`** — ime, telefon, adresa, radno vreme, oba lekara, katalog usluga. Ovo je ono što izvlači „rich result" u Google pretrazi i pomaže na Google Maps-u.
- **Schema.org `FAQPage`** — česta pitanja mogu da se prikažu direktno u rezultatima pretrage
- `robots.txt` i `sitemap.xml` sa jezičkim varijantama
- Semantički HTML (`header`, `main`, `section`, `article`), jedan `h1`, opisni `alt` tekstovi
- Brzo učitavanje: nema biblioteka, nema jQuery-ja, ikonice su inline SVG

### Posle postavljanja na hosting (obavezno)
1. Registruj sajt u **Google Search Console** i pošalji `sitemap.xml`.
2. Otvori **Google Business Profile** za ordinaciju (naziv, adresa, telefon — identično kao na sajtu). Za lokalnog stomatologa ovo donosi više posetilaca nego sam sajt.
3. Uključi **HTTPS** (besplatan sertifikat je standard kod svih hostinga).

## Animacije

Diskretne, kako si tražila: pojavljivanje sekcija pri skrolu, podizanje kartica na hover, pulsiranje WhatsApp dugmeta, sužavanje zaglavlja pri skrolu, 3D nagib logotipa. Sve se automatski gasi ako posetilac ima uključeno „smanji animacije" u sistemu.

## Sitnice

- Radi na mobilnom, tabletu i desktopu (testirano do 360px širine).
- Tastatura i čitači ekrana rade normalno — fokus je vidljiv, dugmad imaju labele.
- Fontovi: **Cormorant Garamond** (naslovi, prati elegantni serif iz logotipa) i **Manrope** (tekst). Oba imaju ćirilicu, pa ruska verzija izgleda isto tako dobro.

## Napomena o futeru

Futer je svetao, a ne tamnoljubičast kao u prvoj verziji: na tamnoj podlozi beli i svetloplavi delovi logotipa su se gubili, jer je pozadina logotipa providna. Ovako ceo sajt ostaje u beloj i lila gami iz brief-a.

## Telefoni

Sajt je proveren na širinama od 320px naviše. Ključne odluke:

- **Zaglavlje je najuže grlo** — logo, prekidač jezika i dugme menija moraju da stanu u jedan red. Zato se na 520px logo smanjuje, na 400px još malo, a ispod 345px se natpis „Dar dent" sklanja i ostaje samo znak. Meni prelazi na hamburger već na 1080px, jer su ruske stavke najduže.
- **Galerija na telefonu ide u jednu kolonu.** U dve kolone natpisi tipa „Oprema i tehnologija" nisu imali gde da stanu.
- **Sve što je na širem ekranu levo-desno** (dugme uz tekst u mapi, dugme uz napomenu u formi, futer) na telefonu se slaže jedno ispod drugog, a dugmad idu preko cele širine da bi bila laka za palac.
- **Duge reči se prelamaju** umesto da probiju okvir — bitno za ruski, gde su reči najduže.

Ako se dodaje nova stavka u meni ili duži tekst na dugme, vredi proveriti zaglavlje na 360px, jer tu ima najmanje vazduha.

## Pre prelaska na domen dardent.rs

Fotografije koje su sada na sajtu su **privremene, za prikaz klijentu**. Nisu snimljene u ovoj ordinaciji i ne smeju ostati na pravom domenu. Redom, sa imenima fajlova:

| Gde | Fajl | Čime se menja |
|---|---|---|
| Prvi ekran + galerija | `enterijer.jpg` | fotografija same ordinacije |
| Galerija — pre i posle | `pre-i-posle.jpg` | **obavezno njihov slučaj**, uz saglasnost pacijenta |
| Galerija — tim | `tim-na-radu.jpg` | fotografija dr Vujović i kolege u radu |
| Galerija — detalj | `detalj-prostora.jpg` | detalj njihovog prostora |
| Galerija — oprema | `oprema.jpg` | njihova oprema |

Nove slike zadržavaju ista imena fajlova i sve radi bez ijedne izmene u kodu. Ako imena budu drugačija, menjaju se na dva mesta u `index.html`: u `<figure class="hero-photo">` i u `<div class="gallery-grid">`.

Fotografija „pre i posle" je posebno osetljiva: postavljena u galeriju ordinacije tvrdi da je to njihov rad. Ako svog slučaja nema, bolje je izbaciti taj okvir nego ostaviti tuđi.

Uz to, pri prelasku na domen:

1. U `index.html` i `sitemap.xml` zameniti `https://www.dardent.rs` stvarnom adresom, ako se razlikuje.
2. Uneti tačne koordinate ordinacije u `"geo"` u JSON-LD.
3. Prijaviti sajt u Google Search Console i poslati `sitemap.xml`.
4. Otvoriti Google Business Profile sa istim nazivom, adresom i telefonom kao na sajtu.
