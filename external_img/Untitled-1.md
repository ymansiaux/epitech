I am R developer, used to the usage of good practices in coding (git, documentation, unit testing ...). I just joined a team of epidemiologist for which of them can use R but without any of these good practices. I had to work on a project in which we had no documentation, a low number of function, global variables in the project, many hard coded elements ... I want to give a presentation to them explaining my path to transform this messy code into a packaged code. I don't want to be too preachy. Can you help me

# From Messy Code to Packaged R Project: A Friendly Guide

## Introduction

I'd be happy to help you create a presentation that shares your journey transforming messy code into a well-structured R package without being preachy. Here's an outline focusing on practical benefits rather than abstract best practices.

## Presentation Outline

### 1. The Starting Point: Challenges We All Face

- Share specific examples from the project (without criticism)
  - "I found myself wondering which variables were still in use"
  - "When trying to rerun analyses from 3 months ago, I had to recreate all the context"
  - "Small changes would unexpectedly affect other parts of the code"

### 2. The Journey: Small Steps, Big Impact

- **Documentation**: Start with simple comments that evolved into function documentation
  - Show a "before and after" example with roxygen2 comments
  - Highlight how this helps future-you and others understand code purpose

- **Functions**: Moving from script mode to function mode
  - Example: Transforming repeated code blocks into reusable functions
  - Benefit: Easier testing, debugging, and maintenance

- **Removing Global Variables**: The path to reproducibility
  - Example: Moving from globals to function parameters
  - Benefit: Code behavior becomes predictable and explicit

- **Addressing Hardcoded Elements**: Making code flexible
  - Example: Parameters instead of hardcoded paths/values
  - Benefit: Code works across environments and for different analyses

### 3. Packaging: Bringing It All Together

- Simple package structure and its advantages
  - Organization: Code, documentation, tests in expected locations
  - Dependency management: Explicit imports
  - Version control: Tracking what changed when

### 4. The Practical Benefits (focus here!)

- **Time savings**: "I spent 3 hours setting up the package, but saved 20+ hours in the following month"
- **Reproducibility**: "We can now regenerate results from 6 months ago in minutes"
- **Collaboration**: "New team members can contribute meaningful code in days rather than weeks"
- **Reduced errors**: "We caught a critical calculation error thanks to our tests"

### 5. Getting Started: Achievable First Steps

- Start small: Pick one analysis script to improve
- Create a single test for a critical calculation
- Document one key function thoroughly
- Use RStudio's package creation tools for easy setup

## Tips for Your Presentation

- **Use concrete examples** from your actual transformation
- **Emphasize practical benefits** over theoretical correctness
- **Show real time savings** with specific examples
- **Make it incremental**: "You don't need to do everything at once"
- **Offer ongoing help**: "I'm happy to pair-program or review code as we adopt these practices"

Would you like me to elaborate on any of these sections or provide specific code examples for the transformation process?


# Epidemiology of Messy Code: A Public Health Approach to R Programming

## Introduction: The Epidemiology of Code

Just as we study the patterns, causes, and effects of health conditions in populations, we can examine the "health" of our code! Today, I'll share my journey of identifying risk factors for "Code Dysfunction Syndrome" and implementing evidence-based interventions.

## 1. Disease Surveillance: Identifying Symptoms of Unhealthy Code

### Clinical Presentation
Our codebase presented with several concerning symptoms:

- **Global Variable Syndrome (GVS)**: Variables appearing and changing mysteriously across the environment
- **Acute Documentation Deficiency (ADD)**: Code with no context or explanation
- **Chronic Repetition Disorder (CRD)**: The same calculations copy-pasted across multiple scripts
- **Hard-Coding Disease (HCD)**: Brittle file paths and parameters embedded throughout the code

### Case Definition
```r
# Patient presents with severe Hard-Coding Disease
data <- read.csv("C:/Users/JohnSmith/Desktop/special_COVID_data_March12.csv")

# Accompanied by Global Variable Syndrome
SIGNIFICANCE <- 0.05
data_clean <- data[data$p_value < SIGNIFICANCE, ]

# And Chronic Repetition Disorder
# (This exact code appears in 7 different scripts)
data$age_group <- cut(data$age, 
                     breaks=c(0, 18, 40, 65, 120),
                     labels=c("0-18", "19-40", "41-65", "65+"))
```

### Transmission Dynamics
"This code traveled through our team via email attachments and shared drives, infecting new analyses as it spread!"

## 2. Etiology: Root Causes of Code Pathologies

### Risk Factors
- **Time pressure**: "We need these results yesterday!"
- **Code isolation**: Each researcher working in separate environments
- **Lack of exposure** to coding best practices
- **Asymptomatic carriers**: Code that "works" but harbors hidden bugs

### Natural History of Disease
"Like many chronic conditions, these problems developed gradually. What began as a simple analysis script mutated into a complex, interdependent system with no clear structure."

## 3. Interventions: Evidence-Based Code Treatments

### Function Therapy: Breaking Dependencies

**Before treatment (high transmission risk):**
```r
# This script depends on 12 other variables being present in the environment
result <- data$measurement * adjustment_factor / control_mean
```

**After treatment (contained spread):**
```r
#' Calculate Adjusted Measurement Ratio
#'
#' @param measurement Vector of raw measurements
#' @param adjustment_factor Calibration factor for instrument
#' @param control_mean Mean value from control group
#' @return Vector of adjusted ratios
#'
calculate_adjusted_ratio <- function(measurement, adjustment_factor, control_mean) {
  return(measurement * adjustment_factor / control_mean)
}

# Now with clear inputs and outputs
result <- calculate_adjusted_ratio(
  data$measurement,
  adjustment_factor = 1.2,
  control_mean = 34.7
)
```

### Vaccination: Preventing Future Infections with Tests

```r
# tests/testthat/test-calculations.R
test_that("adjusted ratio calculation works with known values", {
  # Arrange
  measurement <- c(10, 20, 30)
  adjustment <- 2
  control <- 10
  
  # Act
  result <- calculate_adjusted_ratio(measurement, adjustment, control)
  
  # Assert
  expect_equal(result, c(2, 4, 6))
})
```

"Now our code is immunized against regression infections!"

## 4. Packaging: Quarantine and Control

### Package Isolation

"Just as we isolate infectious patients, we've isolated our code into a controlled package environment:"

```
epiproject/
├── DESCRIPTION        # The patient chart: metadata and dependencies
├── R/                 # Quarantine zone for functions
│   ├── cleaning.R     # Data sanitization procedures
│   ├── analysis.R     # Statistical methods
│   └── plotting.R     # Visualization protocols
├── tests/             # Diagnostic testing center
└── vignettes/         # Treatment protocols and usage examples
```

### Exposure Notification

"Our package documentation serves as a contact tracing system:"

```r
#' Detect outliers using modified Z-score method
#'
#' @param data Vector of measurements
#' @param threshold Z-score threshold (default: 3.5 per Iglewicz & Hoaglin)
#' @return Logical vector indicating outliers
#'
#' @references Iglewicz and Hoaglin (1993), "How to Detect and Handle Outliers"
#' @export
detect_outliers <- function(data, threshold = 3.5) {
  # Implementation
}
```

## 5. Outcomes: Public Health Impact

### Before-After Comparison Study

**Before intervention:**
- Reproduction number (R₀) of bugs: 2.3
- Incubation period for new team members: 3-4 weeks
- Script mortality rate: 25% couldn't be executed after 6 months

**After intervention:**
- Reproduction number (R₀) of bugs: 0.7 (controlled spread!)
- Incubation period for new team members: 2-3 days
- Script survival rate: 98% still executable after 1 year

### Quality of Life Improvements

"Team members reported significantly reduced stress levels and increased confidence in results!"

## 6. Implementation: Community-Based Prevention

### Herd Immunity Through Small Changes

- Start by documenting your most critical functions (vaccination)
- Create config files to replace hardcoding (hygiene practices)
- Extract one repetitive task into a function (targeted intervention)
- Add one test for your most important calculation (surveillance)

### Intervention Costs vs. Benefits

"Yes, there's an upfront investment, but consider the R₀! Each improvement prevents multiple future problems!"

## Conclusion: A Healthier Code Ecosystem

Just as in public health, the goal isn't perfection—it's managing risk and improving outcomes through practical measures. Our code is now more:

- **Resistant** to bugs
- **Less susceptible** to environmental changes
- **Easier to diagnose** when problems occur
- **Capable of safe transmission** between researchers

Remember: Good code practices are preventive medicine for your research!

**Would anyone like a code health screening for their current projects? I'm happy to offer consultation hours!**

I'd like to emphasize that people do their best, and so even if I will list some bad practices, it's not in a way to shame them

# Epidemiology of Messy Code: A Public Health Approach to R Programming

## Introduction: The Epidemiology of Code

Just as we study the patterns, causes, and effects of health conditions in populations, we can examine the "health" of our code! Today, I'll share my journey of identifying common patterns and implementing helpful practices - recognizing that we're all doing our best with the resources and knowledge we have.

> **Key message**: We all develop coding habits based on what we've learned and what gets the job done. There's no shame in how code evolves - we're scientists first, not software engineers!

## 1. Code Development as a Natural Evolution

### How Research Code Naturally Grows

Like how diseases emerge from complex interactions, our code evolves to solve immediate problems:

- **Exploratory Phase**: Quick scripts to understand data
- **Analysis Phase**: Building on successful explorations
- **Reporting Phase**: Generating results for papers
- **Revisiting Phase**: Returning to old code months later

### Familiar Patterns We All Experience

```r
# We've all written code like this - it works!
# (And it helped answer important research questions)
data <- read.csv("my_data.csv")
data <- data[!is.na(data$age),]
results <- aggregate(outcome ~ exposure + age_group, data=data, FUN=mean)
write.csv(results, "for_manuscript_table2.csv")
```

> **Key message**: These approaches aren't "wrong" - they solved real problems! They're the equivalent of public health interventions with limited resources.

## 2. Universal Challenges in Research Coding

### Challenges We All Face

- **Time pressure**: "The grant is due tomorrow!"
- **Priority focus**: Science comes first, code organization second
- **Knowledge gaps**: We weren't trained as programmers
- **Resource constraints**: No dedicated software engineers

### Why Traditional Solutions Emerge

"Like folk medicine, we develop practical solutions based on experience rather than formal training:"

```r
# This pattern emerges naturally when we need to try many approaches
# We've all been here - and it works!
analysis_v1 <- function() { ... }
analysis_v2 <- function() { ... }
analysis_final <- function() { ... }  # The one we actually used

# Or saving our environment to preserve complex work
save.image("analysis_for_paper.RData")
```

> **Key message**: These approaches aren't signs of failure - they're creative adaptations to complex scientific workflows!

## 3. Community Solutions: Learning Together

### Sharing Alternative Approaches

Just as we share epidemiological methods, we can share coding approaches:

**A common approach (perfectly valid):**
```r
# This gets the job done effectively!
df$bmi <- df$weight / ((df$height/100)^2)
df$bmi_category <- ifelse(df$bmi < 18.5, "Underweight",
                         ifelse(df$bmi < 25, "Normal",
                                ifelse(df$bmi < 30, "Overweight", "Obese")))

# Repeated for another dataset
df2$bmi <- df2$weight / ((df2$height/100)^2) 
df2$bmi_category <- ifelse(df2$bmi < 18.5, "Underweight",
                          ifelse(df2$bmi < 25, "Normal",
                                 ifelse(df2$bmi < 30, "Overweight", "Obese")))
```

**An alternative approach that can help:**
```r
#' Calculate BMI from weight and height
#'
#' @param weight Weight in kg
#' @param height Height in cm
#' @return BMI value
calculate_bmi <- function(weight, height) {
  return(weight / ((height/100)^2))
}

#' Categorize BMI values according to WHO standards
#'
#' @param bmi Vector of BMI values
#' @return Character vector of categories
categorize_bmi <- function(bmi) {
  return(case_when(
    bmi < 18.5 ~ "Underweight",
    bmi < 25 ~ "Normal",
    bmi < 30 ~ "Overweight",
    TRUE ~ "Obese"
  ))
}

# Now we can apply consistently
df$bmi <- calculate_bmi(df$weight, df$height)
df$bmi_category <- categorize_bmi(df$bmi)

df2$bmi <- calculate_bmi(df2$weight, df2$height)
df2$bmi_category <- categorize_bmi(df2$bmi)
```

> **Key message**: Both approaches work! The second one just makes some tasks easier as projects grow.

## 4. Benefits That Resonated With Our Team

### Reduced "Research Amnesia"

"Six months after finalizing our manuscript, reviewers asked for additional analyses. With our new approach:"

```r
# Load our package instead of hunting for the right script versions
library(ourproject)

# Documentation reminded us exactly what each function did
?calculate_adjusted_risk

# Generate the new analysis with confidence it matches previous methods
new_results <- calculate_adjusted_risk(
  data = reviewer_suggested_subset,
  include_comorbidities = TRUE
)
```

### Knowledge Transfer Without Pain

"When Priya joined our team mid-project, she could immediately understand our analysis logic without needing to decipher entire scripts."

### Collaboration Became Easier

"Ahmed could improve the visualization functions while Sofia refined the statistical models - without stepping on each other's toes."

## 5. Small Steps That Made Big Differences

### Incremental Improvements Anyone Can Try

> **Key message**: You don't need to transform everything at once! Small steps bring immediate benefits.

1. **Add helpful comments** to your existing code
   ```r
   # This coefficient reflects the log odds ratio adjusted for age and sex
   # (Added this after spending 30 minutes re-understanding it myself!)
   coefficient <- 0.42
   ```

2. **Create simple functions** for calculations you use repeatedly
   ```r
   # Turn code you copy-paste into a simple function
   convert_to_odds_ratio <- function(log_odds) {
     return(exp(log_odds))
   }
   ```

3. **Use consistent file naming** to find things later
   ```
   01_data_import.R
   02_data_cleaning.R
   03_analysis_primary.R
   04_analysis_sensitivity.R
   05_figures.R
   ```

4. **Create a basic README** explaining what each script does

## 6. The Journey Is Personal

### My Own Learning Experience

"I want to emphasize - I made ALL these mistakes myself! I learned through trial and error, just like everyone else. Some things I tried didn't work for our team, and that's okay too."

### Meeting People Where They Are

"Different approaches work for different projects. A 2-week analysis might not need the same structure as a multi-year project. We adapted our practices to fit each situation."

## Conclusion: Growing Together as a Research Community

As epidemiologists, we're used to working with the data and resources we have, making improvements where possible. The same philosophy applies to our code:

- **Recognize the constraints** we all work within
- **Share helpful practices** without judgment
- **Adopt what works** for your specific context
- **Improve incrementally** rather than overhaul everything

Remember: Our shared goal is advancing important research. Better coding practices are just tools to help us get there more efficiently and reliably.

**I'm happy to share specific examples from our projects or pair-program with anyone who's interested in trying these approaches!**

# Code Hoarding Disorder (CHD)

## Clinical Description

**Code Hoarding Disorder (CHD)** is a common condition affecting research environments worldwide. It's characterized by the persistent difficulty in discarding or deleting unused code files, despite their lack of current value to the project. Severe cases include:

- Multiple directories named "old" or "backup" nested within each other
- Files with names like "analysis_v2_final_FINAL_realFinal_USE_THIS_ONE.R"
- Commented-out blocks of code with notations like "// might need later"
- Scripts maintained solely because "it took me three days to write this in 2019"

## Epidemiology

Prevalence rates of CHD approach 95% in academic research settings. Risk factors include:

- Prior traumatic experiences of accidentally deleting needed code
- Analysis deadline pressure leading to "quick fix" duplications
- Uncertainty about which code produces specific results in publications
- Fear of reviewer requests requiring resurrection of old analyses

## Pathophysiology

```r
# Example of advanced CHD:

# I think this was for the 2020 analysis but not sure
# data_old <- read.csv("final_dataset.csv") 

# Use this one instead
# data_new <- read.csv("final_dataset_corrected.csv")

# Actually I think this is the right one now
data <- read.csv("final_dataset_v3_with_fixes.csv")

# Old way of calculating outcome
# result <- data$exposure * 1.5 + data$confounder 

# New way 
# result <- data$exposure * 1.2 + data$confounder

# Newest way (I think this is what we used in the paper)
result <- data$exposure * 1.3 + data$confounder

# write.csv(result, "for_table1.csv")
# Commented out because I'm not sure if this is needed anymore
```

## Complications and Comorbidities

CHD frequently co-occurs with:
- **Version Control Avoidance Syndrome (VCAS)**
- **Documentation Deficiency Disorder (DDD)**
- **Acute Analysis Replication Failure (AARF)**

## Treatment Options

### Git Version Control Therapy (GVCT)
Allows safe code deletion knowing history is preserved:
```bash
# Now you can safely delete, knowing the code is preserved in history
git add old_script.R
git commit -m "Archive old_script.R before removal"
git rm old_script.R
git commit -m "Remove unused script"
```

### File Archaeology Documentation (FAD)
```r
# Create a clear record before removing:
#' @title Dead Code Registry
#' @description Documentation of code removed during cleanup
#' 
#' 1. exposure_calculation_2019.R - Original method using Model A
#'    Removed: 2025-03-15
#'    Reason: Superseded by improved method in current_analysis.R
#'    Location: Git commit 7a8b9c or archived in project/archive/
```

### Exposure and Response Prevention (ERP)
- Gradually increase comfort with code deletion through systematic exposure
- Start with obviously redundant files, progress to more anxiety-provoking deletions
- Use Git branches for "trial deletions" to reduce anxiety

## Prognosis

With appropriate intervention, most researchers can learn to maintain tidy codebases while preserving necessary work. Complete recovery allows for:

- Finding relevant code in seconds rather than hours
- Confidently directing new team members to current methods
- Reduced project bloat and environmental burden on computing resources
- Decreased anxiety when returning to projects after months away

**Remember**: CHD is a normal adaptation to the uncertain nature of research! Treatment focuses on building better systems rather than eliminating the natural instinct to preserve valuable work.