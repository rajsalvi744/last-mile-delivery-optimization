# Optimizing Last-Mile Delivery Planning for Cost Reduction

## Overview
This project focuses on analyzing last-mile delivery operations to identify cost optimization opportunities. The analysis evaluates partner performance, trip costs, and delivery efficiency while exploring different cost-saving scenarios.

## Objectives
- To analyze the cost structure of last-mile delivery partners.
- To identify clusters and regions with high delivery costs.
- To evaluate different scenarios for optimizing delivery operations and reducing costs.

## Dataset Description
The project utilizes five key datasets:

1. **oda_trip_data.csv**: Contains details of consignments, including dispatch times, weights, origin clusters, and delivery partners.
   - Key Columns: `cnote`, `dispatch_time`, `client_name`, `weight`, `origin_cluster`, `to_pincode`, `trip_id`, `bp_id`, `serviceability`

2. **commercials.csv**: Provides information on the fixed and variable cost rates agreed with each delivery partner.
   - Key Columns: `bp_id`, `commercial_type`, `Rate`

3. **partners.csv**: Maps business partner IDs to their respective names.
   - Key Columns: `bp_id`, `bp_name`

4. **cluster_coverage.csv**: Maps pin codes to branches and clusters responsible for deliveries.
   - Key Columns: `to_pincode`, `branch_name`, `branch_code`, `cluster_code`

5. **regions.csv**: Links clusters to regions and states.
   - Key Columns: `cluster`, `cluster_name`, `region`, `state`

## Analysis Workflow
1. **Data Preparation**:
   - Created an `ODA` column by extracting the ODA category from the `serviceability` column, ranging from 1 (closest to warehouse) to 6 (farthest).
   - Added a `trip_category` column: trips categorized as NP (ODA 1 or 2) or DNP (ODA > 2).

2. **Current vs Baseline Analysis**:
   - Introduced a `current_trips` column to flag trips made by business partners based on the maximum ODA in each trip.
   - Established `baseline_trip_flag` to represent trips following baseline instructions, where partners make up to two trips per category (NP and DNP) per day.
   - Calculated `current_fixed_cost` and `current_total_cost` (current fixed cost + variable cost * weight).
   - Calculated `baseline_fixed_cost` and `baseline_total_cost` (baseline fixed cost + variable cost * weight).
   - Compared extra trips made (current trips - baseline trips) and overpayments to partners at the cluster and region levels.

3. **Scenario Testing**:
   - Scenario 1: Partners make 2 NP trips and 1 DNP trip in each half of the week (Monday-Wednesday and Thursday-Saturday).
   - Scenario 2: Partners make 1 NP trip and 1 DNP trip in the first half and 1 NP trip in the second half of the week.
   - Added `sc1` and `sc2` columns to flag trips satisfying these scenarios.
   - Calculated fixed and total costs for both scenarios.

4. **Comparison and Insights**:
   - Compared baseline, Scenario 1, and Scenario 2 total costs to determine the most cost-effective strategy.
   - Identified the top 5 regions where each scenario could be implemented for improvement over the baseline.

## Key Findings
- The most overpaid region was South, with Hyderabad as the most overpaid cluster.
- Scenario 2 significantly reduced delivery costs compared to both the current setup and the baseline.
- Recommendations included implementing Scenario 2 in the top 5 regions identified for maximum cost savings.

## Recommendations
- Implement Scenario 2 in high-cost regions to achieve significant cost reductions.
- Renegotiate variable cost rates with partners in high-cost regions and clusters.
- Optimize trip planning and adherence to baseline instructions to reduce overpayments.

## Files in the Repository
- **data files**: Contains all data files
- **extra_trips_analysis.xlsx**: Contains the cleaned data, analysis, and visualizations.
- **Data Dictionary.pdf**: Describes the datasets and their fields.


## Future Scope
- Automate data cleaning and integration using Python or ETL tools.
- Incorporate real-time delivery data for dynamic optimization.
- Expand analysis to include delivery time and customer satisfaction metrics.

---

Feel free to modify the recommendations and findings sections based on your insights from the analysis.

