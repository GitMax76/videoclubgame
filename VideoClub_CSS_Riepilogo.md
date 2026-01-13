
# VideoClub CSS – Riepilogo (tema Blockbuster + effetto VHS)

Questo file riassume le parti principali del CSS usate per ottenere una grafica “Blockbuster/VideoClub” e un overlay in stile VHS/CRT.

> Nota: i nomi delle classi fanno riferimento ai file HTML generati (Interactive Rulebook / Turn Simulator).

---

## 1) Variabili di tema (palette)

Definisci tutti i colori chiave in `:root` così puoi cambiare mood in 1 punto solo.

```css
:root {
  --blockbuster-blue: #003399;   /* Blu insegna */
  --blockbuster-yellow: #ffcc00; /* Giallo logo */
  --vhs-black: #1a1a1a;          /* Nero “plastica VHS” */
  --neon-pink: #ff00cc;          /* Accento neon */
  --text-white: #f0f0f0;         /* Testo chiaro */
  --lcd-green: #33ff00;          /* Log console tipo terminale */
}
```

---

## 2) Base layout (sfondo scuro + font retro)

- Usa un nero non puro (`--vhs-black`) per un effetto “materico”.
- Font monospace per feeling “terminale / POS anni ’90”.

```css
body {
  font-family: 'Courier New', Courier, monospace;
  background-color: var(--vhs-black);
  color: var(--text-white);
  margin: 0;
  line-height: 1.6;
}
```

---

## 3) Header Blockbuster (blu + giallo + bordo)

Ricrea il colpo d’occhio Blockbuster con:
- fascia blu,
- testo giallo,
- bordone giallo,
- ombra luminosa leggera.

```css
.header {
  background-color: var(--blockbuster-blue);
  color: var(--blockbuster-yellow);
  padding: 20px;
  text-align: center;
  border-bottom: 5px solid var(--blockbuster-yellow);
  text-transform: uppercase;
  box-shadow: 0 0 20px rgba(0, 51, 153, 0.5);
}
```

---

## 4) “Ticket Stub” (pattern diagonale + bordo tratteggiato)

Simula un biglietto/tessera usando:
- `repeating-linear-gradient` a 45° per le righe diagonali,
- `border: dashed` come “strappo”.

```css
.ticket-stub {
  background: repeating-linear-gradient(
    45deg,
    var(--blockbuster-blue),
    var(--blockbuster-blue) 10px,
    #002266 10px,
    #002266 20px
  );
  color: var(--blockbuster-yellow);
  padding: 10px;
  margin: 20px auto;
  max-width: 600px;
  text-align: center;
  border: 2px dashed var(--blockbuster-yellow);
  transform: rotate(-1deg);
}
```

---

## 5) “VHS Tape Card” (riquadro stile cassetta)

Per simulare la plastica della VHS:
- gradient verticale scuro,
- bordo sottile,
- label bianca sopra.

```css
.vhs-tape {
  background: linear-gradient(180deg, #111 0%, #333 50%, #111 100%);
  border-radius: 5px;
  padding: 15px;
  margin: 20px 0;
  border: 1px solid #444;
}

.vhs-label {
  background-color: white;
  color: black;
  padding: 5px 15px;
  border-radius: 2px;
  font-weight: bold;
  display: inline-block;
  transform: rotate(-0.5deg);
  box-shadow: 1px 1px 3px rgba(0,0,0,0.3);
  font-family: Arial, sans-serif;
}
```

---

## 6) Cards interattive (hover + “estrazione cassetta”)

Le sezioni cliccabili `.phase-card` danno feedback fisico:
- bordo laterale neon,
- spostamento laterale in hover.

```css
.phase-card {
  background-color: #2a2a2a;
  border-left: 5px solid var(--neon-pink);
  padding: 15px;
  margin-bottom: 15px;
  cursor: pointer;
  transition: transform 0.2s, background-color 0.2s;
}

.phase-card:hover {
  transform: translateX(10px);
  background-color: #333;
}

.phase-title {
  color: var(--neon-pink);
  font-weight: bold;
  font-size: 1.2em;
}

.hidden-content {
  display: none;
  padding: 10px;
  background: rgba(0,0,0,0.3);
  margin-top: 10px;
  border-left: 2px solid var(--blockbuster-yellow);
}
```

---

## 7) Overlay “Scanline” (effetto VHS/CRT sullo schermo)

È un layer semitrasparente che scorre dall’alto al basso:
- `position: absolute` + `pointer-events: none` per non bloccare i click,
- animazione lineare infinita.

```css
.scanline {
  width: 100%;
  height: 100px;
  background: linear-gradient(
    0deg,
    rgba(0,0,0,0) 0%,
    rgba(255,255,255,0.2) 50%,
    rgba(0,0,0,0) 100%
  );
  opacity: 0.1;
  position: absolute;
  bottom: 100%;
  animation: scanline 10s linear infinite;
  pointer-events: none;
}

@keyframes scanline {
  0%   { bottom: 100%; }
  100% { bottom: -100%; }
}
```

Suggerimento: per migliorarlo ulteriormente puoi aggiungere anche un overlay di “grain” (rumore) con un `background-image` a pattern oppure una texture PNG molto leggera.

---

## 8) Testo “CRT” (aberrazione cromatica + flicker)

Simula la sbavatura rosso/blu dei monitor CRT applicando ombre colorate che cambiano nel tempo.

```css
.crt-effect {
  animation: textShadow 1.6s infinite;
}

@keyframes textShadow {
  0% {
    text-shadow:
      0.4px 0 1px rgba(0,30,255,0.5),
     -0.4px 0 1px rgba(255,0,80,0.3),
      0 0 3px;
  }
  5% {
    text-shadow:
      2.8px 0 1px rgba(0,30,255,0.5),
     -2.8px 0 1px rgba(255,0,80,0.3),
      0 0 3px;
  }
  100% {
    text-shadow:
      0.4px 0 1px rgba(0,30,255,0.5),
     -0.4px 0 1px rgba(255,0,80,0.3),
      0 0 3px;
  }
}
```

Nota: nel file originale alcune “tappe” intermedie dell’animazione erano state abbreviate. Puoi aggiungerne 10–20 con valori casuali per un flicker più naturale.

---

## 9) (Simulator) Look “console”

Nel simulatore, la “console log” usa verde tipo terminale.

```css
.log-console {
  font-size: 0.8em;
  color: var(--lcd-green);
  background: #000;
  border: 1px solid #333;
  padding: 10px;
  height: 80px;
  overflow-y: auto;
}
```

---

## Checklist rapida

- Palette in `:root`
- Sfondo scuro + monospace
- Header blu/giallo con bordo
- Ticket stub a righe diagonali
- Cards “VHS plastic” + label bianca
- Hover laterale sulle sezioni
- Overlay scanline con animazione
- CRT text-shadow animato

