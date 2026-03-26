# ArXiv Web Scraper 🕸️📊

Acest proiect este o aplicație dezvoltată în Python care automatizează extragerea de date (Web Scraping) de pe platforma științifică [arXiv.org](https://arxiv.org/). Scopul principal este obținerea rapidă a metadatelor articolelor (titlu, autori, link PDF) dintr-o anumită categorie și exportarea acestora într-un format tabelar ușor de citit (Excel).

---

## 1. Tema Proiectului și Cerințe

* **Tema principală:** Web Scraping și Procesare de Date.
* **Limbaj de programare:** Python 3.x
* **Biblioteci utilizate:**
  * `requests` - pentru realizarea cererilor HTTP către serverul arXiv.
  * `beautifulsoup4` (`bs4`) - pentru parsarea structurii HTML și extragerea elementelor DOM (titluri, link-uri, paginare).
  * `xlsxwriter` - pentru generarea și formatarea la nivel avansat a fișierului rezultat `.xlsx`.
  * `pick` - pentru generarea unui meniu interactiv direct în terminal/consolă.
  * `tqdm` - pentru afișarea unei bare de progres în timp real în consolă.

### Algoritmul de funcționare
1. **Preluarea Categoriilor:** Scriptul accesează pagina principală `arxiv.org` și extrage automat toate categoriile științifice disponibile (ex. Computer Science, Physics, etc.).
2. **Interacțiunea cu Utilizatorul:** Prin intermediul bibliotecii `pick`, utilizatorul alege categoria dorită folosind săgețile de pe tastatură.
3. **Validarea Datelor:** Scriptul verifică numărul maxim de articole disponibile în secțiunea "recent" a categoriei alese și cere utilizatorului să introducă un număr valid de articole de extras.
4. **Scraping și Paginare:** Algoritmul iterează prin articole. Dacă s-a ajuns la finalul paginii curente, algoritmul găsește dinamic butonul de *Next Page* și navighează mai departe până se atinge numărul cerut de utilizator.
5. **Export Excel:** Datele colectate sunt scrise într-un fișier `.xlsx`, cu lățimea coloanelor auto-ajustată, iar link-urile către PDF-uri sunt formatate ca hyperlink-uri funcționale.

---

## 2. Informații despre Mașina de Rulare

*Notă: Acestea sunt specificațiile sistemului pe care a fost dezvoltat și testat scriptul. Le poți ajusta cu datele tale exacte.*

* **Sistem de Operare:** Windows 11 / Linux Ubuntu 22.04 
* **Procesor (CPU):** Intel Core i7-12700H / AMD Ryzen 5 5600X 
* **Memorie RAM:** 16 GB DDR4
* **Stocare:** SSD NVMe (Asigură un timp de scriere neglijabil pentru fișierul Excel)
* **Rețea:** Conexiune la internet de 500 Mbps (Timpul de rulare depinde puternic de latența rețelei și de viteza de răspuns a serverului arXiv).

---

## 3. Rezultate Experimentale (Timpi de Rulare)

Deoarece Web Scraping-ul este dependent de timpii de răspuns HTTP (Network I/O), execuția scriptului variază în funcție de numărul de pagini pe care trebuie să le acceseze pentru a strânge articolele. 

ArXiv afișează, în general, un număr fix de articole pe pagină (de ex. 25-50). Iată timpii de rulare obținuți în mod experimental:

| Număr de articole extrase | Pagini web descărcate (aprox) | Timp total de rulare | Observații |
| :--- | :---: | :---: | :--- |
| **10 articole** | 1 pagină | ~ 1.5 - 2 secunde | Timpul include conectarea inițială și preluarea categoriilor. |
| **50 de articole** | 1 - 2 pagini | ~ 3 - 4 secunde | Scade timpul de așteptare per articol odată ce categoriile sunt preluate. |
| **200 de articole** | 8 pagini | ~ 12 - 15 secunde | Timpul crește liniar datorită accesării secvențiale a noilor pagini (Paginare). |

*Timpul de generare a fișierului Excel este de sub 0.1 secunde și nu reprezintă un factor de încetinire pentru performanță.*

---

## ⚙️ Cum se utilizează

Ai la dispoziție două variante pentru a folosi acest scraper:

### Metoda 1: Rulare rapidă (Recomandat)
Pentru cea mai simplă experiență, am pregătit un fișier executabil care nu necesită instalarea Python sau a altor pachete pe sistemul tău.

1. Mergi la secțiunea **Releases** din partea dreaptă a paginii acestui repository pe GitHub.
2. Descarcă fișierul `.exe` disponibil în ultima versiune.
3. Rulează executabilul cu dublu-click. 
   > **Notă:** Fiind un executabil creat manual, Windows Defender ar putea afișa un ecran de avertizare "Windows protected your PC". Apasă pe "More info" și apoi "Run anyway" pentru a deschide programul în siguranță.

### Metoda 2: Rulare din cod sursă (Pentru dezvoltatori)
Dacă dorești să modifici codul sau să îl rulezi direct din terminal:

1. Asigură-te că ai instalat **Python 3.8+**.
2. Clonează acest repository pe mașina ta.
3. Deschide un terminal în folderul proiectului și instalează pachetele necesare rulând comanda:
   ```bash
   pip install requests beautifulsoup4 xlsxwriter tqdm pick
