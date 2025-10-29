Modification anomalies are problems that can occur when a database table is not properly [[Normalisation | normalised]]. They make it difficult to add, update, or delete data without causing errors or inconsistencies. There are three main types:

## Insertion Anomaly
You cannot add certain data to the table unless other, unrelated data is also provided.  
*Example:* You cannot add a new course to a student-course table unless at least one student is enrolled in it.

## Update Anomaly
When you update a piece of information in one row, you must remember to update it in all other rows where it appears. If you miss any, the data becomes inconsistent.  
*Example:* If a course name changes, you must update it in every row where that course appears.

## Deletion Anomaly
Deleting a row can unintentionally remove important information that you still want to keep.  
*Example:* If the last student enrolled in a course drops it, deleting that row also deletes all information about the course itself.