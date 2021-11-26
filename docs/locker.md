# Token Locker
Our Token Locker allows users (typically DeFi projects) to deposit tokens into a specialized contract which only allows them to be withdrawn after a certain amount of time. Read on for reaons why this is done and how you can lock your own tokens with us.
# Why Lockers?
## Soft rugs
Lockers are an effective method to combat one of the most common scams in defi, the soft rug. There are a few ways projects can go about this method of scam, but Lockers can help to negate a couple of these methods directly: the liquidity pull and the dumping of native tokens. The liquidity pull refers to a project withdrawing the liquidity of their native token and redeeming it, most often after the project has gained some traction and the pool has grown since their intial contribution. The dumping of native tokens refers to instances where a project has minted a large portion of their native token to themselves/their team members. Then when the token price has risen due to price action, they will either dump en masse in a large sell off, tanking the price, or they will sell in smaller sustained portions which generally does not allow the token price to recover.  

## Lockers to the rescue
To help guarantee users safety, many projects deposit their LP/Native tokens into a special type of smart contract called a "Locker". Lockers help solve both of the aforementioned rug methods with a very simple mechanic: the team locks the liquidity tokens or the native token in Violin lockers and therefore cannot access them for means of sell offs.

!>Disclaimer: Please bear in mind that though we are using our tools and knowledge to best combat these rug methods, nothing is foolproof and everything in Defi carries inherent risk. You are always responsible for your own financial decisions and doing your own due diligence. 

## Our contribution
**As our gift to the community, we offer projects the ability to lock tokens in a secure smart contract for free**. RugDoc encourages all DeFi projects to lock their initial native token liquidity and Violin's locker feature is our way to make sure this is available to every project, no matter the size.

# Violin Locker features
## Holding contracts
For maximum security, our Locker **generates a separate contract to hold the tokens every time users lock funds**. By interacting directly with the smart contract, projects may choose to save some gas by depositing tokens directly into the Locker contract, but this may cause issues in rare cases (such as tokens that change balance on their own, see [Notes](#notes)).

?> Note that these contracts will be unverified but Violin will verify at least one, so most chain explorers will find matching byte code. You can also check the vault contract to verify the holding contracts will not lead to loss of funds. Always check either the frontend or the vault contract to ensure the holding contract was created by Violin and to figure out the actual unlock time
## Lock share NFT
After the tokens are locked in our contract, you will receive an ERC-721 NFT token to represent the locked funds. This NFT can be transferred to other wallets or sold if desired — a transfer of the token does not unlock funds, but **whoever holds the NFT is the only person who can withdraw the locked tokens once they are released**. The NFT is burned upon withdrawal.

!>**Do not burn or lose your NFT.** If this happens, it will be *impossible* to withdraw the locked tokens, ever
## Governance Unlock
When locking tokens, projects may choose to allow RugDoc to prematurely release their funds before the lockout period is over. **This can only be executed by RugDoc herself on request**, and such requests are only granted after a careful review of the  projects' individual circumstances (e.g. if they have to re-deploy due to a bug but already locked liquidity).

?>Governance can never withdraw tokens to their wallet, **the only account which can withdraw funds (after they were unlocked) is the [NFT](#lock-share-nft) holder**

For even more security, users who are certain they will not need the premature unlock may forgo this emergency net and lock without a governance override, or renounce the governance override later.

## Important Notes
* Do not burn or lose your Locker NFT, only the NFT holder can withdraw the locked tokens.
* We recommend not locking any tokens which may **change balance on their own** (reflection tokens, certain algorithmic stablecoins etc.). LPs containing those tokens will work fine, unless of course the LP token itself also changes its balance.
* Verify that the contract you interact with matches the one listed on [this page](contracts.md) for your blockchain when locking tokens.
* You can only withdraw the full amount you locked, **there are no partial withdrawals.**
* You **cannot interact directly with the holding contract**, only the vault can interact with it for the purpose of withdrawing funds.