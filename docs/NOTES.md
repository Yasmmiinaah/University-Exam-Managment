## Notes / Improvements Included

### 1) Fixed inconsistent test data (registration_id)
In the original script there was an insert into `examresults` referencing `registration_id = 1002`,
but `REGISTER` had `1001` and `1004`.  
This repo uses **1001 and 1002** consistently.

### 2) Safer re-runs
The scripts include **DROP USER ... CASCADE** and **DROP TABLE ...** blocks where helpful,
so the lab can be rerun without manual cleanup (best effort).

### 3) Education warning
Privileges like `GRANT ANY PRIVILEGE` are used only to simplify a lab environment.
Avoid this in real systems.
