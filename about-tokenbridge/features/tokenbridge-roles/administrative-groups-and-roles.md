# Administrative Groups and Roles

Administrators on the bridge manage the bridge smart contracts. Validators can be setup as administrators, or separate entities can fulfill this position. The groups are responsible for the following on **each side** of the bridge:

### **Group A (Manages validator set)**

* Adds or removes validators
* Sets minimum required signatures from validators in order to relay a user's transaction

### **Group B: (Manages bridge parameters)**

* Sets daily limits for users and validators
* Sets min/max per transaction limits
* Sets fallback gas price
* Sets finalization threshold

### **Group C: (Manages upgrades)**

* Upgrades contracts in case of vulnerability
* Unlocks funds

## Administrative Groups Setup

There are 3 administrative roles required for each side of the bridge, resulting in a total of 6 administrative groups responsible for these roles. Each group requires a multisig (the minimum number of signatures is configurable) to confirm an action.

The admin group setup can be customized in the bridge settings. For example, the same group of administrators may control multiple groups with a single multisig, or each administrative group may be a distinct entity with different multisig requirements.

In addition, validators on each chain require multisig operations, but this is built-in to the contracts.

### **Chain 1**

* Group A (1)
* Group B (2)
* Group C (3)
* Validators (elected by group A) (4)

### **Chain 2**

* Group A (5)
* Group B (6)
* Group C (7)
* Validators (elected by group A) (8)
