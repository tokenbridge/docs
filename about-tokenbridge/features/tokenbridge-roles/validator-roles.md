# Validator Roles

Validators do not manage smart contracts in the bridge setup (unless they are also given an administrative role). They are managed by Administration Group A. Validators in the network are responsible for:

* Providing 100% uptime to relay transactions
* Listening for `UserRequestForSignature` events on the Home side and signing an approval to relay assets on the Foreign side
* Listening for `CollectedSignatures` events on the Home side. Once enough signatures are collected, transferring all collected signatures to the Foreign side.
* Listening for `UserRequestForAffirmation` or `Transfer` (depending on the bridge mode) events on the Foreign side and sending approval to the Home side to relay assets from Foreign Network to Home.
