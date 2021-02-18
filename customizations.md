## FYI: V2 to V4 Migration issue
I had installed Crater V2 on January 1st, 2020 and recently ran into an upgrade issue that may impact. 
I upgraded to V4 using the documented manual method. I ran the migrations per instructions and was able to login into my local version on my PC. 
I ran my 2020 reports to check if the totals matched the V4 version. All looked good. 
I attempted to create a new invoice and got the following error:

`[2021-02-17 11:42:00] production.ERROR: SQLSTATE[42S22]: Column not found: 1054 Unknown column 'items.unit_id' in 'on clause'`

After a review of the V4 migrations folder, I determined that one of the migrations was changed on 1/5 shortly after I had cloned the project.
`2017_04_11_081227_create_items_table.php`
The modified migration did not run again during the upgrade since the migration already ran on 1/1/2020. 
I believe best practice is to create a new migration in order to alter a table

Attached the migration, I ran to add unit_id and the foreign key constraint on unit_id to the table.

## Notes
Invoice numbers are incremented from the last invoice used so changing the prefix to INV-2021 of the first invoice at the start of the year
should work for the rest of the year.
