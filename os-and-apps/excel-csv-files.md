# Excel CSVs #
Sometimes you need to programmatically create CSV files to import into Excel. 
CSVs are the easiest way to express tabular data that Excel can read in a plain 
text format. Here's how to make them work:

-   Use commas to separate fields and newlines to separate records

-   Start the file with a line containing the field names, if you want a title 
    row, otherwise start with a record that has values for every field, so that 
    the format will be clear if someone reads the CSV directly.
    
-   Put doublequotes around any field that has commas in it, e.g.:

    ```python
    fieldEntry = someString # You'll usually get the string from some existing 
                            #  place over which you don't have complete control.
    if "," in fieldEntry:
        fieldEntry = "\"" + fieldEntry + "\""
    ```
    
-   If the field contains doublequotes to begin with, replace them with double 
    doublequotes `""` and put single doublequotes (this is getting confusing, 
    I know) around the whole field.
    
    ```python
    import re # regular expressions
    
    # Find every instance of a doublequote in the string and double it.
    # ****
    # IMPORTANT: If you're also checking for commas, do this before adding 
    #            surrounding quotes.
    # ****
    fieldEntry = re.sub(r'"', '""', fieldEntry) 
    ```
    
-   If any field has no value, make sure you still add a comma for it:

    ```
    Last,First,Middle,Address,Email
    Smith,John,Edward,10 Park Ln.,jesmith@somewhere.com
    Gonzalez,Tito,,25 Easy Street,titog@elsewhere.com
    ```

-   You can put spaces between fields to make it more readable, but people don't
    generally want to read a CSV raw, so it isn't really important to do so.
    
<!--
----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|
-->
