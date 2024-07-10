# DCbased_CODcoding
Text-based Death Certificate Categorization and Coding

This Python program uses serial keyword searches and overlaid logic to sort death record data into Cause of Death categories useful in public health monitoring and research. The death categories included in the base keywords and program code are Overdose, Environmental Heat Related, Environmental Cold Related, Other Accidental Injury, Firearm Injury, Cardiovascular Disease, Other Illness, and Undetermined. There is a supplemental Excel formula described at the end of this file that allows a user to extract one of the basic steps of this program to be performed in Excel (best for users that only desire to identify deaths of one category).


### Prerequisites

- Keyword lists excel file (available on project GITHub) - this is a file containing pathognomonic keywords for several death categories developed with input from a Medical examiner and will be part of the program input.
- Medical Examiner or Coroner's office (MEO) data formatted into the provided COD Coding input excel sheet (available on project GITHub) - this will also be part of the program input.
- Program is written in Python, user will need an updated version of Python and a shell to run the program in.

### Features

- ALL CAUSE IDENTIFICATION: 
  This function identifies all records that meet the criteria for each of the following categories:
  Overdose, Heat-Related, Cold-Related, Other Injury, Heart Disease, Other Illness, Firearm Injury
  Results are returned as True/False for each record in a column corresponding to each death category. 
  Results are found in columns titled 'FINAL_CATEGORY_UNK' which indicates that unknown records were searched.
  The exception is the 'FINAL_ALL_OD' returns the results for all cause identification of overdoses.
  *This coding method will include deaths of unknown manner
  *This coding method may identify multiple death categories for one record if criteria for multiple categories are met.
  *Ensure to review and manually sort records that returned "True" in the 'MANUAL' column as the algorithm was not able to sort those.
  
- MUTUALLY EXCLUSIVE SORTING
  This function sorts each record into a single cause of death category.
  If a death meets criteria for multiple categories, the following priorities are used:
    - Accidental deaths: Overdose > Heat-Related > Cold-Related > Other Accidental Injury
    - Natural deaths: Heart Disease > Other Illness
  Results are found in the 'COD' column. Refer to the mutually exclusive sorting section 
  of the raw code for the number associated with each death category.
  *All deaths of undetermined/unknown manner are sorted into the Unknown category with this function.
  *Ensure to review and manually sort records that returned "True" in the 'MANUAL' column as the algorithm was not able to       sort those.
  

## Usage
- Format MEO data into provided COD Coding input spreadsheet. If Cause A-D are separated on your MEO report, combine all information in those fields into the 'CAUSE' column on the input spreadsheet. Save to local device.
- Save keyword list spreadsheet to local device.
- Update code to reflect the location of both documents on local device where directed.
- Make other adjustments to the code as directed in code's comments to align with user preferences (ex. adding keyword lists, using SUDORs keywords for Overdose).
- Run code. Output will populate in the file you name at the end of the code.

## Supplemental Excel Formula
The most basic function of this program - identifying whether or not a keyword is present in a list of strings - is also available via the following formula that may be used in Microsoft Excel. This formula will be most useful if a user only desires to identify deaths of a single category (ex. Only interested in Heat Related deaths and only wants to pull out deaths with Heat Related keywords). A key drawback of using the Excel formula is that it does not include logic on the Manner of Death like the Python program. Therefore, this formula should only be used to apply keywords to death records of appropriate manner of death (ex. Do not apply the Heat Related keyword list to Natural deaths).
The formula: =IF(SUMPRODUCT(--ISNUMBER(SEARCH($X$1:$X$5,A2)))>0, 1, "")
- Formula description: This formula will check if a cell (A2) contains any of the strings in cells X1 through X5 (the keyword list, one keyword in each cell). If a keyword is found in A2, the formula will count 1, and if two keywords are found the formula counts 2. The final IF statement puts a 1 in the output cell if the sum of the keyword search is 1 or greater. The user may then apply the formula to cells A3, A4, A5, ...AX to apply the keyword list to all desired data. 
- Users should update the cell labels in the formula to reflect the keyword list and data they are searching.
