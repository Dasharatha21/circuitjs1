# CircuitJS1 -- Android Termux Offline Setup Guide

**Language:** Simple Hinglish\
**Purpose:** Android phone par Electronic Circuit Simulator chalana,
bina har baar internet ke.

------------------------------------------------------------------------

## 1. CircuitJS1 kya hai?

CircuitJS1 ek electronic circuit simulator hai. Isme aap virtual circuit
bana kar experiment kar sakte ho.

Aap isme: - Resistor aur capacitor - Battery aur voltage source - Diode
aur LED - Transistor - AC/DC circuits - Current aur voltage ka flow

jaise experiments kar sakte ho.

**Important:** Ye normal Android APK nahi hai. Hum ise Termux ke through
phone par local website ki tarah chalayenge. Aap Chrome browser mein
simulator open karoge.

## 2. Kya-kya chahiye?

-   Android phone
-   Termux app
-   Internet connection (sirf pehli baar setup aur files download/build
    karne ke liye)
-   Thodi storage space
-   Chrome ya koi modern browser

> Termux ko trusted source se install karein. F-Droid ya official Termux
> GitHub releases use karein. Alag-alag sources ke Termux plugins ko mix
> na karein.

## 3. Pehli baar Termux setup

Termux open karein. Neeche diye gaye commands ko ek-ek karke copy-paste
karein.

### Step 1: Termux packages update karein

``` bash
pkg update && pkg upgrade -y
```

Agar permission ya confirmation pooche, instructions follow karein.

### Step 2: Zaroori tools install karein

``` bash
pkg install git nodejs python -y
```

Inka simple meaning:

  Tool            Kaam
  --------------- -----------------------------------------------------
  Git             GitHub se project download karna
  Node.js / npm   Project ki required files aur build process chalana
  Python          Phone par local web server chalana

### Step 3: Projects ke liye folder banayein

``` bash
mkdir -p ~/projects
```

`~/projects` Termux ke private folder ke andar hai. Yahan Linux tools ko
files aur links banane ki permission milti hai.

**Important:** Project ko Android ke `Download` folder mein build mat
karein. Shared storage mein kuch Linux permissions, jaise symbolic
links, properly kaam nahi karti. Isi wajah se npm mein `EACCES` error aa
sakta hai.

## 4. CircuitJS1 download karein

``` bash
cd ~/projects
git clone https://github.com/pfalstad/circuitjs1.git
```

Download complete hone ke baad:

``` bash
cd ~/projects/circuitjs1/ts
```

## 5. Required files install karein

``` bash
npm install
```

Ye command project ko chalane/build karne ke liye required packages
download karti hai.

Pehli baar is step ke liye internet chahiye.

Agar `npm install` ke baad vulnerabilities ya funding warnings dikhein,
iska matlab zaroori nahi ki installation fail hua. `npm ERR!` ya failed
command aaye toh uska output check karein. Bina samjhe
`npm audit fix --force` mat chalayein.

## 6. Simulator build karein

Isi folder mein ye command chalayein:

``` bash
npm run build
```

Build complete hone par output mein `✓ built` dikh sakta hai.

Build files yahan banti hain:

``` text
~/projects/circuitjs1/ts/dist
```

Aapke build mein entry page `circuitjs.html` hai.

> Build ke waqt kuch warnings aa sakti hain. Agar command successful ho
> aur `dist/circuitjs.html` ban jaye, toh pehle simulator test karein.
> Har warning ka matlab failure nahi hota.

## 7. Simulator start kaise karein?

Jab bhi simulator chalana ho, Termux open karke ye commands run karein:

### Step 1: Website files ke folder mein jaayein

``` bash
cd ~/projects/circuitjs1/ts/dist
```

### Step 2: Local server start karein

``` bash
python -m http.server 8000
```

Ab Termux mein server chalta rahega. Jis terminal mein server chal raha
hai, use band na karein.

### Step 3: Chrome mein simulator kholein

Chrome ke address bar mein ye address type karein:

``` text
http://127.0.0.1:8000/circuitjs.html
```

Ye address sirf isi phone par open hota hai. Ye public internet website
nahi hai.

## 8. Simulator band kaise karein?

Termux mein jis terminal par server chal raha hai, wahan:

1.  `CTRL` key dabayein.
2.  Saath mein `C` dabayein.

Server band ho jayega. Termux ko baad mein close kar sakte hain.

## 9. Terminal band ho gaya? Dobara kaise start karein?

Koi problem nahi. Build dobara karne ki zaroorat nahi hai.

Termux open karein aur bas ye do commands chalayein:

``` bash
cd ~/projects/circuitjs1/ts/dist
python -m http.server 8000
```

Phir Chrome mein:

``` text
http://127.0.0.1:8000/circuitjs.html
```

## 10. Agar Port 8000 already in use error aaye

Iska matlab port 8000 par koi doosra server pehle se chal raha hai.

Aap doosra port use kar sakte hain:

``` bash
python -m http.server 8080
```

Chrome mein ye open karein:

``` text
http://127.0.0.1:8080/circuitjs.html
```

## 11. Internet ke bina kaise chalega?

Pehli baar: - GitHub se source download karna hoga. - `npm install` se
packages download honge. - `npm run build` se website files banengi.

Ye sab complete hone ke baad: 1. Internet OFF karein. 2. Termux mein
local server start karein. 3. Chrome mein
`http://127.0.0.1:8000/circuitjs.html` open karein.

Agar page pehle se open hai, toh offline test ke liye reload bhi karke
dekhein.

**Note:** Local files phone mein rehni chahiye. App data clear ya
project delete karne se setup dobara karna pad sakta hai.

## 12. Common problems aur solutions

  -----------------------------------------------------------------------
  Problem                             Kya karein
  ----------------------------------- -----------------------------------
  `EACCES` / symlink error            Project ko `~/projects/` mein
                                      rakhein, Download folder mein nahi

  `npm: command not found`            `pkg install nodejs -y`

  `python: command not found`         `pkg install python -y`

  `git: command not found`            `pkg install git -y`

  `tsc: not found`                    Project ke `ts` folder mein
                                      `npm install` dobara successful
                                      karein

  Port already in use                 Port `8080` use karein

  Page not found                      `dist` folder aur `circuitjs.html`
                                      file check karein

  Chrome page nahi khol raha          Check karein ki Termux server abhi
                                      bhi chal raha hai
  -----------------------------------------------------------------------

## 13. Useful commands

**Project folder mein jaana:**

``` bash
cd ~/projects/circuitjs1
```

**Build folder dekhna:**

``` bash
ls ~/projects/circuitjs1/ts/dist
```

**Server start karna:**

``` bash
cd ~/projects/circuitjs1/ts/dist
python -m http.server 8000
```

**Server stop karna:** `CTRL + C`

------------------------------------------------------------------------

## 14. Important safety aur usage tips

-   GitHub se project sirf trusted official repository se download
    karein.
-   Random commands ko bina samjhe Termux mein paste na karein.
-   `rm -rf` jaise delete commands carefully use karein.
-   Termux ka data clear karne se project aur installed packages delete
    ho sakte hain.
-   Android battery settings mein Termux ko background mein run karne ki
    permission deni pad sakti hai.
-   Phone ki RAM kam ho toh ek waqt mein bahut saare browser tabs na
    kholein.

## 15. Official project

-   GitHub: https://github.com/pfalstad/circuitjs1
-   Local simulator address: http://127.0.0.1:8000/circuitjs.html

**Short reminder:** Har baar simulator chalane ke liye bas:

``` bash
cd ~/projects/circuitjs1/ts/dist
python -m http.server 8000
```

Aur Chrome mein `http://127.0.0.1:8000/circuitjs.html` open karein.
