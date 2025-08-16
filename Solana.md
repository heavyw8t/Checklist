### Can users get an account with more money in rent then they pay for the transaction?
Look for cases in which a user can transfer, mint or bridge dust amounts and the operator pays for the account creation, letting the user drain the rent of the account. This can then be repeated by the users to fully drain the protocol

// Add Example
[Example]()

### Are Token22 extensions supported?
If the Token22 standard should be supported by the protocol, the extensions that the mint contains need to be checked. The protocol either has to prohibit mints with certain extensions or handle them correctly. 
[Example](https://solodit.cyfrin.io/issues/lack-of-validation-for-extensions-of-the-mint-halborn-huma-huma-protocol-markdown)

// Rewrite this one
### Is there a check to prevent important accounts from accidental transferring their rent 
Any important account that transfers sol somewhere in the flow of the protocol should have a check that it prevents it from sending too much funds and not containing enough rent to stop it from being garbage collected. 