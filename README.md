# Advanced /sell & /buy command
Variables Needed (3): <br>
- Name: cash | Value: 0
- Name: apples | Value: 0
- Name: oranges | Value: 0

# /shop
```
empty 
```

# /sell
command name: sell. <br>
description: sell your items. <br>

<details> <summary> config.nyls </summary>

### option 1
- Name: item
- Type: Text
- ✅ Predefined Choices

- choice 1
- - Name: Apple [$5 Each]
- - Value: apples-5

- choice 2
-  Name: Oranges [$10 Each] 
-  Value: oranges-10

Option values follow the format:
variableName-sellValue.

### option 2
- Name: amount
- Type: Text
- ❌ Predefined Choices

### code:
```
empty
```

</details>

# /buy
```
empty
```

