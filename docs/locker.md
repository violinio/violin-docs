# Token Locker
Our Token Locker allows users (typically DeFi projects) to deposit tokens into a specialized contract which only allows them to be withdrawn after a certain amount of time. For more details, visit [Locker](locker.md).
# Why Lockers?
## Soft rugs
One of the most common ways shady DeFi projects scam users is with so-called **soft rugs**. A soft rug refers to a project's dev team trashing the price of the native token in some way to abscond with the money. There are two typical ways for this to be executed: **first**, projects may simply *mint a large number of native tokens* and sell them; **second**, projects may initially set up a large liquidity pool (e.g. native/USDC) to attract funds, but then *redeem the pool shares* and sell all of their native tokens.

## Lockers to the rescue
To guarantee users are safe from the second type of scam, many projects deposit their LP tokens into a special type of smart contract called a "Locker". This contract will ensure that the project team **is unable to redeem their liquidity pool shares** until the lockup period has ended. Liquidity locking is an important part of protecting DeFi users and generally viewed as a signal of the devs' long-term commitment. 

?>Some projects may also choose to mint a certain number of tokens as a reward for their core team, but lock them for a certain amount of time to reassure users that they will not simply dump them


## Our contribution
**As our gift to the community, we offer projects the ability to lock tokens in a secure smart contract for free**. RugDoc encourages all DeFi projects to lock their initial native token liquidity and Violin's locker feature is our way to make sure this is available to every project, no matter the size.

# Violin Locker features
## Holding contracts
Our Locker **generates a separate contract every time users lock funds** for maximum security. By interacting directly with the smart contract, projects may choose to save some gas by depositing tokens directly into the Locker contract, but this may cause issues in rare cases (such as tokens that change balance on their own, see [Notes](#notes)).

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