https://terokarvinen.com/loota/zei4s/shctf-2026.zip
https://app.terokarvinen.com/lippu/game/16/submit

cd ~/Downloads
esim: strings passtr (passtr=tiedoston nimi)
strings packd | grep -Ei "password|flag|yes|sorry"
packd= tiedoston nimi

# CTF – muistiinpanot

## 1. Uusi tiedosto / ohjelma

Kun saan uuden tiedoston, aloitan aina:

pwd

ls -la

file TIEDOSTO

Jos tiedosto on ohjelma:

chmod +x TIEDOSTO
./TIEDOSTO

Sen jälkeen:

strings TIEDOSTO

Jos haluan etsiä heti jotain kiinnostavaa:

strings TIEDOSTO | grep -Ei "flag|password|pass|secret|key"

2. Jos ohjelma kysyy salasanaa

Kokeilen ensin ohjelmaa normaalisti:

./TIEDOSTO

Jos salasanaa ei löydy strings-komennolla, avaan ohjelman Ghidrassa.

Ghidra:

Import binary
Analyze
Functions
main
Decompiler

Etsi erityisesti:

strcmp
strncmp
memcmp
scanf
fgets
password
flag
secret

Esimerkiksi:

strcmp(input, "password1")

→ oikea salasana on password1.

3. Ghidra – main

Ensimmäinen paikka, jota tutkin, on main.

Jos Decompiler näyttää esimerkiksi:

int compareResult;
char password[32];

scanf("%31s", password);

compareResult = strcmp(password, "piilos-AnAnAs");

if (compareResult == 0) {
    puts("Yes!");
}

Tässä:

password = käyttäjän syöttämä salasana
strcmp = vertaa kahta merkkijonoa
compareResult == 0 = merkkijonot ovat samat

→ oikea salasana on piilos-AnAnAs.

4. Ghidra – muuttujien nimet

Decompiler voi näyttää esimerkiksi:

int iVar1;
char local_28[32];

Muuta nimet helpommiksi:

iVar1 → compareResult
local_28 → password

Ghidrassa:

Right click → Rename Variable

strings

strings on aina hyvä ensimmäinen testi.

strings TIEDOSTO

Tietty sana:

strings TIEDOSTO | grep "password"

FLAG:

strings TIEDOSTO | grep -Ei "flag"

Useita:

strings TIEDOSTO | grep -Ei "flag|password|secret"

UPX / pakattu ohjelma

Jos ohjelma näyttää pakatulta, tarkista UPX:

upx -l TIEDOSTO

Tee ensin kopio:

cp TIEDOSTO TIEDOSTO.packed

Pura:

upx -d TIEDOSTO

Sen jälkeen:

strings TIEDOSTO

GDB – perus

Jos Ghidra ei riitä:

gdb ./TIEDOSTO

Aseta breakpoint main-funktioon:

break main

Aja:

run

Tai lyhyesti:

b main
r

strings challenge | grep "password"

strings challenge | grep "FLAG"

strings challenge | grep -Ei "flag|password|secret"

gdb ./challenge

disassemble main
break main
run


## cd /home/elena/Downloads/ghidra_11.1.2_PUBLIC
./ghidraRun
