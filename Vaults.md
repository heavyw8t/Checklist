## Common bugs and exploits

### Inflation attack
When a new vault is created, the first depositor can be frontrun by an attacker who will deposit just enough so that the initial depositor's shares will be rounded down to 0, and the attacker can withdraw their one share, now also containing the victim's tokens. This can be mitigated by allowing users to pass a `minSharesOutParameter` or using "dead shares," which are placed in the vault during creation.

[Example](https://solodit.cyfrin.io/?b=false&f=&ff=&i=HIGH&l=&maxf=&minf=&p=1&pc=&pn=&qs=1&r=true&rf=alltime&rs=1&s=inflation+attack&sd=Desc&sf=Recency&t=&u=&ur=true)
[Further reading](https://blog.openzeppelin.com/a-novel-defense-against-erc4626-inflation-attacks)

### Rounding errors
When shares are minted or burned, the protocol should do so in a way that benefits the protocol; otherwise, attackers can use user-benefiting rounding to steal funds from the protocol and users or grief by iterating through the deposit and withdraw functions multiple times

[Example](https://solodit.cyfrin.io/?b=false&f=&ff=&i=HIGH&l=&maxf=&minf=&p=1&pc=&pn=&qs=1&r=true&rf=alltime&rs=1&s=rounding+vault&sd=Desc&sf=Recency&t=&u=&ur=true)