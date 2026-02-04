# Cost-Efficient-Asset-Replacement-using-unsupervised-learning
## Problem Statement

Organizations operating under strict budget constraints often concentrate spend on a small number of high-cost assets that drive a disproportionate share of output. While these assets appear indispensable, their cost efficiency and long-term risk exposure are rarely evaluated relative to statistically comparable alternatives.

The core challenge is determining whether performance can be preserved while reducing cost and volatility. This requires moving beyond surface-level labels and identifying similarity based on multidimensional performance patterns rather than reputation, titles, or historical pricing.

This project addresses that challenge by using unsupervised learning and similarity modeling to identify cost-efficient asset substitutes, quantify concentration risk, and support decision-making under constrained resource environments.

## Why This Is a Data Science Problem

The problem cannot be solved using simple rules or static comparisons. Asset labels, titles, or categories often obscure how value is actually created, and traditional one-dimensional metrics fail to capture tradeoffs between volume, efficiency, and risk.

Identifying meaningful substitutes requires learning latent structure from data: understanding how entities contribute across multiple dimensions simultaneously, how those contributions relate to one another, and how stable those patterns are under uncertainty.

This project frames the challenge as a data science problem by:
- Representing each entity as a vector in a standardized feature space  
- Learning functional archetypes using unsupervised clustering rather than predefined labels  
- Measuring similarity based on contribution shape rather than raw scale  
- Evaluating robustness to distinguish structural patterns from statistical noise  

These techniques enable decision-making that balances performance preservation, cost efficiency, and risk exposure in constrained environments.
## Dataset Overview

The analysis uses season-level entity performance data collected from authoritative public sources and frozen into a structured dataset to ensure reproducibility.

Each row represents a single entity-season observation, enabling consistent comparison across time while avoiding short-term variance.

**Dataset characteristics:**
- Time range: 2014–2024  
- Unit of analysis: Entity per season  
- Observations: ~700 entity-seasons after filtering  
- Feature categories:
  - Volume & impact: points, assists, rebounds, steals, blocks, turnovers  
  - Efficiency: field goal %, three-point %, free throw %  
  - Context: age and team identifiers  

**Data preparation decisions:**
- Excluded entities with minimal participation to reduce small-sample bias  
- Deduplicated multi-team entries using season-total aggregates  
- Converted all numeric fields to consistent data types  
- Filled missing values conservatively prior to modeling  

These decisions prioritize structural signal and comparability over granular game-level variance.
## Methodology

The analytical approach combines unsupervised learning, vector similarity modeling, and robustness testing to move from raw performance statistics to decision-support insights.

### 4.1 Feature Engineering & Standardization

A focused set of nine performance features was selected to capture volume, efficiency, and defensive contribution. Because these features exist on different numeric scales, all numeric variables were standardized prior to modeling.

Standardization ensures that no single metric (e.g., scoring volume) dominates the analysis and allows defensive and efficiency signals to carry equal weight in downstream modeling.

### 4.2 Role Archetyping via Unsupervised Learning

K-Means clustering was applied to the standardized feature space to group entities into functional archetypes based on how they contribute rather than how they are labeled.

Clustering was used to:
- Identify role-level structure across the population  
- Separate high-usage, mid-usage, and low-usage contribution profiles  
- Enable comparison within roles rather than across fundamentally different contribution types  

Principal Component Analysis (PCA) was applied for dimensionality reduction and visualization, allowing inspection of cluster separation and overlap without altering the underlying clustering assignments.

### 4.3 Similarity Modeling

To evaluate substitution feasibility, cosine similarity was used to compare entities within the same archetype.

Cosine similarity measures the shape of contribution rather than absolute magnitude, making it well-suited for identifying lower-volume entities whose performance profiles mirror higher-volume peers. This distinction is critical for identifying cost-efficient substitutes rather than simply ranking top performers.

### 4.4 Robustness & Risk Analysis

To assess stability, controlled statistical noise was introduced into the standardized feature space and clustering was recalculated.

Entities that retained their cluster assignments were treated as structurally stable, while those that frequently shifted roles were flagged as borderline profiles with higher evaluation risk. This robustness testing helps distinguish persistent patterns from artifacts of sampling variability.
## Key Insights

1. **Output is highly concentrated across a small number of roles**  
A minority of entities account for a disproportionate share of total output, creating dependency risk when performance is tied to a narrow set of high-usage profiles.

2. **Cost and contribution are weakly aligned within roles**  
Within the same functional archetype, entities exhibit relatively similar performance patterns despite large differences in cost, indicating market inefficiencies not explained by output alone.

3. **Statistically comparable substitutes exist across cost tiers**  
Similarity modeling reveals multiple lower-cost entities that deliver 85–90% comparable contribution profiles to higher-cost peers, suggesting opportunities to preserve output while reducing spend.

4. **High-usage profiles exhibit elevated aging and volatility risk**  
Performance peaks earlier and declines more sharply for high-usage roles, while robustness testing shows that some contributors sit near role boundaries and are more sensitive to small performance shifts.

Together, these findings highlight opportunities to reduce concentration risk and improve capital efficiency without materially impacting aggregate performance.
## Decision Metrics & KPIs

The analysis is designed to support repeatable, data-driven decisions rather than one-off evaluations. The following metrics are used to quantify efficiency, risk, and substitution feasibility:

- **Performance Similarity Score**  
  Measures cosine similarity between entities within the same archetype to evaluate substitution feasibility independent of scale.

- **Role Distance / Volatility Indicator**  
  Captures how frequently an entity shifts archetype under small statistical perturbations, serving as a proxy for evaluation risk.

- **Usage Concentration Ratio**  
  Quantifies the share of total output generated by the highest-usage roles, highlighting dependency and concentration risk.

- **Aging Exposure Index**  
  Measures the proportion of total usage allocated to older entities, indicating vulnerability to performance decline.

These metrics allow decision-makers to monitor portfolio efficiency and risk over time rather than relying on isolated point-in-time comparisons.
## Generalization Beyond the Case Study

Although the demonstration uses NBA player data, the analytical framework is domain-agnostic and applicable to any environment where organizations must allocate limited resources across heterogeneous assets.

The mapping below illustrates how the concepts generalize:

| Case Study Concept | General Data Science Analog |
|-------------------|-----------------------------|
| Player            | Asset / Entity              |
| Salary            | Cost                         |
| Usage             | Demand                       |
| Role cluster      | Archetype                    |
| Similarity score  | Substitution feasibility    |
| Aging curve       | Lifecycle risk               |

This framework applies directly to problems such as:
- Identifying interchangeable suppliers or SKUs under cost pressure  
- Evaluating role redundancy in workforce planning  
- Optimizing spend across advertising or content portfolios  
- Managing risk concentration in constrained financial systems  

By separating contribution patterns from labels and pricing, the approach enables more robust, data-driven decisions across industries.
## Limitations & Next Steps

This analysis is intentionally scoped to prioritize structural insight over exhaustive modeling. Key limitations include:

- The analysis operates at the season level and does not capture short-term or game-level variance  
- Results are descriptive rather than causal and should not be interpreted as performance guarantees  
- Cost figures are treated as external context rather than modeled inputs  
- Injury history, scheme effects, and off-ball impact are not fully captured  

Future extensions could include:
- Multi-season validation to evaluate role stability over time  
- Supervised modeling to predict role transitions or similarity persistence  
- Integration of rate-based or possession-normalized metrics  
- Explicit incorporation of cost data to directly optimize efficiency objectives  

These extensions would further strengthen the framework for longitudinal and predictive decision support.
