# 🤲 Borrow

The space economy is usually described in three broad segments: the ground segment, the launch segment, and the in‑orbit or space segment:

1. Ground-segment covers ground station antennas, ground‑based compute and networking, launch‑site infrastructure, and related support systems at or near the surface.
2. Launch-segment focuses on vehicles like Falcon 9 or Electron and the infrastructure that gets payloads off the pad and into orbit.
3. Space-segment includes satellites and spacecraft operating above the Kármán line (around 100 km altitude) and the links that connect them.

Watchtower’s asset‑backed credit facilities are designed to ring‑fence risk at the hardware layer, so that specific classes of equipment can be underwritten, monitored, and financed faster than in traditional project‑finance workflows. As Watchtower progressively builds its tracking network to address in-orbit or space-segment assets, the initial focus is firmly on the ground segment, with an emphasis on Ground Station Antennas (GSAs), any compute such as GPUs and launch site equipment.

### Asset-Backed Tokenisation for Ground Station Antennas (GSAs)

Outside of T-bill products, most real-world-asset tokenisation models struggle when dealing with physical infrastructure such as ground station antennas and the teleports that host them, especially around enforcement, liquidation, and risk management for crypto‑native participants. A UCC Article 7–based offchain–onchain framework can solve this by enabling direct tokenisation, enforceable redemption, and embedded insurance for GSAs that sit inside teleports.&#x20;

Because of UCC Article 7 requirements for “documents of title,” the asset representation must remain strictly 1:1 with the underlying GSA and is therefore implemented as a compressed Non-Fungible Token (cNFT) Standard rather than a fungible token claim. Fungible representations are easier to trade, but their fractionalisation risk can introduce securities issues and make redemptions and title transfer much harder to enforce in the real world.

***

#### Why Use a cNFT Standard for GSAs <a href="#why-use-a-cnft-standard-for-gsas" id="why-use-a-cnft-standard-for-gsas"></a>

By treating each antenna as a distinct legal object with its own cNFT, tokenisation can respect physical uniqueness (location, specs, lease terms) while still plugging into DeFi rails for credit and secondary markets. With enforceable ownership, integrated insurance, and predictable redemption processes, tokenised GSAs can become a standardised, investable infrastructure class. Sectors such as satellite communications, spectrum‑intensive networks, and other telecommunication primitives can adopt this approach as a base layer before composing more complex on‑chain products on top.

#### From “Financial Product First” to “Asset Representation First” <a href="#from-financial-product-first-to-asset-representati" id="from-financial-product-first-to-asset-representati"></a>

Instead of starting with structured notes and then loosely tying them to off‑chain collateral, this model insists on robust, legally enforceable asset representation as step one. Once the GSA and its teleport context are properly modeled on‑chain, DeFi’s financial engineering (tranching, swaps, options, liquidity layers) can be composed safely on top of an auditable, enforceable base.&#x20;

Smart contracts then act as programmable wrappers around these GSA representations, creating liquid, composable exposure to ground infrastructure cash flows that would be difficult or impossible to package in legacy capital markets.&#x20;

The key is that investors ultimately hold claims on a clearly defined physical antenna, not just a synthetic index of opaque, off‑chain risks

***

#### Core Design Comparisons

**Ownership and Control**

<table><thead><tr><th width="131">Dimension</th><th>cNFT GSA representation</th><th>Typical fungible RWA setup</th></tr></thead><tbody><tr><td>Legal title</td><td>1:1 cNFT mapped to a specific GSA under UCC 7 or UCC 9</td><td>Indirect exposure via pooled claims</td></tr><tr><td>Control path</td><td>On‑chain transfer of document of title</td><td>Off‑chain legal steps, consents, or trust structures</td></tr><tr><td>Asset uniqueness</td><td>Encoded in cNFT metadata (location, specs, contracts)</td><td>Often abstracted away into homogenised tranches</td></tr></tbody></table>

Direct 1:1 ownership via cNFT keeps the link between token and antenna clear enough that a court, teleport operator, and token holder can all agree which physical unit is being referenced. By contrast, fungible token style pooling can blur this mapping and create conflict around which asset is being liquidated or redeemed in a stress scenario.

**Enforcement and Default Outcomes**

<table><thead><tr><th width="128">Dimension</th><th>cNFT + UCC 7 GSA model</th><th>Conventional secured lending</th></tr></thead><tbody><tr><td>Enforcement</td><td>On‑chain controlled repossession via title NFT</td><td>Court‑driven processes, restructuring, workouts</td></tr><tr><td>Timeline</td><td>Pre‑defined auction and redemption windows</td><td>Months or years for resolution</td></tr><tr><td>Transparency</td><td>On‑chain events for lien and transfer</td><td>Opaque negotiations and bilateral agreements</td></tr></tbody></table>

Because the cNFT is the recognised document of title under UCC Article 7 or 9, repossession can follow the token rather than requiring a separate, lengthy court process to identify and seise the antenna at the teleport. Auction logic, grace periods, and redemption rights can all be codified in smart contracts, creating predictable timelines for lenders and operators.

**Insurance and Operational Continuity**

<table><thead><tr><th width="129">Dimension</th><th>GSA cNFT teleports model</th><th>Ad‑hoc RWA insurance models</th></tr></thead><tbody><tr><td>Coverage structure</td><td>Warehouse/teleport‑level policies arranged by tokenising agent</td><td>Deal‑by‑deal, bespoke contracts</td></tr><tr><td>Operational continuity</td><td>Borrower continues operating GSA under bailment</td><td>Assets sometimes sidelined or encumbered heavily</td></tr><tr><td>Scalability</td><td>Standardised documentation per teleport location</td><td>Manual underwriting and fragmented coverage</td></tr></tbody></table>

The tokenising agent can arrange umbrella coverage at the teleport‑facility level, making it possible to scale to many antennas without onboarding a new policy for each financing. Meanwhile, the borrower retains day‑to‑day operational control of the antenna under bailment, so tokenisation does not interrupt revenue‑generating activities.

***

#### Key Stakeholders in a GSA Financing Stack

* Borrower
  * Owns one or more GSAs through a bankruptcy‑remote special purpose vehicle (SPV).
  * Generates revenue from multiple - downlink services, leasing capacity, or bundled ground‑segment contracts - at a time.
* Tokenising Agent
  * Specialised legal entity that converts a specific GSA into a cNFT and manages associated off‑chain documentation.
  * Maintains relationships with teleport operators, insurers, and auditors to keep the registry verifiable and enforceable.
* Teleport Operator
  * Owns or leases the physical teleport facility where GSAs are installed, providing power, connectivity, security, and environmental control.
  * Acts as physical custodian in the bailment chain, ensuring the underlying asset is maintained and accessible in line with contractual terms.
* Lenders and Capital Providers
  * Supply capital against cNFT‑backed collateral, often split into senior and junior tranches with different risk–return profiles.
  * Rely on transparent on‑chain data plus off‑chain reporting (service‑level, utilisation, uptime) to price risk.

***

### How Funds Flow Through the GSA Lifecycle <a href="#how-funds-flow-through-the-gsa-lifecycle" id="how-funds-flow-through-the-gsa-lifecycle"></a>

#### I. Tokenisation via Bailment at the Teleport <a href="#id-1-tokenization-via-bailment-at-the-teleport" id="id-1-tokenization-via-bailment-at-the-teleport"></a>

1. The borrower contributes one or more GSAs into a bankruptcy‑remote Special Purpose Vehicle (SPV) that is insulated from the borrower’s broader corporate liabilities.
2. The SPV signs a bailment agreement with the teleport operator that physically hosts the antennas, establishing the operator as bailee and the future cNFT holder as bailor.
3. The tokenising agent mints a cNFT token that functions as an electronic document of title under UCC Article 7, explicitly mapped to the specific GSA at that teleport.

This structure allows the borrower to keep operating the GSA—signing service contracts, managing satellite passes, and earning revenue—while still posting it as collateral on‑chain.

### II. Loan Origination Against the GSA cNFT <a href="#id-2-loan-origination-against-the-gsa-cnft" id="id-2-loan-origination-against-the-gsa-cnft"></a>

1. The borrower pledges the cNFT into a lending smart contract governed by agreed terms such as tenor, interest rate, and covenants.
2. Loan proceeds are disbursed in stablecoins to the borrower’s on‑chain address, which can be off‑ramped (via custodial partners such as Coinbase, FalconX and Anchorage) or recycled into additional infrastructure build‑out as needed.
3. The borrower services the loan through periodic payments (for example, monthly interest plus scheduled principal amortisation) drawn from GSA‑driven cash flows.

Because the cNFT remains locked as collateral, lenders have clear recourse to the underlying antenna if performance deteriorates or covenants are breached.

### III. Default Handling at the Teleport <a href="#id-3-default-handling-at-the-teleport" id="id-3-default-handling-at-the-teleport"></a>

If the borrower misses required payments beyond a defined grace period, a default event is triggered and enforcement logic begins.

1. The cNFT representing the GSA is moved into an on‑chain auction module, where bidding is open to pre‑qualified & vetted buyers due to export-control laws.
2. After the auction closes, the winning bidder receives the cNFT, gaining legal title and the right to step into the existing bailment and teleport arrangements.
3. The new owner can either physically assume operation of the antenna at that teleport or renegotiate hosting terms with the operator while continuing to serve satellite customers.

This keeps the GSA productive even through credit stress, aligning interests between lenders, operators, and end‑users of the ground segment.

### IV. Borrower Parent Bankruptcy <a href="#id-4-borrower-parent-bankruptcy" id="id-4-borrower-parent-bankruptcy"></a>

If the borrower’s parent entity enters bankruptcy, the SPV that holds the GSA and associated cNFT remains separate and insulated. Other creditors of the parent cannot collapse the SPV to seize the tokenised antenna, preserving the rights of cNFT‑backed lenders and simplifying the claim waterfall.

***

### UCC Article 7 vs Article 9 Considerations for GSAs <a href="#ucc-article-7-vs-article-9-considerations-for-gsas" id="ucc-article-7-vs-article-9-considerations-for-gsas"></a>

Not all GSA financings will be purely UCC Article 7 “document of title” structures; some will require layering in UCC Article 9 secured‑transaction mechanics. The right classification depends on how the interest in the antenna is structured and the type of control the lender receives over proceeds and use.

* Pure Article 7 GSA cNFTs
  * Appropriate where the token functions as an electronic document of title with a direct link to specific antennas at a teleport.
  * Emphasises control over the document itself and the right to recover the goods on default, rather than a broad security interest over general intangibles.
* Article 9‑Enhanced GSA Structures
  * Relevant when the financing adds features such as cross‑collateralisation, security interests in receivables from GSA capacity sales, or broader liens over related equipment at the teleport.
  * May require filing and perfection steps typical of secured lending, instead of the Article 7 regime governing the document of title.

For a portfolio of GSAs, some antennas may be financed on a straightforward Article 7 cNFT basis, while others—especially where lenders seek additional protection over revenue streams or bundled assets—will be structured with Article 9 security interests layered on top. Careful asset‑by‑asset analysis is therefore required so that each GSA’s legal treatment, perfection method, and enforcement path are correctly reflected in its on‑chain representation and associated documentation.
