# Timetable_Scheduling_Optimization
A Python tool that automatically creates optimal university schedules. Handles multiple years, divisions, subjects, professors, and classrooms while avoiding conflicts. Uses evolutionary computation to balance workloads and meet teaching hour requirements. Outputs complete timetables and detailed statistics. 

## Features

- Generates weekly timetables for multiple academic years
- Handles professor availability and workload balancing
- Ensures no classroom or professor double-booking
- Balances subject hours across the week
- Provides detailed statistics on the generated schedule
- Includes both complete and division-wise timetable views

## INPUT DATA CONFIGURATION

This section defines all the scheduling constraints and resources:

1. **YEARS STRUCTURE**:
   - Contains 3 academic years (1st, 2nd, 3rd)
   - Each year has:
     * Divisions: A, B, C, D (4 classes per year)
     * Subjects: 6 subjects per year
     * Professors: 2-3 professors per subject

2. **INFRASTRUCTURE**:
   - Classrooms: 16 rooms available (N201-N208, N301-N308)
   - Time slots: 6 daily slots (9AM-4PM with 1PM-2PM break)
   - Days: Monday to Friday (5-day week)

3. **TEACHING REQUIREMENTS**:
   - Each subject needs 4 hours/week per division
   - Total hours per division: 24 (6 subjects × 4 hours)

You can modify these parameters to match your institution's:
- Academic structure
- Available resources
- Scheduling needs

## GENETIC ALGORITHM TIMETABLE GENERATOR

**CORE COMPONENTS**:

1. **INITIALIZATION**:
   - Creates population of random valid timetables
   - Each chromosome is a 3D structure: [days][time_slots][classrooms]
   - Tracks subject hours and professor assignments

2. **FITNESS FUNCTION**:
   - Evaluates timetable quality using penalty system:
     * Subject hours fulfillment (4hrs/week per subject)
     * Professor workload balance
     * Classroom utilization
     * Division schedule constraints
     * Consecutive hours avoidance
   - Lower penalty = Better timetable

3. **GENETIC OPERATORS**:
   - Selection: Tournament selection with elitism (keeps top 10%)
   - Crossover: Swaps entire days between parents
   - Mutation: Swaps random class assignments
   - Repair: Fixes invalid schedules by filling missing hours

4. **EXECUTION FLOW**:
   - Initial population → Fitness evaluation → Selection →
   - Crossover/Mutation → New generation →
   - Repeat for N generations →
   - Return best timetable

**KEY PARAMETERS (tunable):**
- Population size: 300
- Generations: 400
- Crossover rate: 0.9
- Mutation rate: 0.12
- Subject hours required: 4/week

**OUTPUT FEATURES:**
1. Complete timetable view (all divisions)
2. Individual division timetables
3. Detailed statistics:
   - Professor workload analysis
   - Subject coverage per division
   - Room utilization
   - Fitness score

**USAGE INSTRUCTIONS:**
1. Modify input data as needed (years, subjects, professors)
2. Adjust GA parameters for different problem sizes
3. Run main() to generate optimized timetable
4. View printed output or process returned schedule object


## Requirements

- Python 3.x
- numpy
- collections (defaultdict)
