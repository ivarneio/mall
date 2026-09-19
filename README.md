# maja-mall

Tühi luu ühe lehe jaoks: katus, kolm ust, kolm tuba, paketid, jalg.

See repo on **template**. Siia ei panda kliendi nime, telefoni, pilte ega teenusenimesid (ärä «õhupallid», «glitter»). Nahk tuleb alles koopiasse.

Kui muudad seda repot, muudad kõiki tulevasi maju. Ära tee seda kliendi pärast.

---

## Mis on lukus (ära muuda koopias)

- `index.html` — käitumine. Uks, tuba, galerii, paketiriba, paketi lõpus teised paketid, keeled, kleepuv katus, kleepuv jalg.
- Galerii käitumine on kõigil tubadel sama. Teema toob ainult pildifailid.
- Ülemises reas on alati **kolm ust**. Neljandat ust mallis ei ole.
- Allkorrusel on **ainult paketid**. Kingitused / neljas tuba ei kuulu malli. See lisatakse alles konkreetses majas, kui vaja.
- Jalg on alati näha. Broneerimise tekst elab jalas, mitte toas.

Kui käitumine peab muutuma (uus galerii, neljas uks kõigile), muuda **seda** repot ja tõsta muudatus koopiatesse. Ära hakka ühe kliendi `index.html` omaks.

---

## Mis on lahti (muuda ainult koopias)

| Fail | Mis |
|---|---|
| `maja.json` | Nimi, slogan, keeled, sotsiaalmeedia URL-id, jala tekst, telefon, email, millised kolm kausta on uksed |
| `toad/teenus-1/tuba.json` | Esimese ukse pealkiri, jutt, pildinimede nimekiri |
| `toad/teenus-2/tuba.json` | Teine tuba |
| `toad/teenus-3/tuba.json` | Kolmas tuba |
| `toad/teenus-*/pildid või failinimed tuba.json sees` | Galerii |
| `paketid/paketid.json` | Pakettide tekst, hind, väike pilt, seos tubadega |

Uut tuba mallis ei lisata. Uus **pakett** = uus objekt `paketid.json` massiivis. Luu näitab ta ise teiste pakettide lõpus.

---

## Failipuu

```
index.html              LUKUS
README.md               see tekst
maja.json               maja silt
paketid/paketid.json    allkorrus
toad/teenus-1/tuba.json
toad/teenus-2/tuba.json
toad/teenus-3/tuba.json
```

Pildid toas: pane fail kausta `toad/teenus-1/` ja kirjuta nimi `pildid` massiivi, näiteks `"pildid": ["kass.jpg"]`. Luu otsib `toad/teenus-1/kass.jpg`.

Paketi väike pilt: tee `pilt` väärtuseks relatiivne tee, näiteks `"pilt": "paketid/pakett-1.jpg"`.

---

## maja.json

```json
{
  "pohikeel": "et",
  "keeled": ["et", "ru", "en"],
  "nimi": { "et": "", "ru": "", "en": "" },
  "slogan": { "et": "", "ru": "", "en": "" },
  "sotsiaal": { "facebook": "", "instagram": "" },
  "jalg": {
    "tekst": { "et": "", "ru": "", "en": "" },
    "telefon": "",
    "email": ""
  },
  "uksed": ["teenus-1", "teenus-2", "teenus-3"],
  "allkorrus_toad": []
}
```

- `pohikeel` on avakeel. Praegu `et`.
- `keeled` on nupud katuses. Ära võta `et` ära.
- `uksed` massiivi väärtused **peavad** olema täpselt kaustanimed `toad/` all.
- Tühi `facebook` / `instagram` / `telefon` / `email` = nuppu või linki ei näidata.
- `allkorrus_toad` on mallis tühi massiiv. Ära pane siia kingitusi. See väli on tuleviku konks, mitte Meelika nahk.

---

## tuba.json

```json
{
  "id": "teenus-1",
  "pealkiri": { "et": "Esimene teenus", "ru": "", "en": "" },
  "jutt": { "et": "", "ru": "", "en": "" },
  "pildid": []
}
```

- `id` = kaustanimi.
- Tühi `jutt` on lubatud.
- Tühi `pildid` on lubatud. Galerii lihtsalt ei ilmu.

---

## paketid.json

```json
{
  "paketid": [
    {
      "id": "pakett-1",
      "pilt": "",
      "pealkiri": { "et": "Pakett I", "ru": "", "en": "" },
      "kirjeldus": { "et": "", "ru": "", "en": "" },
      "meta": { "et": "", "ru": "", "en": "" },
      "hind": "",
      "toad": ["teenus-1", "teenus-2"]
    }
  ]
}
```

- `id` unikaalne.
- `toad` on viited ukse-id-dele. See ei ava tuba ise; see on sisu seos.
- Paketi vaates, kui kasutaja on kerinud paketi lõppu, luu joonistab **kõik teised** paketid. Seda nimekirja ei kirjutata käsitsi.

---

## Kuidas leht käitub (ära leiuta muud)

1. Avades: nimi, slogan, kolm ust, all paketiriba, all jalg.
2. Uks → tuba (pealkiri, jutt, galerii). Tagasi majja.
3. Paketiriba kaart → paketi sisu. Lõpus teised paketid. Tagasi majja.
4. Galerii pilt → suur vaade, sulgemine ristiga.
5. Katus ja jalg ei kao.
6. Keelenupp vahetab kõik `et|ru|en` väljad. Puuduva tõlke korral näidatakse `et`.

Ära ehita broneerimisvormi, poodi, kalendrit ega sisselogimist sellesse luusse. Jalg on tekst + tel + mail.

---

## Uus maja (koopia)

1. GitHub: selle repo juures **Use this template** (kui linnuke Template repository on sees) või kopeeri failid uude reposse.
2. Uus repo nimi on kliendi oma, näiteks `ohupalliloomad`.
3. **Ära** kirjuta kliendi andmeid tagasi `ivarneio/mall` sisse.
4. Koopias täida `maja.json`, kolm `tuba.json`, `paketid.json`, pane pildid.
5. Pages: Settings → Pages → Deploy from branch → `main` → `/ (root)`.
6. Kui vaja neljandat asja (kingitused), tee see **ainult koopias**: uus kaust `toad/...`, lisa id `maja.json` väljale `allkorrus_toad`. Mall jääb kolmeks toaks.

---

## Mida järgmine AI ei tohi teha

- Ära kirjuta `index.html` sisse kliendi lauseid.
- Ära nimeta mallis kaustu `pallid`, `glitter`, `kingitused`.
- Ära kopeeri Kahe Vahel / helivanni tekste ega tumedat rännaku nahka siia.
- Ära väida, et tühjad väljad on viga. Tühi on õige olek.
- Ära liida kahte maja ühte reposse.
- Ära muuda galerii loogikat ühe toa jaoks.

---

## Lühike tõde

Template = mootor.  
JSON + pildid = maja.  
Kolm tuba. Paketid all. Jalg paigal.  
Kliendi nimi tuleb alles koopias.
