# Local-Economy-Wallet
Add a local component on cryptocurrencies on Ergo

# Global Economy
We live in a world driven by the global economy. The industries and goods production tend to be made where the cost is the lowest.
Usually, it is closely linked with the people living in the production area. It is a balance between salary cost and expertise, skills.

Therefore, goods with low-skilled needs are produced where buying human time is cheap. High technology goods are produced where people are able to make it even if their skills are expensive.

Thus situations tend to:
  • centralize the know-how. People interested in a specific technology have to move to the area where the production is. In the same time, it becomes         difficult to improve local knowledge if your skilled people moved to another place. 
  • push salaries from top to bottom: if 2 localities have the same level of skill to produce a good, it makes sense to have lower salaries to incentive       industries to come. 
  • increase the transport distance: centralizing the production implies the need of dispatching the goods all around the world. It’s a nonsense in terms       of ecology and energy consumption. 
  • move most of the benefits to just a few investors. 
  
# Local Currencies
The Global Economy is not recent. It has been built for decades or centuries.

Consequently, some economists theorized a way to tackle the negative aspects of the Global Economy through local currencies.

Indeed, a currency used only in a small locality increase local trade exchanges and then, decrease the low salary pressure and improve the people skills there. It’s a weapon to bring vitality in a local economy.

Some of these currencies even had a liquid mechanism to tackle the hoarding which makes rich becoming richer. The idea behind it was to encourage trades and a living economy. Until now, the only way to make the money liquid was to tax the stagnant money. As always, taxes are not popular and can be rightly regarded as confiscation.

So, if the local currencies have so many benefits, why aren’t we using it in everyday life?

Actually, these currencies encounter strong resistance from people themselves. Indeed, we hardly give trust in a value that has been created from nowhere and from nothing. And finally, local currencies often look like Monopoly money…

So, local currencies, even if based on good ideas, have been a failure most of the time.

The weapon that could bring vitality in a local economy has always become no more than a toy.

# And then eUTXO was born…
And what if cryptocurrency and especially eUTXO could enable the circulation of local currencies with trust ?

That is exactly the aim of this paper: implementing trustful local currencies.

## Digital cash
UTXO is often compared to cash with a system of trade and change… and that specificity makes possible the usage of the following idea.
But simple UTXO are not programmable, so an eUTXO model is needed.

There, the idea is not to create a new token from nowhere and from nothing otherwise we’ll face the same obstacles than traditional local currencies.
We want to find a way to give a local component to the current cryptocurrencies which already have value.

## Principles
Big cities are the economic lung of areas. So we will build the local component upon the distribution of big cities around the world.

Our innovation will take the form of a wallet. We’ll call it: the Local Economy Wallet (LEW). It will be divided in two sections. The first one will work as the current wallets we use. But it will be able to add local components to the coins and tokens in the second section of the wallet.

At the creation of the wallet, you’ll have to indicate a big town around you (from a list already defined). The GPS coordinates of the big city you chose will be definitively linked to your address inside the LEW.

When you decide to send coins and tokens from the first section to the second section, the GPS coordinates of your reference city will be added to the UTXOs.

And then, the coins and tokens of the second section will only be able to be spent through the LEW.

All transactions with the same GPS coordinates (same town, city, area…) have no fees (of course the transaction fees of the blockchain will be applied).
Transactions with different GPS coordinates will be operated with variable fees depending on the distance between the coordinates.

Then, it’s not interesting to use your coins and tokens in other economies than your local one. But what could be the incentives to use the second section of our wallet? In other words, is there incentives to add a local component to some of our coins and tokens ?

## Incentives
For each city inside our list, we will create a main city wallet. When a user wallet linked to a city ‘A’ will send coins to a wallet linked to a city B, the applied fees will be sent to the main city wallet.

When a main city wallet achieve a certain amount of value or time, all the coins will be redistributed to all the user wallets linked to the city (same GPS coordinates). UTXO model allows sending many coins and tokens to many wallets in only one transaction.

Therefore, when trades are made between 2 different local economies, a part of the value stays in the locality of the buyer. It is a way to decrease the pressure of the Global Economy and reward the wallets that use local currencies.

# How does the Local Economy Wallet work on Ergo Platform?
## Wallet usage
At the creation of a wallet  (or restoration of a standard wallet) with the Local Economy Wallet (LEW), it will display cities near your location and you’ll need to choose the one with which you interact the most.

Now, your Ergo Wallet address is definitively linked to this city when you use LEW. Next time you restore your ergo wallet on a new LEW, it won’t let you choose another city.

Indeed, a LEW database keeps a link between GPS coordinates of main cities and wallets. This database will offer access to anybody (e.g. from the blockchain) through API.

When an asset is sent from the first to the second section of the wallet, a local component is added to the UTXOs.

Actually, the wallet will perform a transaction (so it will cost 0.001 erg). The output boxes of this transaction will bring information in it registers:
    • R4: longitude of the city linked to the wallet 
    • R5: latitude of the city linked to the wallet 
    • R6: hashed code from LEW
    
Through the implementation of a guard script, the R6 information will forbid any other wallet than a LEW to spend the box.

## Perform a transaction
***Case 1:***
Bob wants to send coins to Alice. Their wallet are linked to the same city.

The transaction compares R4 and R5 between input boxes and output boxes which are the same ⇒ no fees are applied.

***Case 2:***
Bob wants to send coins to Alice. Their wallet is linked to two different cities.

The transaction compares R4 and R5 between input boxes and output boxes, which are different.

We can obtain the distance in meters between their cities through GPS coordinates thanks to the following formula:
<p align="center">$Distance = arc cos (sin ϕ_A*sin ϕ_B + cos ϕ_A * cos ϕ_B * cos d_λ)$</p>

<p>$d_λ: λ_B-λ_A$</p>
$ϕ_A:$ Latitude of City A </br>
$λ_A:$ Longitude of City A </br>
$ϕ_B:$ Latitude of City B </br>
$λ_B:$ Longitude of City B </br>

Then we calculate the % of fees. These fees will never be more than 10%:
<p align="center">$fees = Distance / 1,000,000$</p>
