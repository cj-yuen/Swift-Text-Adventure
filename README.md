# *Swift Text-Adventure*

## Explanations

**What locations/rooms does your game have?**

1. Hero's Base
2. Goblin's Forest
3. Dwarven Mountain
4. Elven City
5. Demon's Castle

**What items does your game have?**

1. Elder Wood
2. Meteorite Ore
3. Orb of Destruction
4. Demon Slaying Sword
5. Suspicious Demonic Heart

**Explain how your code is designed. In particular, describe how you used structs or enums, as well as protocols.**

*I have 2 different structs for Location and Items. I also used a protocol for LocationObject. I used an array to store the different possible Locations. I also implemented 'Help' commands as a String variable within my Location struct.*

**How do you use optionals in your program?**

*I used optionals for items to check whether the player possessed that item or not. For example. (item_name).possession == nil would mean that the player did not obtain the item yet.*

**What extra credit features did you implement, if any?**

*I implemented blue text to highlight the important commands that the player will need to type out. I also underlined the current locations.*

## Endings

### Ending 1: Early Death

```
North
North
North
```

### Ending 2: Slay the Demon King

```
North
Fight
Fight
Fight
SummonElderWood
West
Mine
Mine
Mine
SummonMagicOre
East
East
Search
Search
Search
SummonOrb
West
South
Craft
North
North
Kill
```

### Ending 3: Become the Demon King

```
North
Fight
Fight
Fight
SummonElderWood
West
Mine
Mine
Mine
SummonMagicOre
East
East
Search
Search
Search
SummonOrb
West
South
Craft
North
PickUp
North
Kill
Absorb
```
