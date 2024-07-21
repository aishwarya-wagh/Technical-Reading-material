# ETL Interview Questions

## Q. Difference between OLTP and OLAP systems.
- **OLTP (Online Transaction Processing)** systems are designed for managing transaction-oriented applications. They support day-to-day operations and are characterized by a large number of short online transactions (insert, update, delete).
- **OLAP (Online Analytical Processing)** systems are designed for query and analysis rather than transaction processing. They support complex queries and are characterized by a relatively low volume of transactions. Queries are often complex and involve aggregations.

## Q. What is transformation?
- Transformation in ETL refers to the process of converting data from one format or structure into another. It includes data cleaning, data mapping, data aggregation, and data integration to ensure the data is in the desired format for analysis.

## Q. What is active and passive transformation?
- **Active Transformation**: A transformation that changes the number of rows that pass through it, e.g., filter transformation.
- **Passive Transformation**: A transformation that does not change the number of rows that pass through it, e.g., expression transformation.

## Q. What is threshold value validation testing?
- Threshold value validation testing involves verifying that the data values fall within the specified range or threshold limits. This ensures that the data meets predefined business rules or constraints.

## Q. Name 3 approaches that could be followed by system integration testing.
- **Top-Down Approach**: Extract data from sources, then put the data in the staging area to validate, and then put it in the data warehouse and finally in the data mart.
- **Bottom-Up Approach**: Extract data from sources, validate in the staging area, load data in data marts, and then move data from data marts to the targeted data warehouse.
- **Hybrid Approach**: Combines elements of both top-down and bottom-up approaches.

## Q. What is data purging?
- Data purging is the process of removing all the records from a database or data storage system that are no longer required or that are deemed obsolete.

## Q. What is SCD and what are its types?
- **Slowly Changing Dimensions (SCD)** refer to how data warehouse systems manage and track changes over time.
  - **SCD Type 1**: Overwrites old data with new data.
  - **SCD Type 2**: Creates a new additional record.
  - **SCD Type 3**: Adds a new column to store the new value while preserving the old value.

## Q. What is a self join?
- A self join is a regular join but the table is joined with itself.

## Q. What is meant by a cosmetic bug?
- A cosmetic bug refers to a defect that does not affect the functionality but affects the appearance or layout of the application, such as misaligned text or incorrect fonts.

## Q. Which is the testing bug that comes while performing threshold validation testing?
- Threshold bugs arise when data values do not fall within the expected threshold limits or ranges during threshold validation testing.

## Q. In case user A is already logged in and user B is trying to log in but the system does not allow, what kind of bug is this?
- This is typically a concurrency bug or session management bug.

## Q. Which bug type in ETL testing doesn’t allow entering valid values?
- This is usually referred to as a validation bug or input constraint bug.

## Q. Which testing type is used to check the data type and length of attributes in ETL transformation?
- **Schema Validation**: It ensures that the data types and lengths of attributes match the expected schema definitions.

## Common ETL Testing Scenarios:
1. **Structure Validation**
   - Verify that the structure of the source and target data matches the expected schema, including table names, column names, data types, and constraints.
2. **Validating Mapping Document**
   - Ensure that the data transformation logic is implemented correctly according to the mapping document. This includes checking the data flow from source to target and ensuring all transformations are applied correctly.
3. **Validating Constraints**
   - Check that all constraints, such as primary keys, foreign keys, unique constraints, and check constraints, are correctly applied in the target system.
4. **Data Consistency Check**
   - Ensure that data remains consistent throughout the ETL process. This includes verifying that data values are consistent and follow the same rules in both source and target systems.
5. **Data Completeness Check**
   - Ensure that all expected data is loaded into the target system without any loss. This involves checking that the number of records in the source and target systems match.
6. **Data Correctness Check**
   - Verify that the data is correctly transformed and loaded into the target system. This includes checking for any discrepancies or errors in the data values.
7. **Data Transform Validation**
   - Validate that the transformations applied to the data are correct and produce the expected results. This includes checking the logic of data transformations such as aggregations, calculations, and data mapping.
8. **Data Quality Validation**
   - Ensure that the data meets the required quality standards. This includes checking for data accuracy, consistency, completeness, and reliability.
9. **Null Validation**
   - Check for null values in the data and ensure that they are handled correctly according to the business rules. This includes verifying that null values are correctly transformed and loaded into the target system.
10. **Duplicate Value Validation**
    - Ensure that there are no duplicate records in the target system. This includes checking for any duplicate values in the data and ensuring that they are handled correctly during the ETL process.
