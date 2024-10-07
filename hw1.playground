import SwiftUI

// TODO: Declare any additional structs, classes, enums, or protocols here!
protocol LocationObject {
    var help_commands: String { get set }
    var description: String { get set }
    
    func displayLocation() -> String
}

struct Location : LocationObject {
    var help_commands : String
    var description : String
    var name : AttributedString
    
    // Initialization
    init(help_commands: String, description: String, name: String) {
        self.help_commands = help_commands
        self.description = description
        
        var attributedName = AttributedString(name)
        attributedName.swiftUI.underlineStyle = .single
        
        self.name = attributedName
    }
    
    // Methods
    func displayLocation() -> String {
        return "\(self.name)"
    }
}

struct Item {
    var description: String
    var possession: Bool?
    
    // Initialization
    init(description: String) {
        self.description = description
        self.possession = nil
    }
}

/// Declare your game's behavior and state in this struct.
///
/// This struct will be re-created when the game resets. All game state should
/// be stored in this struct.
struct YourGame: AdventureGame {
    var hero_base = Location(help_commands: "Type 'North' to move towards the Goblin Pastures", description: "Here is where the journey of every hero begins.", name: "Hero's Base")
    var goblin_forest = Location(help_commands: "Type 'South' to move back to the Hero's Base.\nType 'East' to move to the Elven City. \n type 'West' to move to the Dwarven Mountain.\nType North to move to the Demon's Castle.", description: "Here is where many goblins lurk and hide, waiting for unsuspecting travelers to walk through and fall into their traps.", name: "Goblin's Forest")
    var dwarven_mountain = Location(help_commands: "Type 'East' to return back to the Goblin's Forest", description: "Here is where the mighty dwarves have lived for centuries. They are well known for their mighty blacksmithing skills and fine craftsmanship of the greatest weapons of this world", name: "Dwarven Mountains")
    var elven_city = Location(help_commands: "Type 'West' to return back to the Goblin's Forest", description: "Here is where the oldest city lies. Built by the elves, the Elven City is one of the great wonders of this world, possessing ancient relics and many secrets wait to be uncovered.", name: "Elven City")
    var demon_castle = Location(help_commands: "Type 'South' to return back to the Goblin's Forest", description: "Here is the castle which hosts the Great Demon Lord Lucius! Beware of his tricks and mighty powers.", name: "Demon Castle")
    
    var poss_location: [String: Location] = [:]
    var curr_location: Location
    
    var demon_slaying_sword = Item(description: "Sword needed to defeat the Great Demon Lord Lucius!")
    
    var attributedCraft = AttributedString("'Craft'")
    
    var elder_wood = Item(description: "anicent wood needed for the handle of for the Demon Slaying Sword.")
    
    var attributedSummonElderWood = AttributedString("'SummonElderWood'")
    
    var meteorite_ore = Item(description: "extraterrestrial minerals formed one of the strongest ores known to this world. Will be the blade of the Demon Slaying Sword.")
    
    var attributedMeteoriteOre = AttributedString("'SummonMagicOre'")
    
    var orb_of_destruction = Item(description: "forbidden source of power than will provide the mana for the demon-slaying magic within the Demon Slaying Sword.")
    
    var attributedOrb = AttributedString("'SummonOrb'")
    
    var blueCommand = AttributedString("")
    
    var asked_north_unprepared = false
    var slained_goblins = 0
    var mined_rocks = 0
    var search_markets = 0
    
    var demonic_heart = Item(description: "may be useful in the future?")
    
    var demon_king = false
    
    // Initialization
    init() {
        self.poss_location = [
            "Hero's Base": hero_base,
            "Goblin's Forest": goblin_forest,
            "Dwarven Mountains": dwarven_mountain,
            "Elven City": elven_city,
            "Demon Castle": demon_castle
        ]
        self.curr_location = hero_base
    }
    
    /// Returns a title to be displayed at the top of the game.
    ///
    /// You can generate this dynamically based on your game's state.
    var title: String {
        return "Demon Lord Slayer"
    }
    
    /// Runs at the start of every game.
    ///
    /// Use this function to introduce the game to the player.
    ///
    /// - Parameter context: The object you use to write output and end the game.
    mutating func start(context: AdventureGameContext) {
        context.write("Welcome young hero, you have embarked on a mission to save the world from the tyranny of the Great Demon Lord Lucius! He is waiting for a worthy challenger in his castle. Please become stronger and free our world from his grasp.\n\nYou start off your journey at the ")
        context.write(curr_location.name)
        context.write("Type 'Help' for more commands.")
    }
    
    /// Runs when the user enters a line of input.
    ///
    /// Generally, you parse the user's command, update game state as necessary, then
    /// write output.
    ///
    /// To display a line to the user, use the `context.write(_)` function and pass in
    /// a ``String``, like this:
    ///
    /// ```swift
    /// context.write("You have been eaten by a grue.")
    /// ```
    ///
    /// If you'd like to end the game (say, if the player dies), call context.endGame().
    /// Note that this does *not* display a game over message - it merely disables
    /// the buttons and forces the user to reset.
    ///
    /// **Sidenote:** context.write() supports AttributedString for rich text formatting.
    /// Consult the [homework instructions](https://www.seas.upenn.edu/~cis1951/assignments/hw/hw1)
    /// for guidance.
    ///
    /// - Parameters:
    ///   - input: The line the user typed.
    ///   - context: The object you use to write output and end the game.
    mutating func handle(input: String, context: AdventureGameContext) {
        let arguments = input.split(separator: " ")
        if arguments.isEmpty {
            context.write("Please enter a command.")
            return
        }
        
        if (curr_location.name == hero_base.name) {
            switch arguments[0] {
            case "Help":
                context.write("\(curr_location.help_commands)")
            case "North":
                curr_location = goblin_forest
                context.write("Moving \(input), you have entered the")
                context.write(curr_location.name)
                context.write("\(curr_location.description)")
                if (slained_goblins < 3) {
                    context.write("Fight 3 Goblins. To fight a goblin type")
                    blueCommand = AttributedString("'Fight'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
                if (demon_slaying_sword.possession == true) {
                    context.write("On your walking through the forest, you stumble across a suspicious looking object on the ground. It \(demonic_heart.description)")
                    
                    context.write("1) If you want to pick it up type")
                    blueCommand = AttributedString("'PickUp'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                    
                    context.write("\n2) To skip, type")
                    blueCommand = AttributedString("'North'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            case "Craft":
                if ((elder_wood.possession == nil) || (meteorite_ore.possession == nil) || (orb_of_destruction.possession == nil)) {
                    context.write("You are missing crucial materials for the Demon Slaying Sword. Please look for what you're missing.")
                } else {
                    demon_slaying_sword.possession = true
                    context.write("You have crafted the Demon Slaying Sword. Please make your way towards the Demon King's Castle to slay Demon King Lucius and free this world from his tyranny!\n\nIf you forgot how to reach the Demon King's Castle, type")
                    blueCommand = AttributedString("'Help'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            default:
                context.write("Invalid command. Type 'Help' if you are lost.")
            }
        } else if (curr_location.name == goblin_forest.name) {
            switch arguments[0] {
            case "Help":
                context.write("\(curr_location.help_commands)")
            case "PickUp":
                if (demon_slaying_sword.possession == nil) {
                    context.write("You were caught using demonic techniques by the Gods and have been smited ⚡️\n\nYou died...")
                    context.endGame()
                } else {
                    demonic_heart.possession = true
                    context.write("You have picked up susupicious looking object and continue marching towards the Demon King's Castle.\n\nIf you forgot how to reach the Demon King's Castly, type")
                    blueCommand = AttributedString("'Help'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            case "Fight":
                if (slained_goblins < 2) {
                    slained_goblins += 1
                    context.write("Slained goblins ⚔️x\(slained_goblins)")
                }
                else if (slained_goblins == 2) {
                    slained_goblins += 1
                    context.write("Slained goblins ⚔️x\(slained_goblins)\n\nYou have slained 3 goblins, you can now pick collect the elder wood, \(elder_wood.description)\n\nTo pick up the elder wood, type the spell")
                    attributedSummonElderWood.swiftUI.foregroundColor = .blue
                    context.write(attributedSummonElderWood)
                }
                else {
                    slained_goblins += 1
                    context.write("Slained goblins ⚔️\(slained_goblins)")
                }
            case "SummonElderWood":
                if (slained_goblins < 3) {
                    context.write("You were caught using demonic techniques by the Gods and have been smited ⚡️\n\nYou died...")
                    context.endGame()
                } else {
                    elder_wood.possession = true
                    context.write("You have picked up the elder wood however you must collect 2 more items before crafting the Demon Slaying Sword. Please collect some meteorite ore from the Dwarven Mountain.\n\nIf you forgot how to reach the Dwarven Mountain, type")
                    blueCommand = AttributedString("'Help'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            case "South":
                curr_location = hero_base
                context.write("Moving \(input), you have entered the")
                context.write(curr_location.name)
                context.write("\(curr_location.description)")
                if ((elder_wood.possession == true) && (meteorite_ore.possession == true) && (orb_of_destruction.possession == true)) {
                    context.write("Now with the elder wood, meteorite ore, and the orb of destruction, you can craft the Demon Slaying Sword. To do so, type")
                    attributedCraft.swiftUI.foregroundColor = .blue
                    context.write(attributedCraft)
                }
            case "West":
                curr_location = dwarven_mountain
                context.write("Moving \(input), you have entered the")
                context.write(curr_location.name)
                context.write("\(curr_location.description)")
                if (mined_rocks < 3) {
                    context.write("Mine 3 rocks. To mine rocks type")
                    blueCommand = AttributedString("'Mine'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            case "East":
                curr_location = elven_city
                context.write("Moving \(input), you have entered the")
                context.write(curr_location.name)
                context.write("\(curr_location.description)")
                if (search_markets < 3) {
                    context.write("Search the markets 3 times. To search type")
                    blueCommand = AttributedString("'Search'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            case "North":
                if ((demon_slaying_sword.possession == nil) && (asked_north_unprepared == false)) {
                    asked_north_unprepared = true
                    context.write("You do not possess the Demon Slaying Sword required to slay the Demon King. If you wish to still enter type")
                    blueCommand = AttributedString("'North'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                } else if ((demon_slaying_sword.possession == nil) && (asked_north_unprepared == true)) {
                    context.write("You entered Demon King Lucius' Castle unprepared and was slained ruthlessly.\n\nGame Over...")
                    context.endGame()
                } else if (demon_slaying_sword.possession == true) {
                    curr_location = demon_castle
                    context.write("Moving \(input), you have entered the")
                    context.write(curr_location.name)
                    context.write("\(curr_location.description)\n\nTo slay Demon King Lucius type")
                    blueCommand = AttributedString("'Kill'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            default:
                context.write("Invalid command. Type 'Help' if you are lost.")
            }
        } else if (curr_location.name == dwarven_mountain.name) {
            switch arguments[0] {
            case "Help":
                context.write("\(curr_location.help_commands)")
            case "Mine":
                if (mined_rocks < 2) {
                    mined_rocks += 1
                    context.write("Mined rocks 🪨⛏️x\(mined_rocks)")
                } else if (mined_rocks == 2) {
                    
                    mined_rocks += 1
                    context.write("Mined rocks 🪨⛏️x\(mined_rocks)")
                    context.write("\n\nYou have mined 3 rocks and found the meteorite ore, \(meteorite_ore.description)\n\nTo pick up the meteorite ore, type the spell")
                    attributedMeteoriteOre.swiftUI.foregroundColor = .blue
                    context.write(attributedMeteoriteOre)
                } else {
                    mined_rocks += 1
                    context.write("Mined rocks 🪨⛏️x\(mined_rocks)")
                }
            case "SummonMagicOre":
                if (mined_rocks < 3) {
                    context.write("You were caught using demonic techniques by the Gods and have been smited ⚡️\n\nYou died...")
                    context.endGame()
                } else {
                    meteorite_ore.possession = true
                    context.write("You have picked up the meteorite ore however you must collect 1 more item before crafting the Demon Slaying Sword. Please find the orb of destruction from the Elven City.\n\nIf you forgot how to reach the Elven City, type")
                    blueCommand = AttributedString("'Help'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            case "East":
                curr_location = goblin_forest
                context.write("Moving \(input), you have entered the")
                context.write(curr_location.name)
                context.write("\(curr_location.description)")
                if (slained_goblins < 3) {
                    context.write("Fight 3 Goblins. To fight a goblin type")
                    blueCommand = AttributedString("'Fight'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            default:
                context.write("Invalid command. Type 'Help' if you are lost.")
            }
        } else if (curr_location.name == elven_city.name) {
            switch arguments[0] {
            case "Help":
                context.write("\(curr_location.help_commands)")
            case "Search":
                if (search_markets < 2) {
                    search_markets += 1
                    context.write("Searched markets 🔍x\(search_markets)")
                } else if (search_markets == 2) {
                    search_markets += 1
                    context.write("Searched markets 🔍x\(search_markets)")
                    context.write("You have searched the markets 3 rocks and found the orb of destruction, \(orb_of_destruction.description)\n\nTo pick up the orb, type the spell")
                    attributedOrb.swiftUI.foregroundColor = .blue
                    context.write(attributedOrb)
                } else {
                    search_markets += 1
                    context.write("Searched markets 🔍x\(search_markets)")
                }
            case "SummonOrb":
                if (search_markets < 3) {
                    context.write("You were caught using demonic techniques by the Gods and have been smited ⚡️\n\nYou died...")
                    context.endGame()
                } else {
                    orb_of_destruction.possession = true
                    context.write("You have picked up the orb of destruction. Now you can craft the Demon Slaying Sword. Please return to the Hero's Base.\n\nIf you forgot how to reach the Hero's Base, type")
                    blueCommand = AttributedString("'Help'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            case "West":
                curr_location = goblin_forest
                context.write("Moving \(input), you have entered the")
                context.write(curr_location.name)
                context.write("\(curr_location.description)")
                if (slained_goblins < 3) {
                    context.write("Fight 3 Goblins. To fight a goblin type")
                    blueCommand = AttributedString("'Fight'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            default:
                    context.write("Invalid command. Type 'Help' if you are lost.")
            }
        } else if (curr_location.name == demon_castle.name) {
            switch arguments[0] {
            case "Help":
                context.write("\(curr_location.help_commands)")
            case "Kill":
                if ((demonic_heart.possession == true) && (demon_king == false)) {
                    demon_king = true
                    context.write("You are about to kill Demon King Lucius but before your sword reaches him, he pleads for you to listen. Lucius explains how he too was once a hero but discovered a suspicious object that turned out to be a demonic heart. With a demonic heart, one is able to become the next Demon King by slaying the current one and absorbing his power. What is your decision?")
                    context.write("1) Slay Demon King Lucius and free this world, type")
                    blueCommand = AttributedString("'Kill'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                    context.write("\n2) Become the next demon king, type")
                    blueCommand = AttributedString("'Absorb'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                } else {
                    context.write("You have successfully slained Demon King Lucius! As the saviour of this world you are praised for generations. Over time you given riches and treasures beyond your wildest dreams.\n\nA hero's end...")
                    context.endGame()
                }
            case "Absorb":
                if (demon_king == false) {
                    context.write("You were caught using demonic techniques by the Gods and have been smited ⚡️\n\nYou died...")
                    context.endGame()
                } else {
                    context.write("You stab Demon King Lucius and absorb his power becoming the next Demon King. You possess immortality and eternal youth. However one thing that Demon King Lucius failed to mention is that once you becomes the next Demon King, you are forever trapped within the Demon King's Castle.\n\nYou spend centuries waiting and waiting...Hopefully one day someone brave enough will stand up to your so-called 'tyranny' and free this world for the reign of the Demon King!")
                    context.endGame()
                }            case "South":
                curr_location = goblin_forest
                context.write("Moving \(input), you have entered the")
                context.write(curr_location.name)
                context.write("\(curr_location.description)")
                if (slained_goblins < 3) {
                        context.write("Fight 3 Goblins. To fight a goblin type")
                    blueCommand = AttributedString("'Fight'")
                    blueCommand.swiftUI.foregroundColor = .blue
                    context.write(blueCommand)
                }
            default:
                context.write("Invalid command. Type 'Help' if you are lost.")
            }
        }
    }
}

// Leave this line in - this line sets up the UI you see on the right.
// Update this if you rename your AdventureGame implementation.
YourGame.display()
