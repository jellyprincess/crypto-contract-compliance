# Crypto contract compliance (Claude skill)

A Claude skill for issue-spotting in crypto contracts: market making, liquidity provision, token loans and custody, managed trading with profit splits, token-for-services, and launchpad and listing deals. It checks a draft against SEC, CFTC, DOJ, FinCEN, OFAC, FINRA, FTC, IRS, state and exchange rules, then lists the questions to take to a lawyer.

This is not legal advice and does not replace a lawyer. The skill never concludes that a deal is "compliant" or "legal."

## Using it

This repository is the skill folder. Download it as a folder named `crypto-contract-compliance` (it holds `SKILL.md`) and add it to Claude as a custom skill. Then ask Claude to review a token deal. It will confirm which side you are on before it starts.

## Keeping it current

The regulatory baselines in section 4 are dated October 2026. Crypto rules change month to month, so the skill tells Claude to check each one's current status against primary sources before relying on it.
