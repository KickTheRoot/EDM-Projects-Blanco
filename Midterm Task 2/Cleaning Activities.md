{{ let
    Source = Excel.Workbook(File.Contents("C:\Users\COMLAB\Downloads\Uncleaned_DS_jobs.xlsx"), null, true),
    Uncleaned_DS_jobs_Sheet = Source{[Item="Uncleaned_DS_jobs",Kind="Sheet"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(Uncleaned_DS_jobs_Sheet, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"index", Int64.Type}, {"Job Title", type text}, {"Salary Estimate", type text}, {"Job Description", type text}, {"Rating", type number}, {"Company Name", type text}, {"Location", type text}, {"Headquarters", type any}, {"Size", type any}, {"Founded", Int64.Type}, {"Type of ownership", type any}, {"Industry", type any}, {"Sector", type any}, {"Revenue", type any}, {"Competitors", type any}}),
    #"Extracted Text Before Delimiter" = Table.TransformColumns(#"Changed Type", {{"Salary Estimate", each Text.BeforeDelimiter(_, "("), type text}}),
    #"Inserted Literal" = Table.AddColumn(#"Extracted Text Before Delimiter", "MIn Sal", each "101", type text),
    #"Inserted Literal1" = Table.AddColumn(#"Inserted Literal", "Max Sal", each "101", type text),
    #"Added Custom" = Table.AddColumn(#"Inserted Literal1", "Role Type", each if Text.Contains([Job Title], "Data Scientist") then
"Data Scientist"
else if Text.Contains([Job Title], "Data Analyst") then
"Data Analyst"
else if Text.Contains([Job Title], "Data Engineer") then
"Data Engineer"

else if Text.Contains([Job Title], "Machine Learning") then
"Machine Learning Engineer"
else
"other"),
    #"Added Custom1" = Table.AddColumn(#"Added Custom", "Location Correction Column", each if [Location]= "New Jersey" then ", NJ"
else if [Location] = "Remote" then ", other"
else if [Location]= "United States" then ", other"
else if [Location]= "Texas" then ", TX"
else if [Location]= "Patuxent" then ", MA"
else if [Location]= "California" then ", CA"
else if [Location]= "Utah" then ", UT"
else [Location]),
    #"Split Column by Delimiter" = Table.SplitColumn(#"Added Custom1", "Location Correction Column", Splitter.SplitTextByDelimiter(",", QuoteStyle.Csv), {"Location Correction Column.1", "Location Correction Column.2"}),
    #"Changed Type1" = Table.TransformColumnTypes(#"Split Column by Delimiter",{{"Location Correction Column.1", type text}, {"Location Correction Column.2", type text}}),
    #"Replaced Value" = Table.ReplaceValue(#"Changed Type1","Anne Arundel","MA",Replacer.ReplaceText,{"Location Correction Column.2"}),
    #"Renamed Columns" = Table.RenameColumns(#"Replaced Value",{{"Location Correction Column.2", "State Abbreviations"}}),
    #"Inserted Text Before Delimiter" = Table.AddColumn(#"Renamed Columns", "MinCompanySize", each Text.BeforeDelimiter([Size], " "), type text),
    #"Inserted Text Between Delimiters" = Table.AddColumn(#"Inserted Text Before Delimiter", "MaxComapanySize", each Text.BetweenDelimiters([Size], " ", " ", 1, 0), type text),
    #"Replaced Value1" = Table.ReplaceValue(#"Inserted Text Between Delimiters",-1,0,Replacer.ReplaceValue,{"Revenue"}),
    #"Filtered Rows" = Table.SelectRows(#"Replaced Value1", each ([Industry] <> -1)),
    #"Filtered Rows1" = Table.SelectRows(#"Filtered Rows", each ([Revenue] <> "Unknown / Non-Applicable") and ([Competitors] <> -1)),
    #"Split Column by Delimiter1" = Table.SplitColumn(#"Filtered Rows1", "Company Name", Splitter.SplitTextByDelimiter("#(lf)", QuoteStyle.Csv), {"Company Name.1", "Company Name.2"}),
    #"Changed Type2" = Table.TransformColumnTypes(#"Split Column by Delimiter1",{{"Company Name.1", type text}, {"Company Name.2", type number}}),
    #"Renamed Columns1" = Table.RenameColumns(#"Changed Type2",{{"Company Name.2", "Rates"}})
in
    #"Renamed Columns1" }}
