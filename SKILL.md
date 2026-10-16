---
name: "crypto-contract-compliance"
description: "Full compliance review of crypto contracts (market making, liquidity provision, token loans/custody, trading profit splits) against SEC, CFTC, DOJ, FinCEN, OFAC, FINRA, FTC, IRS, state and exchange rules. Use for any token deal."
---

# Crypto Contract Compliance Review

Reviews agreements involving tokens (market making, liquidity provisioning, token loans and custody, managed trading with profit splits, token-for-services, launchpad and listing deals) to answer two questions:

1. Would the deal, as written or as it will actually be run, break a law, regulation or binding platform rule?
2. If the counterparty breaks one, do the contract and the user's own conduct keep the user out of it?

Cover commercial terms (price, impermanent loss, profit math, caps) only where they create compliance or liability exposure. For a full commercial review, use the contract-review skill alongside this one.

This is issue-spotting, not legal advice, and no checklist covers every rule in every jurisdiction. Say so once, and end with what to take to crypto-experienced securities counsel.

## 1. Intake

- **Confirm which side the user is on**: token issuer/project, market maker/liquidity provider, custodian, or investor. Ask if this conversation doesn't say. Never carry the side over from an earlier deal or chat; the same person may review both sides of one negotiation. Write every finding from that side.
- **Read every page.** Collect blanks (effective date, token amount, entity details, transfer date) for a "fill in before signing" list.
- **Redlines (.docx with tracked changes):** extract changes programmatically, not by eye. Unpack the XML and list every insertion, deletion and comment with author and timestamp. Confirm the "reject all changes" text matches the prior draft exactly, which catches untracked edits. Flag odd metadata (e.g., changes attributed to the user's own name). Build a paragraph-level diff.
- **Deal facts.** Ask only for what the document doesn't answer:
  - token, chain, contract address, share of supply involved, current price and liquidity (record source and timestamp)
  - who holds keys at each stage: idle wallet, strategy wallets, pool positions
  - who decides trades, and what the client approves
  - compensation: fixed fee, profit split, token options or calls, retainer, volume- or price-linked bonuses
  - venues (named DEX pools, CEXs) and whether the token is listed or seeking listing on a CEX
  - leverage, margin, perpetuals or borrowing, if any
  - term, exit and return mechanics, settlement asset (token, SOL, which stablecoin)
  - each party's legal entity, state or country, and the individuals behind it
  - whether any party, affiliate or individual is a FINRA member firm or registered person, SEC/CFTC registrant, or licensed money transmitter
  - side agreements: token options, influencer or marketing deals, listing agreements
  - counterparty background: how long operating, how many similar deals

## 2. Map the deal in plain words

Write a short plain-language summary: what moves where, who controls it, who decides, how money is split, how it ends. Then a risk table:

| Risk | Falls on | Section |
|---|---|---|
| Strategy losses | | |
| Missing tokens (hack, lost keys, pool mechanics, bad trades, transfer errors) | | |
| Counterparty insolvency | | |
| Token price | | |
| Token's legal status | | |
| Regulatory halt or exchange blacklisting | | |

Classify the arrangement (loan, custody, managed account, service for a fee) and flag where the label and the mechanics disagree. Classification drives licensing (custody for others), bankruptcy treatment (owner vs. unsecured creditor) and tax (loan vs. disposition).

## 3. On-chain diligence

Check what the chain shows before relying on what the counterparty says. Record explorer links for every finding.

- **Counterparty history.** Look up its disclosed wallets and tokens it has handled before. Did their charts collapse after its deals ended? Do its wallets trade with each other?
- **Funding sources.** Trace where its wallets were funded from: mixers, flagged addresses, sanctioned entities (screen against the OFAC SDN list).
- **Token authorities.**
  - Solana: who holds mint authority and freeze authority; Token-2022 extensions such as transfer fees, transfer hooks, or a permanent delegate that can move anyone's tokens.
  - EVM: contract owner, upgradeable proxy, pause, blacklist and mint functions.
  - A retained freeze or pause power lets the issuer freeze the market maker's positions; a mint power dilutes. Both cut both ways.
- **Position ownership.** In concentrated-liquidity pools (e.g., Orca, Raydium, Meteora, Uniswap v3), each position is its own token (often an NFT). Whoever holds it controls the liquidity. "Tokens remain Client property" means little if the market maker's wallet holds the position NFT.
- **Holder picture.** Top-holder concentration, LP lock status, recent large transfers from treasury or team wallets.

## 4. Regulator-by-regulator check

Crypto rules change month to month. Before relying on any baseline below (dated October 2026), search for its current status, prefer primary sources (agency releases, Federal Register, DOJ and court filings) and major law-firm alerts, and record dates. Separate binding law, binding agency interpretations, proposals, advance notices and enforcement precedent.

For each regime: does it apply, what the contract must do about it, and what remains for counsel.

### A. SEC (securities)
- **Applies when** the token is a security, or is sold as part of an investment contract; or a party deals in securities as a business, advises others on them, or promotes them for pay.
- **Baseline (verify):**
  - SEC/CFTC joint interpretation (Mar 17, 2026; effective Mar 23, 2026) is a formal interpretation binding on both agencies, though a future administration could change it. Five categories: digital commodities, digital collectibles, digital tools, stablecoins, digital securities. A non-security token can still be sold subject to an investment contract when the issuer promises essential managerial efforts, and can later separate from it. Also covers airdrops, protocol mining and staking, and wrapping.
  - SEC staff statement (Feb 2025): meme coins as it defines them generally aren't securities, absent promises of profit from the issuer's efforts.
  - Proposed Regulation Crypto Assets (Aug 18, 2026; comments due Oct 20, 2026): offering exemptions (about $5M over four years; about $75M per 12 months) and a safe harbor once the issuer completes the managerial efforts it promised. Offering side only. Check whether adopted.
  - Innovation exemption order (Sept 17, 2026) for tokenized-securities venues.
  - If the token is a security: Exchange Act anti-manipulation (Section 9(a)(2), Section 10(b)/Rule 10b-5), dealer and broker registration, Section 17(b) anti-touting (paid promotion must disclose payment).
- **Check in the contract:** no promise by the issuer of price support, liquidity or "growing the token" that could read as a managerial-efforts promise; no such language in marketing; token options to the market maker flagged; a profit share for managing someone else's assets flagged for investment-adviser analysis.

### B. CFTC (commodities)
- **Applies when** the token is a non-security commodity (most tokens under the 2026 taxonomy), always for fraud and manipulation; registration questions arise once leverage, margin, perpetuals or managing others' derivatives trading are involved.
- **Baseline (verify):**
  - CEA Section 6(c)(1) and Rule 180.1 anti-fraud and anti-manipulation reach spot commodity markets even where no registration is required.
  - Listed spot crypto on CFTC-registered exchanges since Dec 2025.
  - Oct 5, 2026 advance notice (ANPRM) on Regulation Crypto Asset Transactions and Regulation Crypto Asset Markets for retail leveraged or margined crypto trading. No rule text yet; spot authority stays limited to fraud and manipulation.
  - CFTC enforcement volume has fallen sharply (reported roughly 80% decline, Oct 2026). Lower federal enforcement does not remove DOJ, state or private exposure.
- **Check in the contract:** spot-only clause (no leverage, derivatives, borrowing, perps) unless intended; if derivatives are intended, flag CTA/CPO and venue-registration questions for counsel.

### C. DOJ (criminal)
- **Applies when** there is fraud on investors, wash trading or pump-and-dump, or a willful licensing violation.
- **Baseline (verify):**
  - Wash trading is charged as wire fraud and conspiracy regardless of whether the token is a security. Operation Token Mirrors (Oct 2024) charged market makers (Gotbit, ZM Quant, CLS Global, MyTrade) and token issuers who paid them (Saitama, Robo Inu, VZZN). A second wave unsealed Mar 30, 2026 (N.D. Cal.) charged 10 people tied to Gotbit, Vortex, Antier and Contrarian, again built on FBI-created tokens. MyTrade's founder was fined in Aug 2026 after admitting its "Volume Support" service used wash-trading bots; the SEC filed a proposed final judgment against Gotbit in July 2026.
  - Lesson: the "project" asking for volume services may be the FBI, and issuers who pay for fake volume are defendants too.
  - DOJ memo "Ending Regulation by Prosecution" (Apr 7, 2025): priority on fraud that harms investors; regulatory violations such as unlicensed money transmission under 18 U.S.C. 1960(b)(1)(A)-(B) and BSA failures not charged absent willfulness; 1960(b)(1)(C) is outside that policy.
  - Tornado Cash developer Roman Storm was convicted (Aug 2025) of conspiracy to operate an unlicensed money-transmitting business; retrial on remaining counts was requested for about Oct 2026.
  - Insider trading in non-security tokens is charged as wire fraud. The Second Circuit vacated the first such conviction (Chastain/OpenSea, July 31, 2025), requiring the misused information to have commercial value to its owner. The theory is narrower, not dead; if the token is a security, Rule 10b-5 insider trading applies.
- **Check in the contract:** see section 5A; information-handling and personal-trading rules (section 5E).

### D. FinCEN and the Bank Secrecy Act
- **Applies when** a party accepts and transmits value for others or custodies tokens for others (FinCEN's 2019 guidance treats hosted wallet providers as money transmitters), which means MSB registration, an AML program, SARs and the Travel Rule.
- **Baseline (verify):** GENIUS Act (July 2025) treats permitted payment stablecoin issuers as BSA financial institutions; FinCEN/OFAC proposed the AML and sanctions program rule Apr 8, 2026, and a customer-identification rule followed in June 2026. Check finalization and effective dates if a stablecoin issuer is involved.
- **Check in the contract:** a clause saying a party "is not a money transmitter" doesn't make it so; test it against who controls keys. Require a representation on MSB registration or why none is needed.

### E. OFAC (sanctions)
- **Applies always.** Liability is strict; OFAC lists wallet addresses on the SDN list; its 2021 virtual-currency guidance expects a risk-based program (management commitment, risk assessment, internal controls, testing, training).
- **Check in the contract:** mutual sanctions representations; screening of parties, beneficial owners, wallets, counterparties and venues before transfer and on an ongoing basis; blocking and reporting procedure; immediate termination for breach.

### F. FINRA
- **Applies only when** a party, affiliate or individual involved is a FINRA member firm or registered person.
- **Baseline (verify):** the 2026 Annual Regulatory Oversight Report (Dec 9, 2025) has a "Member Firms' Nexus to Crypto" topic and flags outside business activities and private securities transactions tied to crypto businesses. Regulatory Notices 20-23 and 21-25 encourage firms to tell FINRA about crypto activities, including affiliates' and non-security crypto activities.
- **Check:** if anyone is registered, flag Rule 3270 (outside business activities) and Rule 3280 (private securities transactions) approvals, Rule 2210 for communications, and firm notification.

### G. FTC and promotion rules
- **Applies when** anyone promotes the token or the deal.
- **Baseline:** FTC Act Section 5 bars deceptive practices; the FTC Endorsement Guides require disclosure of material connections for paid promoters; SEC Section 17(b) requires disclosure of payment for promoting a security (Kim Kardashian's 2022 EthereumMax settlement); state consumer-protection laws apply too.
- **Check:** ask about influencer or marketing deals running alongside; no promotion timed to strategy activity; disclosures in every paid post.

### H. IRS and tax
- **Baseline (verify):** custodial brokers report 2025 sales on Form 1099-DA (gross proceeds) and add cost basis for covered assets acquired from Jan 1, 2026; Congress repealed the DeFi broker rule in April 2025.
- **Check:** flag for tax counsel whether the token transfer is a loan or a disposition, how the profit split is characterized and reported, and who issues forms. Don't opine.

### I. States
- **Money transmission and crypto licenses.** Many states license transmitting or custodying virtual currency for others (sources count them differently, and a few exempt it); a few have adopted the Money Transmission Modernization Act with its optional virtual-currency article. Check every state where a party operates or has customers.
- **New York.** BitLicense covers custody of virtual currency for others. NYDFS custody guidance (Sept 30, 2025) expects segregation, no use of customer assets for the custodian's own purposes, and no discretion beyond the customer agreement, which is hard to square with a custodian deploying tokens for a profit share.
- **California DFAL.** Since July 1, 2026, exchanging, transferring or storing digital financial assets with or on behalf of California residents requires a DFPI license, an application filed by that date and still pending, or an exemption. A California money transmitter license doesn't cover it. Final regulations took effect June 29, 2026. Check whether the counterparty is licensed or pending.
- **State securities and AGs.** Blue-sky laws apply unless preempted (proposed Regulation Crypto Assets would preempt only for its covered offerings). State attorneys general (e.g., New York's Martin Act) act independently of federal enforcement priorities.
- **UCC Article 12.** Adopted by more than 30 states including California and Delaware; New York's took effect June 3, 2026. Perfection by "control" (multisig arrangements can qualify) matters if tokens secure any obligation or if the user needs priority in an insolvency.

### J. Exchange and platform rules
Not law, but binding if the token is listed or wants to be.
- **Binance (Mar 25, 2026):** projects must disclose their market maker's identity, legal entity and contract terms; profit-sharing and guaranteed-return arrangements between projects and market makers are banned; token-lending agreements must state how borrowed tokens can be used. Binance flags selling against release schedules, one-sided trading and volume that doesn't move price, and may blacklist market makers.
- Check the current rules of every venue where the token trades or will list, and whether the contract's confidentiality clause allows the required disclosures.

### K. Non-US parties or venues
- **EU (MiCA Title VI):** bans insider dealing, unlawful disclosure of inside information and market manipulation for crypto-assets admitted to trading in the EU; anyone professionally arranging or executing transactions must have systems to prevent and detect abuse and report suspicious orders (Article 92). ESMA supervisory guidelines (Apr 2025).
- **Elsewhere:** research the local regime (e.g., UK FCA, Singapore MAS, Hong Kong SFC, Dubai VARA). Don't apply US analysis by default.

## 5. Contract checklist

For each item give: what the contract says (section number plus a short quote), the gap, and a fix with model language where useful. Adapt names, numbers and brackets in the model clauses.

### A. Manipulation and fake volume
Red flags. Raise these first. If the deal's real purpose is faking volume or supporting price, say so plainly and don't draft around it.
- pay or bonuses tied to volume or price; price targets, "floor", "support", "maintain above"
- minimum daily volume commitments; "volume support" packages or dashboards
- trading timed to announcements, promotions or token unlocks; selling against the release schedule
- one-sided liquidity that sells supply into rallies
- the client trading alongside the strategy (copy trading)

Normal for legitimate market making: spread, depth and uptime commitments on named venues, and disclaimers that price and volume aren't guaranteed.

Check for:
- express bans on wash trading, self-trades, circular or matched trades between related wallets, spoofing and layering, trading timed to promotions, and leverage or borrowing if spot-only
- a wallet registry the client can see, covering affiliates' and personnel's wallets
- trade-level reporting:
  > "Each monthly statement will include, in a machine-readable format, trade-level data for every Strategy transaction (time, venue, direction, size, price, counterparty address where available, and transaction hash), and [Provider] will provide the same data for any period on request."
- a records-review or audit right

### B. Securities exposure for the issuer
- No price-support language in the contract, announcements or marketing; describe the deal factually as liquidity provision. Look for a clause barring either side from advertising a floor, depth or price impact.
- Disclosure to holders: flag for counsel. A ban on "misleading liquidity" or a "false appearance of demand" can make disclosure matter; some exchanges now require it.
- Token options or discounted grants to the market maker: flag for securities counsel.

### C. Custody, licensing, ownership
- Licensing representation plus condition precedent:
  > "[Provider] represents that it holds every license, registration, and approval required to custody the [Tokens] and conduct the Strategy, or that none is required, and Client will not be required to deliver any [Tokens] until the counsel confirmation under Section [x] addresses that question. [Provider] will notify Client within one (1) business day if that status changes."
- A counsel-review condition naming the regimes (New York, California DFAL, other states, FinCEN MSB, securities, commodities, sanctions, tax), with token delivery tied to written sign-off.
- Ownership: tokens remain client property; segregated; no commingling, re-lending, pledging or rehypothecation; position NFTs held in a wallet the client controls or co-controls; express statement that tokens are not property of the provider's estate. In 2023 the Celsius bankruptcy court held that customer assets in Earn accounts belonged to the estate because of the terms of use, so wording decides this.
- Structural option: the client keeps tokens in its own multisig. A limited co-sign key on the idle wallet is a lock on property; co-signing trades makes the client look like it directed trading.

### D. AML, KYC, sanctions
Mutual KYC of entities and individuals before any transfer; sanctions screening (section 4E); ongoing representations; immediate termination for breach.

### E. Control, direction and liability
Regulators and plaintiffs ask who directed the trading. Check for:
- A roles clause:
  > "Client does not direct, approve, or control individual trades. Client's approval of Schedule B is limited to venues, position types, and risk limits. [Provider] is solely responsible for all execution decisions and their legality."
- Information flow: advance notice of trades gives the client insider-like information. Prefer after-the-fact reports plus a promise not to trade on strategy information. Remove copy-trading clauses.
- Compliance representations: compliance with securities, commodities, AML and sanctions laws and exchange rules; no investigations or enforcement against the provider, its officers or key staff (exceptions disclosed in writing before signing); written market-conduct and personal-trading policies with monitoring; annual certification.
- Early warning:
  > "[Provider] will notify Client within [3] business days of any subpoena, investigation, inquiry, enforcement action, or material litigation involving [Provider], its affiliates, or personnel that relates to market making, liquidity provision, or digital-asset trading, whether or not it concerns [Token]."
- Pause and exit: on client notice, the provider immediately stops opening or changing positions, except protective steps. Termination triggers: conduct breaches, an early-warning event, credible public allegations of fraud or manipulation, exchange blacklisting, insolvency, change of control, loss of a key person. Fixed return deadlines instead of "commercially reasonable" unwinds.
- A misconduct indemnity with a duty to defend, covering regulator and holder claims, allegations as well as proven violations, and conduct with other clients, outside the liability cap. Aggressive option: a founders' personal guaranty limited to fraud. If the user is the indemnifying party, watch for one-way, uncapped indemnities triggered by mere allegations.
- Fee forfeiture for the provider's share in any period with a violation; ask counsel whether the client's own profit from that period should be held back too.
- Names and logos: mutual consent. Confidentiality carve-outs for regulators, legal requirements, exchange disclosure requirements and holder disclosure.

### F. Token and chain mechanics
- Forks, airdrops, migrations, redenominations and chain halts: who gets airdrops and staking rewards earned by tokens in custody; how a migration to a new contract is handled; what happens to deadlines if the chain halts mid-unwind.
- Token authorities found in section 3: require notice before any use of freeze, pause, mint or upgrade powers that affects positions.
- Bridges and wrapped tokens: whether the provider may bridge or wrap, and who bears bridge risk.
- Transfer errors and address poisoning: who bears the loss if tokens go to a wrong or spoofed address; require address allowlists and test transfers.

### G. Settlement and valuation
- Thin tokens are easy to push around at one moment. Use a time-weighted average price over a stated window across several named sources, not one spot price.
- Name the settlement stablecoin and chain, and a fallback if it depegs. Stablecoin issuers can freeze addresses.

### H. Counterparty, security and enforcement
- Identify the real legal entity and the individuals behind it; flag offshore or anonymous teams.
- Tokens move in seconds: check governing law, forum or arbitration seat, service of process, and whether emergency relief (emergency arbitrator, injunctions or asset-freeze orders) is available.
- Key security: multisig threshold, notice of signer changes, hack or loss notice within hours, a crime policy that covers digital-asset theft (or disclosure of what insurance exists).
- Automated or AI-agent execution: logs, human oversight, notice of changes to the agent's code or parameters, and a kill switch.

### I. Side deals and prior promises
- Loan plus call option structures: strike price, exercise window, caps, and whether the option rewards pumping and dumping.
- Influencer or marketing agreements running alongside (section 4G).
- Prior public statements to holders (locked treasury, team lockups, tokenomics) that lending or moving tokens would contradict.
- Wallets are public: confidentiality can't hide the market maker's on-chain activity, so plan communications.
- Exchange disclosure rules (section 4J) vs. the confidentiality clause.

### J. Vague terms that become compliance gaps
- Items left to be "mutually approved" with no fallback (pools, valuation source, payout events, deductible costs, forks and migrations) may be unenforceable agreements to agree.
- Soft standards ("promptly", "material", "commercially reasonable", "regulatory concern") at points where assets can get stuck: replace with deadlines.
- Disclaimers that contradict the mechanics, such as "not a custodian" while holding keys.

### K. Beyond the contract
List practical steps for the user's side:
1. Communications policy: no price-support language; never time announcements to strategy activity.
2. Team trading policy: no trading during the deal, or pre-clearance only; a list of who knows about approvals.
3. Monitoring with a paper trail: run the check in section 6 monthly; use the pause right on red flags; keep notes.
4. Diligence file on the counterparty: on-chain findings (section 3), background and regulatory searches, written answers about regulatory history, references.
5. Corporate hygiene: board resolution; officers sign only in their official capacity; separate company and personal wallets.
6. Insurance: check whether D&O and E&O policies cover regulatory investigations; many exclude crypto.

## 6. Wash-trading check

When trade-level data is available, run a check in code instead of eyeballing it. Adapt column names to the data:

```python
import pandas as pd
t = pd.read_csv("trades.csv", parse_dates=["time"])   # time, venue, side, size, price, wallet, counterparty, tx_hash
registry = set(open("provider_wallets.txt").read().split())

self_trades = t[t.wallet == t.counterparty]
related = t[t.wallet.isin(registry) & t.counterparty.isin(registry)]

# round trips: the same two wallets trade in opposite directions within 10 minutes
t["pair"] = [tuple(sorted([str(a), str(b)])) for a, b in zip(t.wallet, t.counterparty)]
t = t.sort_values(["pair", "time"])
g = t.groupby("pair")
prev_side, prev_time = g.side.shift(), g.time.shift()
round_trips = t[prev_side.notna() & (t.side != prev_side) & (t.time - prev_time <= pd.Timedelta("10min"))]

# volume spikes with flat price, hourly
h = t.set_index("time").sort_index().resample("1h").agg({"size": "sum", "price": ["first", "last"]})
h.columns = ["vol", "p0", "p1"]
h["move"] = (h.p1 / h.p0 - 1).abs()
flat_spikes = h[(h.vol > h.vol.rolling(24, min_periods=6).median() * 5) & (h.move < 0.005)]

for name, df in [("self", self_trades), ("related", related), ("round_trips", round_trips), ("flat_spikes", flat_spikes)]:
    print(name, len(df))
```

Report counts and examples with transaction hashes. A flag is a question for the counterparty, not proof of manipulation.

## 7. Numbers

Compute every profit split, impermanent-loss scenario, matched-capital figure and payout illustration in code. Show inputs (price, source, timestamp) and label results as illustrations, not forecasts. When an input changes, re-run the whole table instead of patching cells.

## 8. Calibration

- Separate what the contract says, what is guaranteed, and what a regulator could argue. Avoid "always", "never" and "guaranteed" unless the text says so, and cite the section.
- Label each authority: statute, binding agency interpretation, final rule, proposed rule, advance notice, staff statement, enforcement precedent, exchange rule.
- Never conclude a deal "is compliant" or "is legal". Say what the risks are and what counsel should confirm.
- When the user challenges an earlier statement, re-read the source and correct it plainly.

## 9. Output

Default, in chat:

- **Header:** your position · counterparty · deal type · risk level (🔴/🟡/🟢) · status (draft or signed, pages read)
- **Fill in before signing:** the blanks
- **Short answer:** 2-4 sentences
- **Deal in plain words** plus the risk table
- **On-chain findings** with explorer links
- **Regulatory map:** | Regime | Applies? | Why | What the contract does | Gap | Source |  (one row per section 4 regime; mark "not applicable" with the reason rather than dropping it)
- **Findings by severity:** 🔴 must fix · 🟡 should fix · 🟢 fine as is. Each with section, issue, fix (model language) and negotiability (high/medium/low).
- **Protections beyond the contract**
- **Questions for counsel**
- **Sources**

Redlines, when asked:
- Build a tracked-changes .docx (use the docx skill) with an anchored comment on every change explaining why.
- Offer two synchronized versions with identical contract text: INTERNAL (candid rationale, risk view, likely counterparty objections; for the user and counsel only) and EXTERNAL (neutral comments and softened headings). Generate both from one spec script, and before delivering, search the external file for internal-only wording.
- When the user wants a draft the counterparty will sign, trim aggressive extras first (fee forfeiture, flat licensing reps, required insurance, long post-settlement trading bans; convert reps and insurance to disclosure duties) and keep the core protections the user names as must-haves.
- Recommend counsel review the external version before it goes out.

## Lessons from use

These came from reviewing real token deals with this skill's earlier versions.

- Drafts that move from "loan" to "custody" wording can raise state licensing and FinCEN money-transmitter questions even while the draft says the provider is not a money transmitter. Test the label against who holds the keys (sections 2 and 4D).
- The same redline read from the counterparty's side gives opposite findings. That is why step 1 confirms the side, and why a pass from the other side is a useful stress test before sending a draft.
- A profit table drifted out of sync across turns (section 7).
- An "always" claim about capital return had to be walked back (section 8).
- The March 2026 SEC/CFTC interpretation was once described as non-binding when it binds both agencies, and Binance's March 2026 ban on project and market-maker profit sharing was missed. Both were already public. Section 4 now requires checking each authority's current status, and section 4J covers exchange rules.

## Guardrails

- Don't help design wash trading, volume-for-hire, price-support schemes or structures meant to avoid required licenses. Decline that part and explain the exposure.
- Recommend crypto-experienced counsel review before anything is signed or sent.