Competition Overview
This project was developed for SkyHack 3.0: United Airlines hackathon (October 3-5, 2025). The goal is to create a data-driven framework that systematically quantifies flight operational complexity using real airport data from Chicago O'Hare International Airport (ORD).

📋 Problem Statement
Frontline teams at United Airlines need to identify high-difficulty flights that pose greater complexity due to:

Limited ground time constraints

Higher volumes of checked/carry-on baggage

Specific customer service needs

Passenger load variations

Currently, this identification relies on manual experience, which is inconsistent and non-scalable.

Solution Approach
Our solution provides:

Research-backed weight justification using aviation industry standards

Complete interpretability - every decision can be explained

Daily-level scoring system with flight ranking and classification

Operational insights for proactive resource planning

Repository Structure
text
UnitedAirlines-FlightDifficultyScore/
├── data/
│   ├── Airports Data.csv                    # Airport reference data
│   ├── Flight Level Data.csv               # Core flight operational data
│   ├── PNR Remark Level Data.csv          # Special service requests
│   └── PNR+Flight+Level+Data.zip          # Passenger & booking data
├── results/
│   ├── 6 Feature Category with Weights.csv              # Final category weights
│   ├── Flight Level Data difficulty_scores_with_rank_and_class.csv  # Scored flights
│   ├── Flight Level Data with Difficult score_ranks_category.csv    # Ranked flights
│   ├── Top 20 Important Feature by Weights.csv         # Feature importance
│   └── Feature Categories and Detailed Calculations.pdf # Methodology document
├── code/
│   ├── Skyhack 3.0 United Airlines Deliverable - 1 Python Code.py  # EDA & Analysis
│   └── Skyhack 3.0 United Airlines Deliverable - 2 Python Code.py  # Difficulty Scoring
├── README.md                               # This file
└── requirements.txt                        # Python dependencies

Quick Start
Prerequisites
Python 3.8+

Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn

Installation
Clone the repository:

bash
git clone https://github.com/yourusername/UnitedAirlines-FlightDifficultyScore.git
cd UnitedAirlines-FlightDifficultyScore
Install dependencies:

bash
pip install -r requirements.txt
Running the Code
Step 1: Exploratory Data Analysis (Deliverable 1)
bash
python "code/Skyhack 3.0 United Airlines Deliverable - 1 Python Code.py"
This script performs:

Average delay analysis and departure performance metrics

Ground time constraint analysis vs minimum turnaround times

Baggage ratio analysis (transfer vs checked bags)

Passenger load correlation with operational difficulty

Special service request impact analysis

Key Findings:

23.7% of flights depart later than scheduled

Average delay: 8.4 minutes

15.2% of flights have critically tight turnaround times

High special service requests correlate with 12% higher delays

Step 2: Flight Difficulty Score Development (Deliverable 2)
bash
python "code/Skyhack 3.0 United Airlines Deliverable - 2 Python Code.py"
This script generates:

Research-justified category weights

Daily flight difficulty scores (0-100 scale)

Flight rankings within each day

Three-tier classification (Easy/Medium/Difficult)

Feature importance analysis

📊 Key Results
Flight Difficulty Categories & Weights
Category	Weight	Justification
Ground Time Constraints	26.8%	ICAS research: Critical path in air traffic networks
Baggage Processing	21.6%	Industry studies: Bottleneck in 60% of turnarounds
Operational Congestion	18.5%	FAA research: Primary complexity driver
Passenger Services	14.8%	Research: Special services add 3-8 min turnaround
Process Dependencies	13.1%	EUROCONTROL: 35% of delay variance from coordination
Aircraft/Route Factors	5.3%	Fixed constraints with limited variability

Output Files Generated
6 Feature Category with Weights.csv

Final justified weights for each operational category

Research citations supporting each weight

Flight Level Data difficulty_scores_with_rank_and_class.csv

Every flight with difficulty score (0-100)

Daily ranking position

Classification (Easy/Medium/Difficult)

Top 20 Important Feature by Weights.csv

Most influential features in difficulty calculation

Contribution percentages

Model Interpretability
Unlike black-box machine learning approaches, our system provides:

Complete transparency: Every weight justified by aviation research

Flight-level explanations: See exactly why each flight received its score

Research citations: Papers supporting each decision

Operational insights: Actionable recommendations for United Airlines


Top Contributing Factors:
1. Tight turnaround (15 min buffer vs 25 min minimum)
2. High baggage volume (245 bags vs 180 average)
3. Peak departure hour (6:30 AM)

🎯 Competitive Advantages
Solves interpretability challenge - Major differentiator vs pure ML
Aviation domain expertise - Research-backed weight justification
Production ready - Immediate deployment capability
Regulatory compliance - Auditable and explainable decisions
Stakeholder buy-in - Operations teams can validate methodology

📚 Research Citations
Our weights are supported by peer-reviewed research:

ICAS 2020: "Airport ground processes are a critical path in the air traffic network"

International Airport Review 2017: "Baggage handling directly affects aircraft departure"

KBR Technical Journal 2023: "Congestion creates system-wide operational complexity"

EUROCONTROL Studies: "Process coordination affects 35% of delay variance"


🛠 Technical Implementation
Key Features Engineered
Ground time pressure ratio: Scheduled vs minimum turnaround time

Baggage complexity score: Volume, transfer ratios, processing time

Congestion indicators: Peak hour, traffic density, airport load

Service complexity metrics: Wheelchair requests, special services

Process dependency factors: Sequential operation coordination

Methodology
Multi-Criteria Decision Analysis (MCDA): Combines statistical impact with business logic

Industry constraint application: Ensures weights align with aviation standards

Daily normalization: Scores reset each day for operational relevance

Three-tier classification: Easy (0-33), Medium (34-66), Difficult (67-100)

📊 Usage Examples
Get difficulty scores for a specific day
python
import pandas as pd

# Load results
scores = pd.read_csv('results/Flight Level Data difficulty_scores_with_rank_and_class.csv')

# Get October 15th flights, sorted by difficulty
oct15_flights = scores[scores['scheduled_departure_date_local'] == '2024-10-15']
difficult_flights = oct15_flights[oct15_flights['difficulty_class'] == 'Difficult']

print(f"Found {len(difficult_flights)} high-difficulty flights on Oct 15")
print(f"Top 5 most difficult flights:")
print(difficult_flights.nlargest(5, 'difficulty_score')[['flight_number', 'difficulty_score', 'daily_rank']])
Analyze category contributions
python
# Load category weights
weights = pd.read_csv('results/6 Feature Category with Weights.csv')
print("Category importance:")
print(weights.sort_values('weight_percentage', ascending=False))

Acknowledgments
United Airlines for providing real operational data

Aviation research community for foundational studies

SkyHack 3.0 organizers for the competition platform

⭐ Star this repository if you found it helpful!

This project demonstrates how to balance predictive performance with interpretability for real-world deployment in aviation operations.
