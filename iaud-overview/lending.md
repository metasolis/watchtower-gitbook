# 🤝 Lending

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

The lending side is driven by a yield-generating stablecoin - **IAUD (**[1aud.md](../watchtower-stack/1aud.md "mention")**)** - and is designed into three (or more) general vaults: the genesis vault to mint and burn Watchtower’s stablecoin; a reserves vault and a set of yield-generating vaults on a portion of the reserves. The core PDAs for lending are related to users that mint Watchtower’s stablecoin specific for each vault, the oracle price feeds and management fees. The User State is common for borrow, lend and underwriting actors.
