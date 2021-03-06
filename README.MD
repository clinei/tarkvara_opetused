##### Julgustav eelsõna
Käesolevas juhendis on asju millest ei pruugi kohe aru saada.
Sel juhul soovitan lugeda eelnevat teksti uuesti
ning kui see ei aita siis lihtsalt jätkake lugemist.

Eeldan, et omate mingit inglise keele oskust ja olete installinud Visual Studio ja avanud uue projekti.

## Mis on tarkvara arendus?
Tarkvara võimaldab meil simuleerida olukordi.

Programmeerides määrame algse olukorra ning millal ja kuidas see muutub.

Kujutame ette olukorda, kus ärkate mingis kõhedas ruumis ning soovite sealt lahkuda, kuid uks on lukus ja võtit teil pole.

Kirjeldame seda järgneva koodiga: 
```csharp
        static void Main(string[] args)
        {
            bool uksLukus = true;
            bool votiOlemas = false;
        }
```

Algne olukord on siis ukse lukus olemine ja võtme puudumine.

Oletame, et te ei lõpeta enne kui olete ukse lahti saanud.

Seda kirjeldame while tsükliga:
```csharp
        static void Main(string[] args)
        {
            bool uksLukus = true;
            bool votiOlemas = false;

            while (uksLukus)
            {
                // proovime ust lahti saada
            }
        }
```

(kahe kaldkriipsuga rida ära kirjuta, see on kommentaar mis selgitab ümbritsevat koodi)

Nüüd ütleme, et vaatate toas ringi ja leiate lähedalolevalt laualt võtme, 
avate sellega ukse ning põgenete.

Oleku muutused on siis võtme laualt võtmine ning ukse avamine:
```csharp
        static void Main(string[] args)
        {
            bool uksLukus = true;
            bool votiOlemas = false;
            
            while (uksLukus)
            {
                votiOlemas = true;

                uksLukus = false;
            }

            Console.WriteLine("Põgenesid!");
            Console.ReadKey();
        }
```

Te olete aga mõtlev ja otsustav olend ning programm võiks seda peegeldada.

Selleks peab programm esitama võimalikud valikud:
```csharp
Console.WriteLine("Mis teed?");

Console.WriteLine("V: Võtan laualt võtme");
Console.WriteLine("U: Teen ukse lahti");
```

peate saama vastata:
```csharp
valik = Console.ReadKey(true).KeyChar.ToString().ToUpper();
```

programm peab vastusest aru saama:
```csharp
if (valik == "V")
{
    votiOlemas = true;
}
else if (valik == "U")
{
    uksLukus = false;
}
```
ja meid tulemusest teatama:

```csharp
if (valik == "V")
{
    votiOlemas = true;

    Console.WriteLine("Võtsid laualt võtme");  // uus
}
else if (valik == "U")
{
    uksLukus = false;

    Console.WriteLine("Tegid ukse lahti");  // uus
}
```

Lisame uue muutuja `valik` algsesse olukorda:
```csharp
bool uksLukus = true;
bool votiOlemas = false;

string valik = "";  // uus

while (uksLukus)
```

Kood peaks praegu välja nägema selline:
```csharp
        static void Main(string[] args)
        {
            bool uksLukus = true;
            bool votiOlemas = false;

            string valik = "";
            
            while (uksLukus)
            {
                Console.WriteLine("Mis teed?");

                Console.WriteLine("V: Võtan laualt võtme");
                Console.WriteLine("U: Teen ukse lahti");

                valik = Console.ReadKey(true).KeyChar.ToString().ToUpper();

                if (valik == "V")
                {
                    votiOlemas = true;

                    Console.WriteLine("Võtsid laualt võtme");
                }
                else if (valik == "U")
                {
                    uksLukus = false;

                    Console.WriteLine("Tegid ukse lahti");
                }
            }

            Console.WriteLine("Põgenesid!");
            Console.ReadKey();
        }
```

Vajutades klahvi **F5** saate proovida **V** ja **U** tähtede vajutamist.

Olukorrad ei muutu aga niisama, vaid ainult teatud tingimustel.

Ukse lahti saamiseks on meil vaja võtit.

Selleks muudame olemasolevat koodi:
```csharp
else if (valik == "U")
{
    if (votiOlemas)
    {
        uksLukus = false;

        Console.WriteLine("Tegid ukse lahti");
    }
    else
    {
        Console.WriteLine("Uks on lukus");
    }
}
```

Kuna võtit saab võtta ainult siis kui see on veel laual, muudame valikute esitamise koodi:
```csharp
Console.WriteLine("Mis teed?");

if (votiOlemas == false)
{
    Console.WriteLine("V: Võtan laualt võtme");
}

Console.WriteLine("U: Teen ukse lahti");
```

ning valikute töötlemise koodi:
```csharp
if (valik == "V")
{
    // eitus, ehk sama mis "if (votiOlemas == false)"
    if (!votiOlemas)
    {
        votiOlemas = true;

        Console.WriteLine("Võtsid laualt võtme");
    }
    else
    {
        Console.WriteLine("Laual pole enam võtit");
    }
}
```


Nüüd peaks kood välja nägema nii:
```csharp
        static void Main(string[] args)
        {
            bool uksLukus = true;
            bool votiOlemas = false;

            string valik = "";

            while (uksLukus)
            {
                Console.WriteLine("Mis teed?");

                if (!votiOlemas)
                {
                    Console.WriteLine("V: Võtan laualt võtme");
                }

                Console.WriteLine("U: Teen ukse lahti");

                valik = Console.ReadKey(true).KeyChar.ToString().ToUpper();

                if (valik == "V")
                {
                    if (!votiOlemas)
                    {
                        votiOlemas = true;

                        Console.WriteLine("Võtsid laualt võtme");
                    }
                    else
                    {
                    	Console.WriteLine("Laual pole enam võtit");
                    }
                }
                else if (valik == "U")
                {
                    if (votiOlemas)
                    {
                        uksLukus = false;

                        Console.WriteLine("Tegid ukse lahti");
                    }
                    else
                    {
                        Console.WriteLine("Uks on lukus");
                    }
                }
            }

            Console.WriteLine("Põgenesid!");
            Console.ReadKey();
        }
```

## Edasi arendamise võimalused
Nagu alguses mainitud, võimaldab tarkvara simuleerida olukordi.

Olekumuutused sõltuvad reaalelus lugematul hulgal asjadest.

Tarkvara arendajatena on meie ülesanne üldistada seda soovitud täpsusastmele.

Siiani loodud programmi saame täiendada näiteks järgmistel viisidel:

Võtit saab laualt võtta alles siis kui on ringi vaadatud (uus tegevus, algne olukord ning tingimus)

Loetavust saab parandada eristades valikute esitamist, sisendi küsimist ning tulemusest teavitamist. Seda saab teha tähemärkidega fraasi alguses (`+++ Mis teed?`, `### Uks on lukus`) või neid tühjade ridadega eraldades, asetades `Console.WriteLine()` vastavatesse kohtadesse.

Võimalikud valikud sõltuvad asukohast.

Asukoha vahetus on üks valikutest.

Uus algne olukord:
```csharp
string asukoht = "algus";
```

Uued tegevused:
```csharp
if (valik == "U")
{
    asukoht = "uks";
}
```

Asukohad on algus, uks ja laud.

Algusest saab minna ukse või laua juurde.

Ukse juurest saab minna laua juurde ning vastupidi.

Algusesse tagasi minna pole vaja.

Soovitus: kohe peale 
```csharp
while (uksLukus)
{
```

pane
```csharp
    if (asukoht == "algus")
```

ning ümbritse ülejäänud kood loogeliste sulgudega.

Uue asukoha eristamiseks lisa peale olemasolevat koodi `else if` kus võrdled praegust asukohta valikus määratud asukohaga.

Peale seda kopeeri eelneva asukoha kood ning kohanda esitatavad valikud ja nende tulemused.

Kui hätta jääd, võid vaadata rohkem edasi arendatud ja inglisekeelset versiooni [siit](https://github.com/clinei/tpt_kodutood/blob/master/02_choice_game/02_choice_game/Program.cs).

Jõudu!
