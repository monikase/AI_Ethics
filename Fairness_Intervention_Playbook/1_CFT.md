# Causal Fairness Toolkit

---

## Implementation Framework
To systematically construct causal models for bias detection, follow this structured methodology:

### 1. Variable Identification and Classification:

- Identify protected attributes relevant to your fairness concerns (e.g., race, gender, age).
- Specify outcome variables representing decisions where fairness matters (e.g., loan approval, hiring recommendation).
- Identify potential mediators through which protected attributes might influence outcomes (e.g., education, test scores).
- Determine possible confounders that affect both protected attributes and outcomes (e.g., neighborhood characteristics, socioeconomic factors).
- Categorize each variable according to its role in the causal structure and document the reasoning.

### 2. Causal Relationship Mapping:

- Draw on domain knowledge to determine direct causal relationships between variables.
- Consult with subject matter experts to validate proposed relationships.
- Review relevant literature and research findings supporting causal connections.
- Consider temporal ordering to ensure causality (causes must precede effects).
- Document evidence supporting each proposed causal relationship.

### 3. Formal Model Development:

- Create a directed acyclic graph (DAG) representing the causal structure.
- Specify structural equations for each variable based on its direct causes.
- Determine functional forms for relationships based on domain knowledge.
- Implement the model using appropriate causal modeling tools.
- Document model assumptions and limitations clearly.

### 4. Model Validation:

- Test implied conditional independencies against observational data.
- Perform sensitivity analysis to assess robustness to assumption violations.
- Compare model predictions with established findings in the domain.
- Seek expert review of model structure and assumptions.
- Iteratively refine the model based on validation results.

---

## Implementation Challenges
When constructing causal models for bias detection, practitioners commonly face these challenges:

### 1. Limited Domain Knowledge: 
Accurate causal modeling requires substantial domain expertise, which might be incomplete or evolving.   
Address this by:

- Adopting an iterative approach that evolves the causal model as knowledge improves.
- Constructing multiple candidate models representing different causal hypotheses.
- Collaborating with diverse domain experts to capture different perspectives.
- Being explicit about uncertainty in the model and conducting sensitivity analysis.

### 2. Unobserved Confounders:  
Critical confounding variables might be unmeasured in available data.  
Address this by:

- Conducting sensitivity analysis to assess how unobserved confounding might affect conclusions.
- Using domain knowledge to identify potential unmeasured confounders.
- Leveraging techniques like instrumental variables or proxy variables when appropriate.
- Explicitly documenting potential unobserved confounders and their implications for model validity.

Successfully implementing causal modeling for bias detection requires resources including domain expertise to inform model construction, data to test implied relationships, technical knowledge of causal modeling techniques, and organizational commitment to addressing bias based on causal understanding.


---

## Evaluation Approach

To assess whether your causal models effectively represent bias mechanisms, implement these evaluation strategies:

### 1. Structural Validation:

- Test implied conditional independencies (d-separation properties) derived from the causal graph.
- Measure the strength of associations along different causal pathways.
- Assess whether temporal sequences in data align with the proposed causal ordering.
- Document validation evidence for key causal relationships in the model.

### 2. Functional Validation:

- Evaluate whether structural equations accurately predict relationships observed in data.
- Measure goodness-of-fit for equations representing key relationships.
- Assess sensitivity of model predictions to parameter variations.
- Test whether interventions produce expected downstream effects according to the model.

These evaluation approaches should be integrated with your organization's broader fairness assessment framework, providing deeper insights than purely statistical metrics while acknowledging the limitations of causal knowledge in practical applications.

---

## Application Guidance
To apply these causal modeling techniques in practice:

- Start by systematically identifying and classifying variables relevant to your fairness analysis, ensuring you include protected attributes, outcomes, potential mediators, and confounders.
- Draw on domain expertise, existing research, and data analysis to construct causal graphs representing how these variables relate to each other, paying particular attention to pathways from protected attributes to outcomes.
- Formalize your causal understanding through structural equations that specify the functional relationships between variables, enabling more precise analysis and intervention design.
- Validate your causal models through conditional independence testing, sensitivity analysis, expert review, and comparison with established domain knowledge, iteratively refining them based on validation results.

---

## Counterfactual Fairness

Counterfactual fairness provides a formal mathematical definition of fairness based on causal reasoning: a prediction is counterfactually fair if it remains unchanged in counterfactual worlds where an individual's protected attributes are different, but all variables not causally dependent on those attributes remain the same. 

Would this individual receive the same prediction if their protected attributes were different but all other causally independent factors remained the same?  
Traditional fairness metrics like demographic parity or equal opportunity operate purely on statistical outcomes without considering the underlying causal mechanisms.  
Counterfactual fairness provides a more principled approach by explicitly modeling how protected attributes influence outcomes through various causal pathways. 

Formally, Kusner et al. (2017) define counterfactual fairness as follows: A prediction Ŷ is counterfactually fair if:  

P(Ŷ₍A←a₎(U) = y | X = x, A = a) = P(Ŷ₍A←a′₎(U) = y | X = x, A = a)   

Where A represents protected attributes, X represents observed features, U represents unobserved background variables, and the notation Ŷ₍A←a′₎(U) represents the counterfactual prediction if the protected attribute had been a' instead of a.  

### Structural Causal Models for Counterfactuals

Structural causal models (SCMs) provide the mathematical foundation for generating and evaluating counterfactual scenarios. These models enable us to simulate "what if" scenarios by intervening on protected attributes while preserving the appropriate relationships between other variables.  

It interacts with the counterfactual fairness definition by providing the computational framework for determining whether a model satisfies this criterion.  

An SCM consists of:  

- A set of exogenous (background) variables U
- A set of endogenous (observed) variables V
- A set of structural equations F that determine how each endogenous variable depends on other variables
- A probability distribution P(U) over the exogenous variables


Following Pearl's framework (2009), counterfactuals are computed in three steps:

1. Abduction: Update the probability distribution of exogenous variables based on observed evidence  
2. Action: Modify the structural equations to implement the intervention (e.g., setting the protected attribute to a different value)  
3. Prediction: Compute the resulting distribution of the target variable

### Path-Specific Counterfactual Fairness

Path-specific counterfactual fairness refines the basic counterfactual framework by distinguishing between fair and unfair causal pathways from protected attributes to outcomes. This nuanced approach recognizes that not all influences of protected attributes constitute discrimination—some causal pathways may represent legitimate relationships that should be preserved.  

Example: For example, in educational settings, gender might influence subject preference, which legitimately affects performance in certain courses. A path-specific approach could allow this influence while blocking pathways where gender affects how the same performance is evaluated.   

The key insight is that fairness judgments ultimately require normative decisions about which causal pathways constitute legitimate influence versus discrimination—decisions that must be made based on ethical principles and application-specific context rather than purely technical considerations.  

### Implementing Counterfactually Fair Models

Implementing counterfactually fair models requires specific techniques for training models that satisfy counterfactual fairness criteria.  


Kusner et al. (2017) proposed several approaches for implementing counterfactually fair models:

- **Fair representation learning:** Transform the data to remove the influence of protected attributes along unfair pathways while preserving other information.
- **Causal inference-based approaches:** Estimate the true causal effects in the data and use these to build models that explicitly control for unfair influences.
- **Constrained optimization:** Train models with explicit counterfactual fairness constraints during the optimization process.

These implementation approaches often involve trade-offs between counterfactual fairness, model complexity, and predictive performance. Research by Chiappa et al. (2020) demonstrated that in many cases, counterfactually fair models can achieve comparable accuracy to unconstrained models when properly implemented, challenging the notion that fairness necessarily comes at a significant cost to performance.   

### Evaluating Counterfactual Fairness

Evaluating counterfactual fairness means checking whether a model treats people fairly in hypothetical “what if” scenarios and measuring how much it may violate fairness.  

This step is important because it shows whether fairness interventions are actually working and helps improve them over time.  

Black et al. (2020) proposed several metrics for evaluating counterfactual fairness:

- **Counterfactual Effect Size:** Measures the average difference in predictions between factual and counterfactual worlds.
- **Counterfactual Fairness Violation Rate:** The proportion of instances where counterfactual predictions differ from factual ones by more than a specified threshold.
- **Path-Specific Effect Metrics:** Measure the influence of protected attributes along specific causal pathways.

### Intersectionality Consideration

Counterfactual fairness approaches must be extended to address intersectional concerns, where multiple protected attributes interact to create unique patterns of discrimination.  

Recent work by Yang et al. (2020) has extended counterfactual fairness to address intersectionality by developing techniques for:

1. **Intersectional Counterfactual Queries:** Formulating counterfactual questions that change multiple protected attributes simultaneously to evaluate their joint effects.
2. **Compound Pathway Analysis:** Identifying causal pathways that specifically affect individuals at certain intersections, such as pathways that uniquely impact women of color.
3. **Intersectional Fair Representations:** Learning data representations that remove unfair influences along pathways affecting intersectional groups.

For our Causal Analysis Methodology, addressing intersectionality requires:

1. Explicitly modeling interactions between protected attributes in causal graphs
2. Formulating counterfactual queries that examine combinations of protected attributes
3. Identifying causal pathways that specifically affect intersectional groups
4. Developing evaluation measures that capture intersectional counterfactual fairness

### Implementation Framework

#### 1. Counterfactual Fairness Analysis:
- Formulate specific counterfactual queries relevant to your application: "Would this prediction change if the individual's protected attributes were different?"
- Identify which causal pathways should be considered fair versus unfair based on domain knowledge and ethical principles.
- Compute counterfactual predictions using the causal model for different protected attribute values.
- Measure disparities between factual and counterfactual predictions to quantify counterfactual unfairness.
- Document fairness violations with specific examples and patterns discovered.

#### 2. Path-Specific Analysis:

- Decompose the total effect of protected attributes into path-specific components.
- Classify these pathways as fair or unfair based on domain expertise and ethical considerations.
- Quantify the contribution of each pathway to observed disparities.
- Identify the most problematic pathways that require intervention.
- Document the rationale for pathway classifications with stakeholder input.

#### 3. Intervention Design:

- Select appropriate intervention approaches based on the specific counterfactual fairness violations identified:
- For data-level issues: Transform features to remove unfair influences while preserving legitimate information.
- For model-level issues: Modify the learning objective to incorporate counterfactual fairness constraints.
- For post-processing: Adjust predictions to satisfy counterfactual fairness criteria.
- Implement the selected interventions while monitoring their effect on both fairness and performance metrics.
- Iterate on intervention design based on evaluation results.

### Implementation Challenges
When implementing counterfactual fairness approaches, practitioners commonly face these challenges:  

1. **Uncertainty in Causal Models:** Counterfactual fairness relies on accurate causal models, but perfect causal knowledge is rarely available. Address this by:

- Conducting sensitivity analysis to determine how robust your counterfactual conclusions are to variations in causal assumptions.
- Developing multiple plausible causal models based on different domain expertise and testing counterfactual fairness under each.
- Being transparent about causal assumptions and their limitations in documentation.
- Using data-driven approaches to validate causal structures where possible.

 2. **Balancing Counterfactual Fairness and Model Performance:** Strictly enforcing counterfactual fairness constraints may significantly impact predictive performance. Address this by:
- Implementing path-specific approaches that only block unfair pathways, preserving legitimate predictive relationships.
- Developing relaxed notions of counterfactual fairness that allow for small violations when justified.
- Making explicit the trade-offs between different objectives and establishing acceptable thresholds.
- Exploring whether the prediction task itself needs reformulation if fairness and performance seem fundamentally at odds.

### Evaluation Approach
To assess whether your counterfactual fairness implementation is effective, apply these evaluation strategies:

1. **Counterfactual Disparity Measurement:**
- Calculate the average difference between factual and counterfactual predictions across the dataset.
- Measure the proportion of instances where predictions change under counterfactual scenarios.
- Compute confidence intervals for these measures to account for statistical uncertainty.
- Compare these measures across different demographic subgroups to identify patterns in counterfactual unfairness.

2. **Path-Specific Effect Evaluation:**
- Decompose total counterfactual effects into contributions from different causal pathways.
- Measure the magnitude of effects along pathways classified as unfair.
- Compare these effects before and after interventions to assess improvement.
- Validate that legitimate predictive pathways are preserved while unfair ones are mitigated.


### Application Guidance
To apply these concepts in your practical work:

1. Start by developing a causal model of your application domain, identifying how protected attributes influence other variables and ultimately predictions.
2. Formulate specific counterfactual queries relevant to your fairness concerns, focusing on whether predictions would change under different protected attribute values.
3. Classify causal pathways as fair or unfair based on domain knowledge, ethical principles, and stakeholder input, explicitly documenting the rationale for these classifications.
4. Select appropriate implementation approaches based on the specific counterfactual fairness violations identified, targeting the problematic causal pathways while preserving legitimate predictive relationships.
5. Evaluate your interventions using both counterfactual fairness metrics and traditional performance measures to ensure you're effectively addressing discrimination without unnecessarily sacrificing utility.

---

### The Fundamental Challenge of Causal Inference

The main problem in causal inference is that we can never observe two different versions of reality at the same time.  
We can’t see both what actually happened and what would have happened under different conditions.  

In AI fairness, this means we cannot directly measure true counterfactual fairness.  
For example, we can’t observe the same person both with and without a different protected attribute (like race or gender). So we must estimate what would have happened using causal models.  

Pearl’s “ladder of causation” explains three levels of reasoning:  
1. **Association** – noticing correlations
2. **Intervention** – predicting what happens if we act
3. **Counterfactuals** – imagining alternative realities

Fairness often requires the third level, which is the hardest.

For example, in hiring, we might see that women receive lower scores than men.
Counterfactual fairness asks: Would this specific woman have received the same score if she were a man, with everything else the same?
We can’t directly observe this — we can only estimate it.

The key takeaway:
Because we can’t observe counterfactuals directly, fairness analysis must combine data, causal modeling, and domain knowledge.

---

### Observational Causal Inference Methods

1. **Matching methods** attempt to mimic experimental conditions by comparing outcomes for individuals with similar characteristics but different protected attributes. For instance, Rubin's (2006) approach to causal inference uses propensity score matching to estimate treatment effects by comparing similar individuals who received different "treatments" (in fairness contexts, having different protected attributes).
2. **Instrumental variable (IV) approaches** leverage external variables that influence the protected attribute but affect outcomes only through that attribute. As explained by Angrist and Pischke (2008), this approach can help identify causal effects when randomized experiments aren't possible. For example, historical policy changes that affected educational access for certain demographic groups might serve as instruments for estimating the causal effect of education on employment outcomes.
3. **Regression discontinuity designs** exploit threshold-based policies or natural boundaries to approximate experimental conditions. This approach, formalized by Imbens and Lemieux (2008), compares individuals just above and below thresholds, assuming they are otherwise similar. In fairness applications, this might involve examining outcomes for individuals near threshold scores or policy boundaries.
4. **Difference-in-differences methods** compare outcome changes over time between groups affected and unaffected by a change, as described by Card and Krueger (1994). This approach might be used to estimate the causal effect of a policy or intervention on fairness outcomes by comparing changes before and after implementation.

For our Causal Analysis Methodology, these observational methods provide practical tools for estimating counterfactual outcomes when experimental data is unavailable, enabling the application of causal fairness principles despite real-world constraints.  

---

### Sensitivity Analysis for Unmeasured Confounding

In real-world data, we rarely measure every factor that could influence outcomes.  
Some hidden variables (unmeasured confounders) may affect both a protected attribute and the prediction.  

Sensitivity analysis helps us answer:  

How strong would a hidden factor need to be to change our fairness conclusions?  

This is important in AI fairness because it:  
- Acknowledges that our causal models are incomplete
- Quantifies uncertainty
- Prevents overconfidence in fairness claims

One common method is the E-value (VanderWeele & Ding, 2017), which measures how strong an unmeasured confounder would need to be to eliminate the observed causal effect.  

Example  

In a hiring model, suppose we estimate that gender affects hiring recommendations.  
Sensitivity analysis might show that this effect would disappear only if there were a very strong hidden factor influencing both gender and hiring ability.  

If such a strong hidden factor seems unrealistic, we can feel more confident in our fairness conclusion.  

---

### Causal Discovery from Observational Data

Earlier, we assumed causal relationships were known from domain knowledge.  
Causal discovery methods try to **learn causal structures directly from data**.

This is useful in AI fairness when:
- Domain knowledge is limited  
- We want to confirm assumed causal relationships  
- We suspect hidden discrimination mechanisms  

---

### Why It Matters for Fairness

Causal discovery can:
- Reveal hidden pathways from protected attributes to outcomes  
- Detect proxy variables that indirectly encode protected attributes  
- Provide empirical support for fairness analysis  

It helps reduce reliance on assumptions alone.

---

### Main Types of Causal Discovery Methods

1. **Constraint-based methods (e.g., PC algorithm)**  
   - Use statistical independence tests  
   - Infer which variables cause others under certain assumptions  

2. **Score-based methods**  
   - Compare many possible causal graphs  
   - Choose the one that best fits the data while staying simple  

3. **Hybrid methods (e.g., FCI algorithm)**  
   - Combine both approaches  
   - Can handle hidden (latent) confounders  

---

### Example in Fairness

In hiring data, causal discovery has been used to:
- Identify features acting as proxies for race or gender  
- Reveal discrimination pathways not obvious from domain knowledge  
- Support targeted fairness interventions  

---

### Key Takeaway

Causal discovery complements domain expertise by helping identify or validate causal structures using data — making fairness analysis more evidence-based and less assumption-driven.  







