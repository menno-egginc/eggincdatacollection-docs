# API routes

## All data
`eggincdatacollection.azurewebsites.net/api/GetAllData`

Artifact parameters excluded by default, use `includeArtifactParameters=true` to include them

## All data in CSV format
`eggincdatacollection.azurewebsites.net/api/GetAllDataCsv`

Compact format (IDs only):
`eggincdatacollection.azurewebsites.net/api/GetAllDataCsvCompact`

## Filtered data
Json format:
`eggincdatacollection.azurewebsites.net/api/GetFilteredData?filterName=filtervalue1,filtervalue2&otherfilterName=filtervalue3`

Artifact parameters excluded by default, use `includeArtifactParameters=true` to include them

CSV format:
`eggincdatacollection.azurewebsites.net/api/GetFilteredDataCsv?filterName=filtervalue1,filtervalue2&otherfilterName=filtervalue3`

Compact CSV format:
`eggincdatacollection.azurewebsites.net/api/GetFilteredDataCsvCompact?filterName=filtervalue1,filtervalue2&otherfilterName=filtervalue3`

Filters of the same type work as OR, filters of different type work as AND. 
Example: to return all rare and epic artifacts:
`eggincdatacollection.azurewebsites.net/api/GetFilteredData?artifactRarity=rare,epic`

Example: to return all tier 1 artifacts from henerprise ships (note: tier 1 is id 0)
`eggincdatacollection.azurewebsites.net/api/GetFilteredData?artifactLevel=0&shipType=henerprise`

### Available filters
| Field name | Meaning | Possible values |
|---|---|---|
| shipType | Type of ship that was sent | See `Ship types` table, both ids or filtering name can be used |
| shipDurationType | Duration of ship that was sent | See `Ship duration types` table, both ids or filtering name can be used |
| targetArtifact | Artifact that was targeted | See `Artifact types` table, both ids or filtering name can be used. Note that ships without a target show up as UNKNOWN |
| shipLevel | Number of stars the ship has | An integer between 0 and 7 |
| artifactType | Type of artifact that was dropped | See `Artifact types` table, both ids or filtering name can be used. |
| artifactRarity | Rarity of artifact that was dropped | See `Artifact rarities` table, both ids or filtering name can be used |
| artifactLevel | Level/Tier of artifact that was dropped. Note that tier 1 is id 0, tier 2 is id 1, etc | See `Artifact tiers` table, both ids or filtering name can be used

## Get your own inventory in CSV / JSON format
`https://eggincdatacollection.azurewebsites.net/api/GetInventoryCsv?eid=EIxxx`
`https://eggincdatacollection.azurewebsites.net/api/GetInventoryJson?eid=EIxxx`

## JSON return format
```
[
  {
    "shipConfiguration": {
      "shipType": {
        "id": 9,
        "name": "HENERPRISE"
      },
      "shipDurationType": {
        "id": 2,
        "name": "EPIC"
      },
      "level": 7,
      "targetArtifact": {
        "id": 0,
        "name": "LUNAR_TOTEM"
      }
    },
    "artifactConfiguration": {
      "artifactType": {
        "id": 11,
        "name": "PHOENIX_FEATHER"
      },
      "artifactRarity": {
        "id": 0,
        "name": "COMMON"
      },
      "artifactLevel": 0,
/// EXCLUDED BY DEFAULT
      "artifactParameters": {
        "baseQuality": 10.9,
        "oddsMultiplier": 0.0006
///
      }
    },
    "totalDrops": 17
  }
]
```

## CSV return format
```
Ship type ID,Ship type,Ship duration type ID,Ship duration type,Ship level,Target artifact ID,Target artifact,Artifact type ID,Artifact type,Artifact rarity ID,Artifact rarity,Artifact tier,Total drops
9,HENERPRISE,2,EPIC,7,10,BOOK_OF_BASAN,4,BEAK_OF_MIDAS,3,LEGENDARY,3,1
9,HENERPRISE,2,EPIC,7,17,GOLD_METEORITE,12,TUNGSTEN_ANKH,3,LEGENDARY,2,1
```

## Ship types
| id  | API name  | In-game name  | Filtering name |
|---|---|---|---|
| 0  | CHICKEN_ONE  | Chicken One  | ChickenOne |
|  1 | CHICKEN_NINE  | Chicken Nine  | ChickenNine |
|  2 | CHICKEN_HEAVY  | Chicken Heavy | ChickenHeavy |
|  3 | BCR | BCR | Bcr |
|  4 | MILLENIUM_CHICKEN | Quintillion Chicken | MilleniumChicken |
|  5 | CORELLIHEN_CORVETTE | Cornish-Hen Corvette | CorellihenCorvette |
|  6 | GALEGGTICA | Galeggtica | Galeggtica |
|  7 | CHICKFIANT | Defihent | Chickfiant |
|  8 | VOYEGGER | Voyegger | Voyegger |
|  9 | HENERPRISE | Henerprise | Henerprise |
| 10 | ATREGGIES | Atreggies Henliner | Atreggies |

## Ship duration types
| id  | API name  | In-game name  | Filtering name |
|---|---|---|---|
|  0 | SHORT | Short | Short |
|  1 | LONG  | Standard | Long |
|  2 | EPIC  | Extended | Epic |
|  3 | TUTORIAL | Tutorial | Tutorial |

## Artifact types
| id  | API name  | In-game name  | Filtering name |
|---|---|---|---|
|  0 | LUNAR_TOTEM | Lunar totem | LunarTotem |
|  1 | TACHYON_STONE | Tachyon stone | TachyonStone |
|  2 | TACHYON_STONE_FRAGMENT | Tachyon stone fragment | TachyonStoneFragment |
|  3 | NEODYMIUM_MEDALLION | Neodymium medallion | NeodymiumMedallion |
|  4 | BEAK_OF_MIDAS | Beak of Midas | BeakOfMidas |
|  5 | LIGHT_OF_EGGENDIL  | Light of Eggendil | LightOfEggendil |
|  6 | DEMETERS_NECKLACE | Demeters necklace | DemetersNecklace |
|  7 | VIAL_MARTIAN_DUST | Vial of Martian dust | VialMartianDust |
|  8 | ORNATE_GUSSET | Gusset | OrnateGusset |
|  9 | THE_CHALICE | The Chalice | TheChalice |
| 10 | BOOK_OF_BASAN | Book of Basan | BookOfBasan |
| 11 | PHOENIX_FEATHER | Phoenix feather | PhoenixFeather |
| 12 | TUNGSTEN_ANKH | Tungsten Ankh | TungstenAnkh |
| 13 | EXTRATERRESTIAL_ALUMINUM | n/a | ExtraterrestialAluminum |
| 14 | ANCIENT_TUNGSTEN | n/a | AncientTungsten |
| 15 | SPACE_ROCKS | n/a | SpaceRocks |
| 16 | ALIEN_WOOD | n/a | AlienWood |
| 17 | GOLD_METEORITE | Gold meteorite | GoldMeteorite |
| 18 | TAU_CETI_GEODE | Tau ceti geode | TauCetiGeode |
| 19 | CENTAURIAN_STEEL | n/a | CentaurianSteel |
| 20 | ERIDANI_FEATHER | n/a | EridaniFeather |
| 21 | AURELIAN_BROOCH | Aurelian brooch | AurelianBrooch |
| 22 | CARVED_RAINSTICK | Carved rainstick | CarvedRainstick |
| 23 | PUZZLE_CUBE | Puzzle cube | PuzzleCube |
| 24 | QUANTUM_METRONOME | Quantum metronome | QuantumMetronome |
| 25 | SHIP_IN_A_BOTTLE | Ship in a bottle | ShipInABottle |
| 26 | TACHYON_DEFLECTOR | Tachyon Deflector | TachyonDeflector |
| 27 | INTERSTELLAR_COMPASS | Interstellar compass | InterstellarCompass |
| 28 | DILITHIUM_MONOCLE | Dilithium monocle | DilithiumMonocle |
| 29 | TITANIUM_ACTUATOR | Titanium actuator | TitaniumActuator |
| 30 | MERCURYS_LENS | Mercurys lens | MercurysLens |
| 31 | DILITHIUM_STONE | Dilithium stone | DilithiumStone |
| 32 | SHELL_STONE | Shell stone | ShellStone |
| 33 | LUNAR_STONE | Lunar stone | LunarStone |
| 34 | SOUL_STONE | Soul stone | SoulStone |
| 35 | DRONE_PARTS | n/a | DroneParts |
| 36 | QUANTUM_STONE | Quantum stone | QuantumStone |
| 37 | TERRA_STONE | Terra stone | TerraStone |
| 38 | LIFE_STONE | Life stone | LifeStone |
| 39 | PROPHECY_STONE | Prophecy stone | ProphecyStone |
| 40 | CLARITY_STONE | Clarity stone | ClarityStone |
| 41 | CELESTIAL_BRONZE | n/a | CelestialBronze |
| 42 | LALANDE_HIDE | n/a | LalandeHide |
| 43 | SOLAR_TITANIUM | Solar titanium | SolarTitanium |
| 44 | DILITHIUM_STONE_FRAGMENT | Dilithium stone fragment | DilithiumStoneFragment
| 45 | SHELL_STONE_FRAGMENT | Shell stone fragment | ShellStoneFragment |
| 46 | LUNAR_STONE_FRAGMENT | Lunar stone fragment | LunarStoneFragment |
| 47 | SOUL_STONE_FRAGMENT | Soul stone fragment | SoulStoneFragment |
| 48 | PROPHECY_STONE_FRAGMENT | Prophecy stone fragment | ProphecyStoneFragment |
| 49 | QUANTUM_STONE_FRAGMENT | Quantum stone fragment | QuantumStoneFragment |
| 50 | TERRA_STONE_FRAGMENT | Terra stone fragment | TerraStoneFragment |
| 51 | LIFE_STONE_FRAGMENT | Life stone fragment | LifeStoneFragment |
| 52 | CLARITY_STONE_FRAGMENT | Clarity stone fragment | ClarityStoneFragment |
| 10000 | UNKNOWN | Unknown / No target | Unknown |

## Artifact rarities
| id  | API name  | In-game name  | Filtering name |
|---|---|---|---|
|  0 | COMMON | Common | Common |
|  1 | RARE | Rare | Rare |
|  2 | EPIC | Epic | Epic |
|  3 | LEGENDARY | Legendary | Legendary |

## Artifact tiers
| id  | API name  | In-game name  | Filtering name |
|---|---|---|---|
|  0 | INFERIOR | Tier 1 | Inferior |
|  1 | LESSER | Tier 2 | Lesser |
|  2 | NORMAL | Tier 3 | Normal |
|  3 | GREATER | Tier 4 | Greater |
|  4 | SUPERIOR | n/a | Superior |


