# Pet Info Functions

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
```
