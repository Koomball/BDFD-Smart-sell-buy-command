<details> <summary> Index </summary>
(/Shop)[#/sell]
</details>

# Advanced /sell & /buy command
Variables Needed (3): <br>
- Name: cash | Value: 0
- Name: apples | Value: 0
- Name: oranges | Value: 0

This sell / buy command can take `All` as an input.

---

# /sell
command name: sell. <br>
description: sell your items. <br>

### Option 1 (Text, Preset Choices)
***Option Name:*** item <br>
**Choices:**
| Name | Value |
| :----: | :-----: |
| Apples [$5 Each] | apples-5 |
| Oranges [$10 Each] | oranges-10 |

Option values follow the format:
variableName-sellValue.

### Option 2 (Text)
***Option Name:*** amount <br>

### code:
```
$nomention
$textSplit[$message[item];-]
$c[1]$if[$isNumber[$message[amount]]]
$c[2]$if[$message[amount]>$getVar[$splitText[1];$authorID]]
$title[Invalid Amount]
$description[> You only have $getVar[$splitText[1];$authorID] $splitText[1]]
$footer[TIP: Type all to sell all of the selected item you own.]
$c[2]$else
$setVar[$splitText[1];$sub[$getVar[$splitText[1];$authorID];$message[amount]];$authorID]
$setVar[cash;$calculate[$getVar[cash;$authorID]+($splitText[2]*$message[amount])];$authorID]
$title[Sale Successfull!]
$description[> Sold $message[amount] $splitText[1] for $$multi[$message[amount];$splitText[2]]]
$footer[TIP: Type all to sell all of the selected item you own.]
$c[2]$endif

$c[1]$elseif[$toLowercase[$message[amount]]==all]
$var[amount;$getVar[$splitText[1];$authorID]]
$setVar[$splitText[1];0;$authorID]
$setVar[cash;$calculate[$getVar[cash;$authorID]+($splitText[2]*$var[amount])];$authorID]
$title[Sale Successfull!]
$description[> Sold $var[amount] $splitText[1] for $$multi[$var[amount];$splitText[2]]]
$footer[TIP: Type all to sell all of the selected item you own.]
$c[1]$else
$title[ERROR]
$description[> You entered a invalid number.]
$footer[TIP: Type all to sell all of the selected item you own.]
$c[1]$endif
```
<div> </div>

---

# /buy
### Option 1 (Text, Preset Choices)
***Option Name:*** item <br>
| Name | Value |
| :----: | :-----: |
| Apples [$10 Each] | apples-10 |
| Oranges [$20 Each] | oranges-20 |

Option values follow the format:
variableName-buyCost.

### Option 2 (Text)
***Option Name:*** amount <br>

### code:
```
$nomention
$textSplit[$message[item];-]
$c[1]$if[$isNumber[$message[amount]]]
$var[cost;$multi[$message[amount];$splitText[2]]]
$c[2]$if[$var[cost]>$getVar[cash;$authorID]]
$title[Invalid Amount]
$description[> You only have $$getVar[cash;$authorID]]
$footer[TIP: Type all to buy all of the selected item you can afford.]
$c[2]$else
$setVar[$splitText[1];$sum[$getVar[$splitText[1];$authorID];$message[amount]];$authorID]
$setVar[cash;$calculate[$getVar[cash;$authorID]-($splitText[2]*$message[amount])];$authorID]
$title[Sale Successfull!]
$description[> Bought $message[amount] $splitText[1] for $$multi[$message[amount];$splitText[2]]]
$footer[TIP: Type all to buy all of the selected item you can afford.]
$c[2]$endif

$c[1]$elseif[$toLowercase[$message[amount]]==all]
$var[canAfford;$divide[$getVar[cash;$authorID];$splitText[2]]]
$var[cost;$multi[$var[canAfford];$splitText[2]]]
$setVar[$splitText[1];$sum[$getVar[$splitText[1];$authorID];$var[canAfford]];$authorID]
$setVar[cash;$calculate[$getVar[cash;$authorID]-$var[cost]];$authorID]
$title[Sale Successfull!]
$description[> Bought $var[canAfford] $splitText[1] for $$var[cost]]
$footer[TIP: Type all to buy all of the selected item you can afford.]
$c[1]$else
$title[ERROR]
$description[> You entered a invalid number.]
$footer[TIP: Type all to buy all of the selected item you can afford.]
$c[1]$endif
```
