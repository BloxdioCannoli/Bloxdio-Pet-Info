# Supported petInfo
`friendShipPoints`, `lastFedAt`, `highestFriendshipLevelReached`, `superlikedFood`, `superlikedFoodKnown`, `bonusesGained`

# Pet Info Functions
> Note that you have to be holding a full Mob Catcher for these to work

```js
/**
 * Modify things like friendship level
 * @param {PlayerId} myId
 * @param {String} setting - See above list for supported settings
 * @param {Any} value
 * @returns {void}
 */

function setCaughtMobPetInfo(myId, setting, value) {
  /* Code by Bloxdio Cannoli */
  try {
    let held = api.getHeldItem(myId)?.attributes
    held.customAttributes.mobSettings.petInfo[setting]=value
    /* Code by Bloxdio Cannoli */
    let name=api.getHeldItem(myId).name
    /* Code by Bloxdio Cannoli */
    api.removeItemName(myId, api.getHeldItem(myId).name, 1)
    api.giveItem(myId, name, 1, {customAttributes: {
      /* Code by Bloxdio Cannoli */
      dbId: held.customAttributes.dbId,
      health: held.customAttributes.health,
      mobSettings: held.customAttributes.mobSettings,
      /* Code by Bloxdio Cannoli */
      version: 1,
      /* Code by Bloxdio Cannoli */
    }})
  } catch(err) {api.log("Error"+err)}
  /* Code by Bloxdio Cannoli */
}


/**
 * Get things like friendship level
 * @param {PlayerId} myId
 * @param {String} setting - See above list for supported settings
 * @returns {Any}
 */

function getCaughtMobPetInfo(myId, setting) {
  /* Code by Bloxdio Cannoli */
  try {
    let held = api.getHeldItem(myId)?.attributes
    return held.customAttributes.mobSettings.petInfo[setting]
  } catch(err) {api.log("Error"+err)}
  /* Code by Bloxdio Cannoli */
}
```

# Get max pet
```
setCaughtMobPetInfo(myId, "friendshipPoints", 10000000)
setCaughtMobPetInfo(myId, "lastFedAt", api.now()-1000000)
setCaughtMobPetInfo(myId, "superlikedFoodKnown", true)
```
