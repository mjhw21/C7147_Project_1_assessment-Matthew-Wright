# C7147_Project_1_assessment-Matthew-Wright

## Purpose!
This program checks sequencing gene reads against a set reference, it finds base mismatches (mutations) and compares the patterns between treated and control groups. The aim is to address whether a genotoxic treatment causes more mutations, and where in the sequence do they occur.

## How to run?
Open the notebook in Google colab. Run the cells from top to bottom including the initial loading cells. At the bottom of the document finally run the final analysis for the complete results

## Inputs and outputs
### Inputs:
A reference sequence file containing 200 bases (A/T/C/G) and a CSV of 6000 reads with columns 'Read_id', 'sample', 'group' and 'sequence'

### Outputs:
For each group, a table of valid and invalid reads, mismatch percentages, events and top gene positions as well as a substitution table (A to C ect.). The function 'compared_positions' then prints one Welch T-test line for each of the 3 top positions

## Code design
**Sample data comes from the data:** My first draft hardcoded 'sample1' to 'sample6'. 'summarise_samples' now creates each samples dictionary when it first sees it, so any different sample or group names work

**Printing is separated from calculations:** print_summary only formats the tables so the returned dictionary can be tested without parsing in any printed text. 

**Percentage set to 'none' when a sample has no valid reads:** In compare_positions, if percentage mismatches do not have any values to base of returns 'None', later when the percentages are looped over they are ignored instead of counting as 0% potentially biasing the Welch's T-test, as well as avoiding a divide by 0 error when 'mismatch_count / valid_reads *100'

## Testing
**No valid reads:** a sample with only invalid reads should give mismatch_percentage=None, and empty input should return {}

**Human Check:** each sample had 1000 reads, the control mismatch rate of 7-10% compared to ~60% for treatment is to be expected for a successful experiment, as well as closely ditributed top 3 gene locations and normal position data for each sample

**Hand check:** I made a small table with simple but made up data for compare_positions, I then worked out the percentage changes and difference between control and treatment by hand and they matched with the result

