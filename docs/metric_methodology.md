# Brady Analysis Project Evolution

# Methodology Evolution: From Basic Context to Context-Aware Metrics

## Background & Problem Statement

- limitations of traditional box score metrics
- why basic z-scores miss game context
- need for situation-aware performance measurement

## Literature Review

- EPA vs traditional stats
- success rate as consistency measure
- CPOE for skill isolation
- win probability for game context

## Proposed Methodology

### Data Filtering Criteria:

$$
Qualified\_Plays = \{p \in Plays : play\_type = "pass" \land rush\_attempt = 0 \land 0.1 \leq WP \leq 0.9 \land sack = 0 \land qb\_spike = 0 \land qb\_kneel = 0\}
$$

$$
Qualified\_QB = \{q : |Qualified\_Plays_q| \geq 250\}
$$

### Data Filtering Logic

- Play type: pass attempts only
- Game context: 0.1 ≤ WP ≤ 0.9 (eliminate garbage time)
- Meaningful plays: excludes spikes , kneels, sacks
- Volume threshold: ≥ 250 attempts per season

### Basic Metrics Calculation:

- EPA per play (expected value contribution)

$$
EPA\_per\_play = \frac{1}{n} \sum_{i=1}^{n} EPA_i
$$

- Success Rate (play-level consistency)

$$
Success\_Rate = \frac{1}{n} \sum_{i=1}^{n} Success_i
$$

- Air EPA (throwing value)

$$
Air\_EPA\_per\_play = \frac{1}{n} \sum_{i=1}^{n} Air\_EPA_i
$$

- CPOE (completion percentage over expected

$$
CPOE_{season} = \frac{1}{n} \sum_{i=1}^{n} (Completion_i - P(completion_i))

$$

- Interception rate (risk management)

$$
Interception\_Rate = \frac{\sum_{i=1}^{n} Interception_i}{n}
$$

### Z-Score Standardization:

$$
Z_{metric} = \frac{metric - \mu_{season}}{\sigma_{season}}
$$

### Composite Score:

$$
QB_{Composite} = 0.40 \cdot Z_{EPA} + 0.25 \cdot Z_{Success} + 0.20 \cdot Z_{CPOE} + 0.15 \cdot Z_{Air\_EPA} - 0.10 \cdot Z_{INT\_Rate}
$$

Weighting Rationale: 

- 40% EPA (comprehensive value measure)
- 25% Success rate (consistency reward)
- 20% CPOE (pure skill isolation)
- 15% Air EPA (throwing difficulty)
- -10% Interception rate (turnover penalty, account for mistakes)

### Value Above Replacement:

$$
QB_{VAR} = QB_{Composite} - P_{20}(QB_{Composite_{season}})
$$

- where $P_{20} \text{ represents the 20th percentile (replacement level) in each season}$

### Future Considerations:

- pressure situation adjustments
- target depth weighting
- clutch performance modifiers