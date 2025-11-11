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
  try {
    let held = api.getHeldItem(myId)?.attributes
    held.customAttributes.mobSettings.petInfo[setting]=value

    let name=api.getHeldItem(myId).name

    api.removeItemName(myId, api.getHeldItem(myId).name, 1)
    api.giveItem(myId, name, 1, {customAttributes: {

      dbId: held.customAttributes.dbId,
      health: held.customAttributes.health,
      mobSettings: held.customAttributes.mobSettings,

      version: 1,

    }})
  } catch(err) {api.log("Error"+err)}
}


/**
 * Get things like friendship level
 * @param {PlayerId} myId
 * @param {String} setting - See above list for supported settings
 * @returns {Any}
 */

function getCaughtMobPetInfo(myId, setting) {
  try {
    let held = api.getHeldItem(myId)?.attributes
    return held.customAttributes.mobSettings.petInfo[setting]
  } catch(err) {api.log("Error"+err)}
}
```
