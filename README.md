# Dopredný produkčný systém
Projekt z umelej inteligencie - Dopredný produkčný systém

# Zadanie
Produkčný systém na základe odvodzovacieho pravidla modus ponens (pravidlo 
odlúčenia) odvodzuje zo známych faktov a produkčných pravidiel nové fakty. Ak 
systém nemá dostatok vstupných údajov, môže klásť užívateľovi otázky. 
K funkčnému programu je potrebné pripojiť aj dokumentáciu s opisom 
konkrétneho riešenia (reprezentácia znalostí, algoritmus, špecifické vlastnosti) a 
zhodnotením činnosti vytvoreného systému. Systém musí správne pracovať aspoň 
nad prvou uvedenou (jednoduchou) bázou znalostí, bázu znalostí si musí systém 
vedieť načítať zo súboru. V tom prípade je tiež potrebné napísať do dokumentácie, 
ako by bolo možné systém rozšíriť. Je možné si vytvoriť aj vlastné bázy znalostí.

# Riešenie

```java
// Najde všetky aplikovateľné akcie 
for (Pravidlo prav : vsetkyPravidla) { 
 List<String[]> naviazania = new ArrayList<>(); 
 searching(prav.Nazov, prav.Podmienka, prav.Akcia, naviazania); 
} 
```

Funkcia searching, prehliadava postupne pre dané pravidlo, ktoré sa skladá z podmienky, 
tvorenej viacerými podpodmienkami. 
 
Takže na začiatku funkcie searching sa skontroluje koľko mám ešte aktuálnych podmienok, ak 
by už nebola ani jedna, úspešne sme získali všetky naviazania a môže vypísať akciu, ktorú má 
vykonať. Ak ešte máme nejakú podmienku tak ju ideme riešiť najskôr pozerám na prvý znak, ktorý 
môže byť v špecifických prípadoch (<>) a vtedy sa postupuje odlišným spôsobom, ak sa tento znak na 
začiatku podmienky nenachádza postupne prehľadáva všetky fakty, kým nenájde vyhovujúci fakt, 
ktorý sedí s konkrétnou podmienkou. To znamená, že vždy si rozdrobím fakt na slová (napr: Peter, je, 
rodic, Jano) a podobne aj podmienku(?X, je, rodic, ?Y) a kontrolujem slovo po slove ak navzájom 
vyhovujú a teda sú rovnaké v tom prípade som našiel správny fakt a snažím sa vytvoriť naviazanie 
medzi Peter->?X a Jano->?Y . Tieto naviazania kontrolujem s predošlými vytvorenými v danej 
podmienke (v prípade ,že nájde dve úplne rovnaké naviazania vymaže jedno z nich ako zbytočné 
a v prípade, že nájde naviazanie, ktoré protirečí predošlému zahodí celý fakt a rieši celú podmienku 
od začiatku a snaží sa nájsť iný fakt, ktorý by vyhovoval.) 
Ak úspešne nájde naviazania, zníži počet podpomienok a vracia sa na úplný začiatok, a tam 
zistí čí ešte má nejakú ďalšiu podpodmienku. 
