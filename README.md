# Crypto Contract Compliance

A Claude skill that reviews crypto contracts for compliance problems. I built it while reviewing token deals at work. General contract-review skills aren't built for crypto, and Claude on its own often missed what a token deal needed, so I wrote down what a good review has to cover and turned it into a skill that anyone on the team can run.

It is not legal advice. It won't tell you a deal is "compliant" or "legal," and every review ends with questions for a lawyer. Have one look at anything before you sign it.

## What it reviews

Agreements that involve tokens:

- market making and liquidity provision
- token loans and custody
- managed trading with profit splits
- token-for-services deals
- launchpad and listing deals

For each one it answers two questions:

1. Would the deal, as written or as it will actually be run, break a law, a regulation or a binding platform rule?
2. If the counterparty breaks one, do the contract and your own conduct keep you out of it?

It looks at commercial terms such as price, impermanent loss and profit math only where they create compliance or liability exposure. For a full commercial review, run it alongside a general contract-review skill.

## How a review works

1. It confirms which side you're on (token issuer, market maker, custodian or investor) and writes every finding from that side. The same contract reads very differently from the other side.
2. It reads every page and lists the blanks to fill in before signing. Given a redline, it uses code to pull every tracked change and comment out of the Word file, and checks for edits that weren't tracked.
3. It asks only for the deal facts the document doesn't answer: the token and chain, who holds the keys at each stage, who decides trades, how everyone gets paid, which venues are involved, and who the parties are.
4. It explains the deal in plain words, with a table of who bears each risk: strategy losses, missing tokens, insolvency, token price, the token's legal status and a regulatory halt. It also checks whether the deal's label matches how it works, since a "loan" that functions like custody raises different licensing, bankruptcy and tax questions.
5. It checks the blockchain before trusting the counterparty's account: wallet history, funding sources, sanctions screening, the token's mint, freeze and upgrade powers, and who actually holds the liquidity positions.
6. It goes regulator by regulator (see the table below).
7. It works through a contract checklist. Each finding names the section, the gap and a fix, often with model clause language.
8. When trade data is available, it runs a wash-trading check in Python that looks for self-trades, trades between related wallets, quick round trips and volume spikes with a flat price. A flag is a question for the counterparty, not proof of manipulation.

## Regulators and rules it checks

| Regime | When it applies | What the skill looks for |
|---|---|---|
| SEC | The token is a security or is sold under an investment contract, or a party deals in, advises on or promotes securities | Promises of price support that could read as managerial efforts, token options for the market maker, profit shares that raise investment-adviser questions |
| CFTC | Most non-security tokens, for fraud and manipulation; registration questions once leverage or derivatives appear | A spot-only clause unless derivatives are intended |
| DOJ | Fraud, wash trading, pump-and-dump schemes, willful licensing violations | Bans on manipulation and fake volume, rules on information handling and personal trading |
| FinCEN | A party transmits value or holds tokens for others | A money-transmitter representation, tested against who actually controls the keys |
| OFAC | Always | Sanctions representations, screening of wallets and counterparties, termination for breach |
| FINRA | Only if someone involved is a member firm or registered person | Approvals for outside business activity and private securities transactions |
| FTC and promotion rules | Anyone promotes the token or the deal | Paid-promotion disclosures and influencer deals running alongside |
| IRS | Any token transfer or profit split | Whether the transfer is a loan or a disposition and how the split is reported, flagged for tax counsel |
| States | A party operates in or serves a state that licenses crypto custody or transmission | New York's BitLicense, California's Digital Financial Assets Law, state securities laws, UCC Article 12 |
| Exchanges | The token is listed or wants to be | Venue rules such as Binance's March 2026 market-maker rules, and whether the confidentiality clause allows required disclosures |
| Outside the US | A non-US party or venue | EU MiCA market-abuse rules; other countries' regimes researched on their own terms |

## The contract checklist

- Manipulation and fake volume, raised first: pay tied to price or volume, price targets, minimum volume commitments, trading timed to announcements
- Securities exposure for the issuer
- Custody, licensing and ownership, including who holds the liquidity position tokens and whether the client's tokens stay out of the provider's bankruptcy estate
- AML, KYC and sanctions
- Control and liability: who directs trading, early warning of investigations, pause and exit rights, indemnities
- Token and chain mechanics: forks, airdrops, migrations, freeze powers, bridges, transfer errors
- Settlement and valuation: time-weighted prices from several sources, a named stablecoin and a fallback if it depegs
- The counterparty itself: its real legal entity, governing law, emergency relief, key security and any AI-agent execution
- Side deals and earlier public promises to token holders
- Vague terms such as "commercially reasonable" or "mutually approved" at points where tokens can get stuck
- Steps outside the contract: communications and team trading policies, monitoring, a diligence file and insurance

## What you get back

A report in chat. It opens with your position, the counterparty, the deal type and an overall risk level, followed by the blanks to fill in and a short answer. Then come the deal in plain words with its risk table, on-chain findings with explorer links, and a regulatory map with one row per regime. Findings are sorted into must fix, should fix and fine as is, each with a suggested fix and how negotiable it is. The report ends with protections beyond the contract, questions for counsel and sources.

If you ask for redlines, it builds a tracked-changes Word file with a comment explaining every change. It can make two matching versions: an internal one with candid reasoning for you and your lawyer, and an external one with neutral comments for the other side.

## Safeguards built in

Several of these rules came from mistakes Claude made during real reviews.

- Every regulatory baseline is dated, and Claude has to check its current status against primary sources before relying on it.
- Every authority is labeled by type: statute, binding agency interpretation, final rule, proposed rule, staff statement, enforcement precedent or exchange rule. In crypto, much of what governs a deal is proposals, staff statements and exchange rules, and the label shows how much weight each one carries.
- Profit splits, impermanent-loss scenarios and payout tables are computed in code and re-run in full whenever an input changes.
- It keeps what the contract says, what is guaranteed and what a regulator could argue separate, and avoids "always" and "never" unless the text says so.
- When you challenge something it said, it re-reads the source and corrects itself plainly.
- It never concludes that a deal is compliant or legal.
- It won't help design wash trading, volume-for-hire, price-support schemes or structures meant to avoid required licenses.

The specific lessons are listed at the end of `SKILL.md`.

## Install

Download the repo (click Code, then Download ZIP), rename the unzipped folder to `crypto-contract-compliance`, and add it to Claude as a custom skill. It works best when Claude can search the web, to check the baselines, and run code, for redlines, numbers and the wash-trading check.

## Example requests

- "Review this market-making agreement. We're the token issuer."
- "Here's the counterparty's redline. What changed, and what should we push back on?"
- "We're the liquidity provider. What in this custody agreement could get us in trouble?"
- "Run the wash-trading check on this trade export."

## Keeping it current

The regulatory baselines in section 4 of `SKILL.md` are dated October 2026. Crypto rules change month to month, which is why the skill makes Claude check each one before relying on it.
