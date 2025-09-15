# NFL Quarterback Performance Analysis: Context-Aware Metrics and Supporting Cast Evaluation

## Project Overview

This analysis develops a comprehensive framework for evaluating NFL quarterback performance while controlling for supporting cast quality. The methodology addresses limitations in traditional box score metrics by implementing context-aware performance measures and team-level supporting cast quantification.

## Research Question

**Primary:** Is Tom Brady's career success primarily attributable to individual quarterback skill, superior supporting cast quality, or a combination of both factors?

**Secondary:** How can quarterback performance be isolated from team context effects to enable fair cross-era and cross-team comparisons?

## Data Specifications

### Temporal Scope
- **Analysis Period:** 2011-2024 NFL regular seasons
- **Rationale:** Advanced metrics (CPOE, Air EPA) availability in nflfastR dataset
- **Sample Size:** 14 seasons × 32 teams = 448 team-seasons

### Data Source
- **Primary:** nflfastR play-by-play dataset
- **Coverage:** Complete regular season games only (`season_type == "REG"`)

## Part I: Quarterback Performance Metrics

### Data Filtering Criteria

**Qualified Plays:**
$$
Qualified\_Plays = \{p \in Plays : season\_type = "REG" \land play\_type = "pass" \land rush\_attempt = 0 \land 0.1 \leq WP \leq 0.9 \land sack = 0 \land qb\_spike = 0 \land qb\_kneel = 0\}
$$

**Qualified Quarterbacks:**
$$
Qualified\_QB = \{q : |Qualified\_Plays_q| \geq 350\}
$$

### Base Metrics Calculation

**Expected Points Added per Play:**
$$
EPA\_per\_play = \frac{1}{n} \sum_{i=1}^{n} EPA_i
$$

**Success Rate (Consistency):**
$$
Success\_Rate = \frac{1}{n} \sum_{i=1}^{n} Success_i
$$

**Completion Percentage Over Expected:**
$$
CPOE = \frac{1}{n} \sum_{i=1}^{n} (Completion_i - P(completion_i))
$$

**Air Expected Points Added per Play:**
$$
Air\_EPA\_per\_play = \frac{1}{n} \sum_{i=1}^{n} Air\_EPA_i
$$

**Interception Rate:**
$$
Interception\_Rate = \frac{\sum_{i=1}^{n} Interception_i}{n}
$$

### Z-Score Standardization

Season-specific normalization to account for league evolution:
$$
Z_{metric,s} = \frac{metric_{qb,s} - \mu_{metric,s}}{\sigma_{metric,s}}
$$

Where $s$ represents season, ensuring fair comparison across different competitive environments.

### QB Composite Score

$$
QB_{Composite} = 0.40 \cdot Z_{EPA} + 0.25 \cdot Z_{Success} + 0.20 \cdot Z_{CPOE} + 0.15 \cdot Z_{Air\_EPA} + 0.10 \cdot Z_{INT\_Rate}
$$

**Weighting Rationale:**
- **40% EPA:** Comprehensive value contribution measure
- **25% Success Rate:** Consistency and reliability indicator  
- **20% CPOE:** Pure completion skill isolation
- **15% Air EPA:** Throwing difficulty and arm talent
- **10% Interception Rate:** Risk management (reversed sign)

### Threshold Justification

**350+ Attempts:** Data-driven analysis of 502 QB seasons revealed:
- Eliminates small-sample bias (e.g., Ryan Tannehill 2022 anomaly)
- Captures ~18 quarterbacks per season
- Represents ~21 attempts per game (starter-level volume)
- Balances statistical reliability with inclusivity

## Part II: Supporting Cast Metrics

### Team-Level Approach Rationale

Individual player thresholds create artificial exclusions and fail to capture collective unit performance. Team-level aggregation eliminates volume threshold complexities while measuring the actual context quarterbacks experience.

### Rushing Unit Metrics

**Qualified Rushing Plays:**
$$
Rush\_Plays = \{p \in Plays : play\_type = "run" \land !is.na(rushing\_yards) \land !is.na(epa) \land 0.1 \leq WP \leq 0.9\}
$$

**Base Metrics:**
$$
Rush\_EPA = \frac{1}{n} \sum_{i=1}^{n} EPA_{rush,i}
$$
$$
Rush\_Success = \frac{1}{n} \sum_{i=1}^{n} Success_{rush,i}
$$

### Receiving Unit Metrics

**Qualified Receiving Plays:**
$$
Rec\_Plays = \{p \in Plays : play\_type = "pass" \land !is.na(receiver) \land !is.na(epa) \land 0.1 \leq WP \leq 0.9 \land sack = 0\}
$$

**Base Metrics:**
$$
Receiving\_EPA = \frac{1}{n} \sum_{i=1}^{n} EPA_{target,i}
$$
$$
Catch\_Rate = \frac{1}{n} \sum_{i=1}^{n} Completion_i
$$

### Defensive Unit Metrics

**Qualified Defensive Plays:**
$$
Def\_Plays = \{p \in Plays : play\_type \in \{pass, run\} \land !is.na(epa) \land 0.1 \leq WP \leq 0.9\}
$$

**Base Metrics (Lower = Better Performance):**
$$
Defense\_EPA = \frac{1}{n} \sum_{i=1}^{n} EPA_{allowed,i}
$$
$$
Defense\_Success = \frac{1}{n} \sum_{i=1}^{n} Success_{allowed,i}
$$

### Supporting Cast Z-Score Standardization

**Standard Metrics:**
$$
Z_{metric,s} = \frac{metric_{team,s} - \mu_{metric,s}}{\sigma_{metric,s}}
$$

**Defensive Metrics (Reversed):**
$$
Z_{def\_metric,s} = -1 \times \frac{metric_{team,s} - \mu_{metric,s}}{\sigma_{metric,s}}
$$

### Unit Composite Scores

**Rushing Unit:**
$$
Rushing_{composite} = \frac{Z_{Rush\_EPA} + Z_{Rush\_Success}}{2}
$$

**Receiving Unit:**
$$
Receiving_{composite} = \frac{Z_{Receiving\_EPA} + Z_{Catch\_Rate}}{2}
$$

**Defense Unit:**
$$
Defense_{composite} = \frac{Z_{Defense\_EPA} + Z_{Defense\_Success}}{2}
$$

### Overall Supporting Cast Composite

$$
Supporting\_Cast_{composite} = 0.30 \times Rushing_{composite} + 0.40 \times Receiving_{composite} + 0.30 \times Defense_{composite}
$$

**Weighting Rationale:**
- **40% Receiving:** Direct impact on QB performance and game outcomes
- **30% Defense:** Field position, game script, and situational context effects  
- **30% Rushing:** Play-action efficiency, defensive pressure relief

## Methodological Advantages

### Context-Aware Design
- **Garbage Time Exclusion:** 0.1 ≤ WP ≤ 0.9 filter removes non-competitive situations
- **Meaningful Play Focus:** Excludes administrational plays (spikes, kneels)
- **Season Normalization:** Accounts for rule changes and league evolution

### Statistical Rigor
- **Volume Thresholds:** Evidence-based minimum attempt requirements
- **Standardization:** Season-specific z-scores enable cross-era comparison
- **Team-Level Aggregation:** Eliminates individual player sample size bias

### Football Intelligence
- **Metric Selection:** Advanced metrics capture skill and context separation
- **Unit Weighting:** Reflects actual impact on quarterback performance
- **Situational Awareness:** Game context integration throughout framework

## Applications

This methodology enables:

1. **QB Performance Isolation:** Separating individual skill from team context
2. **Era-Adjusted Comparisons:** Fair evaluation across different seasons and rule sets
3. **Supporting Cast Quantification:** Objective measurement of non-QB team contributions
4. **Brady Analysis:** Specific evaluation of career success attribution factors

## Validation Framework

The methodology's effectiveness is validated through:
- **Face Validity:** Known elite seasons rank appropriately
- **Construct Validity:** Metrics capture intended performance dimensions  
- **Predictive Validity:** Correlation with team success while controlling for QB performance

## Implementation Notes

- **Regular Season Focus:** Eliminates playoff sample size inconsistencies
- **Complete Case Analysis:** Requires full data availability across all metrics
- **Reproducible Framework:** Documented methodology enables replication and extension