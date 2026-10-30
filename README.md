# econ5200-lab09-ab-testing

# Diagnosing Experimental Failures in A/B Testing

## Objective

I worked through six common ways A/B tests go wrong and measured how much each one distorts the result.

## Methodology

- **CUPED debugging:** I found and fixed three bugs in an analyst's CUPED (variance reduction) code, then compared the variance reduction and standard error before and after.
- **Sample ratio mismatch (SRM):** I ran chi-squared tests on two experiments, one with 100,000 users and one with 20 million users.
- **Marketplace interference:** I simulated a marketplace where discounted buyers take inventory from the control group, then compared the naive A/B estimate of the average treatment effect (ATE) with the effect of rolling the discount out to everyone.
- **Bayesian A/B test:** I computed P(B > A) and the expected loss of shipping B, applied a ship rule, and checked the result with a permutation test.
- **Custom Bayesian function:** I wrote my own function for the Bayesian test and ran it on a test with four times the users.
- **Peeking simulation:** I ran 1,000 experiments with no true effect, checked each at 50 points, and counted how many crossed p < 0.05 at least once. I compared this with a single test at the end.
- **Challenge (LaLonde):** I applied CUPED to the LaLonde job training data, using re74 and re75 as covariates.

## Key Findings

| Topic | Result |
|---|---|
| CUPED bugs | The analyst reported 0.0% variance reduction. After my fixes it was 82.7%, and the SE fell from 0.1539 to 0.0641. |
| SRM, 100,000 users | A 0.6 pp imbalance gave chi-squared 14.4. |
| SRM, 20 million users | A 0.05 pp imbalance gave chi-squared 20. |
| Marketplace interference | The naive ATE was 0.1861, against 0.1428 for a full rollout. The naive estimate overstated the effect by -0.0433% |
| Bayesian test | P(B > A) = [P(B > A)], expected loss of shipping B = 0.000473, so the ship rule said [SHIP]. The permutation test gave p = 0.2302. |
| Bayesian test, 4x users | P(B > A) = [P(B > A) AT 4X USERS]. |
| Peeking |32.4% of experiments crossed p < 0.05 at least once, against 5.3% with a single test at the end.|
