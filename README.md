# Auto-DS: Automated Data Science Agent Skills

An agent framework for aiding the Data Science process through the use of Claude skills.

This project defines a comprehensive set of AI agent skills designed to augment data scientists in their Exploratory Data Analysis (EDA) and Machine Learning (ML) workflows. These skills automate repetitive tasks, implement best practices, and provide insights, allowing practitioners to focus on high-value activities like interpretation, decision-making, and domain expertise application.

## Overview

The auto-ds project aims to minimize the boilerplate code and repetitive tasks in data science, allowing practitioners to focus on what matters most: understanding their data, making informed decisions, and solving real-world problems.

## Key Documents

### 1. Data Scientist Role Definition
**File**: [`data-scientist-role.md`](data-scientist-role.md)

Comprehensive description of the data scientist role in the context of EDA & ML, including:
- Core responsibilities across the data science workflow
- Required technical and soft skills
- Typical workflow stages
- Opportunities for AI augmentation

### 2. Agent Skills Breakdown
**File**: [`agent-skills-breakdown.md`](agent-skills-breakdown.md)

Detailed breakdown of 28 discrete agent skills organized into 7 categories:
- Data Understanding & Profiling (3 skills)
- Exploratory Visualization (3 skills)
- Data Preparation & Feature Engineering (5 skills)
- Machine Learning Model Development (7 skills)
- Model Validation & Analysis (3 skills)
- Communication & Documentation (4 skills)
- Best Practices & Guidance (3 skills)

Includes implementation priority roadmap across 9 phases.

### 3. Skills Catalog
**Directory**: [`skills/`](skills/)

Individual skill specifications with detailed documentation for each of the 28 skills. See [`skills/README.md`](skills/README.md) for the complete catalog.

## Project Structure

```
auto-ds/
├── README.md                           # This file
├── data-scientist-role.md             # Role definition document
├── agent-skills-breakdown.md          # Skills breakdown and roadmap
└── skills/                            # Individual skill specifications
    ├── README.md                      # Skills catalog and index
    ├── data-understanding/            # Data exploration skills
    ├── exploratory-visualization/     # Visualization skills
    ├── data-preparation/              # Data prep & feature eng. skills
    ├── ml-development/                # Model development skills
    ├── validation/                    # Model validation skills
    ├── communication/                 # Reporting & documentation skills
    └── best-practices/                # Quality & guidance skills
```

## Design Philosophy

### Human-AI Collaboration
These skills are designed to **augment**, not replace, data scientists. The human maintains:
- Strategic decision-making
- Domain expertise application
- Critical interpretation of results
- Ethical considerations
- Creative problem-solving

The AI agents handle:
- Boilerplate code generation
- Comprehensive analysis execution
- Best practice implementation
- Pattern recognition at scale
- Repetitive tasks automation

### Key Principles
- **Modular**: Each skill can be used independently
- **Composable**: Skills combine for complex workflows
- **Configurable**: Adaptable to different needs
- **Transparent**: Explains actions and reasoning
- **Educational**: Helps users learn while working

## Quick Start

### Understanding the Framework
1. Read [`data-scientist-role.md`](data-scientist-role.md) to understand the problem space
2. Review [`agent-skills-breakdown.md`](agent-skills-breakdown.md) for the complete skills landscape
3. Browse [`skills/README.md`](skills/README.md) for the full catalog
4. Dive into individual skill specs in `skills/` subdirectories

### Implementation Roadmap

**Phase 1: Core EDA** (Foundation)
- Data Loader & Inspector
- Data Profiler
- Data Quality Assessor
- Auto-Visualizer

**Phase 2: Data Preparation**
- Missing Data Handler
- Feature Encoder
- Feature Scaler & Transformer

**Phase 3: Basic ML**
- Problem Formulator
- Baseline Model Builder
- Model Trainer
- Model Evaluator

See [`agent-skills-breakdown.md`](agent-skills-breakdown.md) for the complete 9-phase roadmap.

## Use Cases

### For Data Scientists
- **Rapid EDA**: Instant dataset understanding with automated profiling and visualization
- **Model Development**: Quick experimentation with training and evaluation automation
- **Best Practices**: Guidance to avoid common pitfalls
- **Documentation**: Auto-generated reports and documentation

### For Data Science Teams
- **Standardization**: Consistent approaches across team members
- **Knowledge Transfer**: Junior members learn from embedded best practices
- **Productivity**: Reduce time spent on repetitive tasks
- **Quality**: Automated checks for common issues

## Contributing

This project welcomes contributions:
- **Skill Proposals**: Suggest new skills for additional use cases
- **Skill Refinement**: Improve existing skill specifications
- **Implementation**: Build the actual agents based on specs
- **Feedback**: Share experiences and improvement ideas

---

**Status**: Framework Definition Complete ✓  
**Next Step**: Begin Phase 1 Implementation
