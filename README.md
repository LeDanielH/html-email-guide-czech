# JAK PSÁT HTML EMAIL

+ Zapomeňte slovo semantic a vše co víte o tradičním web designu. 
+ Cílem tohoto tutoriálu není vysvětlit specifika jednotlivých klientů, ale ukázat, co můžete použít ve všech.

----

### ZÁKLAD - TABULKY A NIC JINÉHO!
+ Nepoužívat "div" element pro wrapping, vytvořte další "table" a vždy uvnitř "td" elementu.

```html

    <table>
        <tr>
            <td>
                <table></table>
            </td>
        </tr>
    </table>
```

----

### HTML ELEMENTY, JAKÉ POUŽÍVAT A JAKÝM SE VYHNOUT
+ Nepoužívat block level elementy pro obsah tabulek: "div", "h1, h2...", "p". Nelze na ně aplikovat positioning přes "td" atributy(align, valign).
+ Text wrapujte do "span", není block level elementem, lze tedy na něj aplikovat positioning přes "td" atributy(align, valign).
+ "img" bývá wrapnut do "a" tagu, proto s ním lze manipulovat přes "td" attributy(align, valign). Vysvětleno níže v "USPOŘÁDÁNÍ ELEMENTŮ UVNITŘ TABULKY".
+ Maximálně využívat html elementů pro styling textu jako "strong", "small" a "em".

----

### STYLING - OBECNĚ
+ Nedávat styling do "head" (kromě specifických stylů pro email klienty, viz. základní kostra emailu na konci tohoto dokumentu).
+ Link k css stylům v "head" nepříchází v úvahu.
+ Všechny styly aplikujte inline a až po vyčerpání možností stylingu přes html element atributy. V HTML 5 se již s většinou těchto attributů nesetkáte (status "deprecated"), podle mé zkušenosti jsou však jedinou cestou, jak napsat html email kompatibilní se všemy emailovými klienty.
+ Inline style attribute používejte jen když je to opravdu nutné - například pro styling textu nebo pro změnu spacingu v "td" elementu.
+ Dle mých zkušeností -> nepoužívat následující css properties: "display", "position", "margin".
 
```html
       
    <!-- TYTO ATTRIBUTY I STYLE ATTRIBUTE BUDE MÍT KAŽDÝ "table" ELEMENT VE VAŠEM EMAIL TEMPLATE -->
    <table border="0" cellpadding="0" cellspacing="0" width="800" style="border-collapse: collapse;">
        <tr>
            <td align="center" valign="top">

                <!-- HEADING -->
                <span style="font-family: Arial, sans-serif; font-size: 20px;">
                    <em>THIS IS ITALIC <strong> BOLD TEXT</strong></em>    
                </span>
            </td>
            <td>
                <a href="#">
                    <img src="#" alt="image">
                </a>
            </td>
            <td>
                <small>This is 12px text</small>
            </td>
        </tr>
    </table>

```

----

### BARVA TABULKY
+ nepoužívejte zkratky jako #fff, ale #ffffff na všechny barvy, v outlooku mi to přes zkratku barvu ignoruje.
+ "background-color" aplikujte jen na "table" element přes "style" attribute a na "td" element "vždy"(pro jistotu) přes "bgcolor" attribute.

```html

    <table style="background-color: #ffffff;">
        <td bgcolor= "#dddddd"></td>
    </table>
``` 

----

### ROZMĚRY 
+ Doporučená šířka pro HTML email je 600px - současný trend. Maximum je 800px.
+ Používejte raději width="800" attribute než style="width: 800px";.
+ Pokud definujete výšku elementu přes style attribute, místo "height" používejte "max-height", gmail konvertuje "height" do "min-height" a obrázky tím roztáhne do výšky.

```html
   
    <table width="800">
        <tr>
            <!-- COLUMN 1 -->
            <td width="500"></td>
            
            <!-- COLUMN 2 -->
            <td width="300">
                <a href="#">
                    <img width="230" src="#" alt="image">
                </a>
            </td>
        </tr>
    </table>
```

----

### SPACING
+ V žádném případě nepoužívejte style="margin: ;". Na cokoli! Outlook ho ignoruje. Kromě margin definovaných v highlevel elementech u základní kostry emailu na konci tohoto dokumentu. 
+ Aplikujte základní spacing přes "table"(cellpadding) attribute.
+ Pokud chcete zmenšit / zvětšit spacing unvitř "table", definovaný přes "cellpadding" attribute, aplikujte inline style "padding" na "td" element.
+ Neaplikujte spacing na žadný jiný element než "table"(cellpadding) a td(style="padding: ;")
    - tzn. žádný padding na "span", "a", "img", "em", "strong", "small", jen "table" a "td"!
    
```html
   
    <!-- 10px na všech stranách uvnitř každého <td> elementu -->
    <table cellpadding="10">
        
        <tr>
            <!-- zmenší spacing top na 5px, ostaní zůstávají na 10px. -->
            <td style="padding-top: 5px">
                <span>Tento text je o 5px výše než je definovaný cellpadding, v tomto případě je jen 5px. "tr" elementy pod ním se také posunou o 5px výše.</span>
            </td>
            <td>
                <span>Tento text je 20px vedle prvního "span" tagu. 10px + 10px. A 10px od horního okraje definovaného pres "table"(cellpadding).</span>
            </td>
        </tr>
        <tr>
            <td>
                <span>Tento text je 20px pod "span" tagy v prní "tr". 10px + 10px. Ale posunutý o 5px výše, protože "td" v první "tr" má definovaný "padding-top: 5px;"</span>
            </td>
        </tr>
    </table>
```

----

### DESIGN HORIZONTÁLNÍ LINKY / ODDĚLOVACÍHO PANELU
+ Tato "table row" Vám pomůže se ujistit, že pod Vaším sloupečkem bude vždy místo. 
+ Díky tomu nemusíte přidávat padding-bottom na poslední "td" element sloupečku a mazat z předchozího "td" elemetnu sloupečku pokaždé, když přidáte nový element.
+ => Čím méně stylingu budete ke style attributu přidávat, tím pravděpodobněji bude email kompatibilní s různými druhy klientů.

```html

    <tr>
        <td align="center" valign="top">
            <table border="0" cellpadding="0" cellspacing="0" width="100%" style="border-collapse: collapse;">
                <tr>
                
                    <!-- ZDE DEFINUJETE ŠÍŘKU A BARVU LINKY -->
                    <td height="3" style="font-size:1px; line-height:1px;" bgcolor="#333333">&nbsp;</td>
                </tr>
            </table>
        </td>
    </tr>
```

----

### USPOŘÁDÁNÍ ELEMENTŮ UVNITŘ TABULKY
+ Abyste mohli manipulovat s elementy uvnitř "td" elementu přes "td" attributy(align - horizontal, valign - vertical), elementy nesmí být block level ("p", "h", "div"), použijte "span" místo nich.

```html
   
    <!-- USPOŘÁDÁ TEXT UPROSTŘED A ON TOP OF THE TD ELEMENT -->
    <td align="center" valign="top">
        <span>Some text</span>
    </td>
```

+ "img" element je také block level element ale často bývá wrapnutý v "a" tagu, který block level elementem není. Proto s ním lze také manipulovat přes "td" attributy(align, valign).

----

### OBRÁZKY
+ Pokud je to jen možné, mějte obrázky v přesné požadované velikosti.
+ Pokud obrázek nemá požadovanou šířku, definujte jeho šířku přes "img" attribute "width". Outlook mi to bral.

```html
    
    <!-- TAKTO BY MĚL VYPADAT STYLING KAŽDÉHO <img> ELEMENTU PODLE MAILCHIMPU -->
    <img width="240" style="border: 0; height: auto; line-height: 100%; outline: none; text-decoration: none;" src="http://lorempicsum.com/nemo/240/140/6" alt="article one image">
```

----

### TYPOGRAFIE
+ Používejte jen [web safe fonts](http://web.mit.edu/jmorzins/www/fonts.html).
+ Aplikujte text styling přímo na text elementy jako "span", "em", "strong", "a".
+ Pokud aplikujete text styling na "table" nebo "td" element, Outlook bude styly ignorovat.
+ Outlook ignoruje line-height a nastavuje vlastní. 
+ Při větší line-height než je font-size se začne tvořit malý margin on top, kterého se nelze zbavit - například negativním margin, který v outlooku nefunguje.

----

### LINKY
+ do "a" tagu obalujte jen text a obrazky, nikdy neobalovat a tagem "table", "tr" a "td" - linky přestanou fungovat.

----

## Základní HTML struktura inspirovaná MailChimp templatem:

```html
    
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Euro Newsletter</title>
        <style type="text/css">
            
            /* FORCE OUTLOOK TO PROVIDE A "VIEW IN BROWSER" BUTTON. */
            #outlook a {
                padding: 0;
            }
            
            /* FORCE HOTMAIL TO DISPLAY EMAILS AT FULL WIDTH */
            .ReadMsgBody {
                width: 100%;
            }

            .ExternalClass {
                width: 100%;
            }
            
            /* YAHOO OVERRIDE */
            a .yshortcuts {
                color: #336699;
                font-weight: normal;
                text-decoration: underline;
            }

        </style>
        <meta name="description" content="email-template">
    </head>
    <body leftmargin="0" marginwidth="0" topmargin="0" marginheight="0" offset="0" style="margin:0; padding:0; width: 100% !important;">
        <table border="0" cellpadding="0" cellspacing="0" height="100%" width="100%" style="height:100% !important; margin:0; padding:0; width:100% !important; border-collapse: collapse;">
            <tr>
               
                <!-- USE align="center" ATTRIBUTE TO CENTER THE EMAIL, DON'T USE style="margin: 0 auto;" -->
                <td align="center" valign="top">
                   
                    <!-- THIS IS WHERE YOU SET EMAIL WIDTH -->
                    <table border="0" cellpadding="0" cellspacing="0" width="800" style="border-collapse: collapse;">
                       
                        <!-- EMAIL HEADER ROW -->
                        <tr>
                            <td align="center" valign="top">
                                <table border="0" cellpadding="0" cellspacing="0" width="800" style="border-collapse: collapse;">
                                    <!-- EMAIL HEADER -->
                                </table>
                            </td>
                        </tr>
                        
                        <!-- EMAIL CONTENT ROW -->
                        <tr>
                            <td align="center" valign="top">
                                <table border="0" cellpadding="0" cellspacing="0" width="800" style="border-collapse: collapse;">
                                    <!-- EMAIL CONTENT -->
                                </table>
                            </td>
                        </tr>
                        
                        <!-- EMAIL FOOTER ROW -->
                        <tr>
                            <td align="center" valign="top">
                                <table border="0" cellpadding="0" cellspacing="0" width="800" style="border-collapse: collapse;">
                                    <!-- EMAIL FOOTER -->
                                </table>
                            </td>
                        </tr>
                    </table>
                </td>
            </tr>
        </table>
    </body>
    </html>
```

----

### Zajímavé odkazy:
http://templates.mailchimp.com/development/
