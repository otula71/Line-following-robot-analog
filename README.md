# A line following robot

Robotek na experimentální DPS, který sleduje čáru a zastaví před překážkou &mdash; dle zadání na zápočet do Robotiky a automatizace. Postaven na Arduino Nano, řadiči motorů TB6612FNG, používá 5 IR čidel TCRT5000, UZ čidlo HC SR-04, 6V motorky N20, 2 trimry pro ladění parametrů a 2 LED (modrou a červenou) pro signalizaci různých stavů. Dále je připojeno tlačítko a 2 spínače. Jeden spínač pro napájení digitální části, druhý spínač pro napájení motorků (Toshiba v dokumentaci k TB6612 píše, že nikdy nemá být připojeno napájení motorků dříve, než je pod napětím digitální část). Tlačítko slouží pro spuštění/zastavení jízdy.

Čidla jsou čtena <strong>analogově</strong>, senzory díky tomu dokážou načítat hodnoty celkem hezky průběžně, ne skokově, jak je tomu u digitálního čtení, je ale tím pádem potřeba před jízdou dělat kalibraci senzorů. Ta naběhne automaticky po zapnutí, stačí autíčko postavit někam k čáře, případně &ndash; pokud není zapnuto napájení motorů &ndash; s ním ručně pohybovat senzory nad čarou. Já mám zakoupeny moduly, které mají pouze digitální výstup, takže byla potřeba malá úprava:

<img src="https://raw.githubusercontent.com/otula71/KRAA1-line-following-robot-analog/main/analog-out.jpg" alt="analog data" width="450" />

Pro řízení využívá proporcionálně-integračně-derivační algoritmus, ale je možno použít i jednoduchý algoritmus kačena, stačí odkomentovat Kačenu v <code>setup.h</code> a místo <code>jedeme_s_PID</code> se použije <code>jedeme_stupid</code>. Pomocí trimrů je možno si nastavovat, co je potřeba, a po doladění je možno jejich použití úplně zrušit.

Z důvodu, že jsem napíchnul ultrazvukový senzor na RX pin, je zablokováno jeho použití v ladicím režimu, protože už to tak mám vyleptáno na DPS, ale není problém připojit ho na D3, který jsem plánoval pro servomotorek a zůstal volný...

Schéma vypadá nějak takto:
![schéma](https://raw.githubusercontent.com/otula71/KRAA1-line-following-robot-analog/main/auticko_schema.png)

Součástky:

<ul>
<li><a href="https://www.aliexpress.com/item/1005002524993718.html">motor s úchytem a kolem</a></li>
<li><a href="https://www.aliexpress.com/item/32465698640.html">H-můstek TB6612FNG</a></li>
<li><a href="https://www.aliexpress.com/item/32465698640.html">H-můstek TB6612FNG</a></li>
<li>čidla s TCRT5000 &ndash; najděte si taková, co mají analogový výstup nebo jsou rovno na jedné liště</li>
<li>Arduino Nano, UZ modul HC SR-04, tlačítko, 2 spínače&hellip;</li>
<li>Držák na 2 lithiovky a ty baterky k tomu. Já používám 18650, ale pokud máte 14500, ušetříte na hmotnosti a vejdou se vám do držáku na AA.</li>
</ul>
