# ITIS6177-assignment14

# Quick Set-up (WSL)
## Pre-reqs
- Python
- pip
- postgres + psycopg2
## Installing sandman2 and postgres
1. In terminal, navigate to cloned repository and create your virtual environment
    ```
    python3 -m venv .venv
    ```
3. Activate your virtual environment
   ```
     source .venv/bin/activate
   ```
5. Install dependencies, including sandman2
   ```
     pip install -r requirements.txt
   ```
7. Create postgres role/user and database

    a. Access psql
       ```
       sudo -u postgres psql
       ```
   
    b. Create role + db
      ```
      CREATE ROLE sandman_user WITH LOGIN PASSWORD 'password';
      ALTER ROLE sandman_user CREATEDB;
      CREATE DATABASE sandman_db OWNER sandman_user;
      \q
      ```
7. Create table and insert data
   
    a. Access psql as sandman_user
       ```
       psql -h localhost -U sandman_user -d sandman_db
       ```

   b. Create table
      ```
      CREATE TABLE book (
      id serial PRIMARY KEY,
      name text NOT NULL,
      author text NOT NULL
      );
      \q
      ```

   c. Insert dummy data
     ```
     INSERT INTO  book (name, author) VALUES
    ('Omniscient Readers Viewpoint', 'singNsong'),
    ('Hero of Ages', 'Brandon Sanderson');
    ```

   d. Confirm
     ```
     SELECT * FROM book;
     \q
    ```
     <img width="498" height="325" alt="image" src="https://github.com/user-attachments/assets/6d2c36e8-a0f1-402a-971f-fbc87deb1b1a" />

9. Run sandman2 pointing at the database
  ```
  sandman2ctl postgresql+psycopg2://sandman_user:password@localhost:5432/sandman_db
  ```
<img width="862" height="121" alt="image" src="https://github.com/user-attachments/assets/9a4caa4f-80d7-4a8e-bfb1-959fdcee3dfd" />

10. While running, go to `http://localhost:5000/admin/` your browser, where you will find database information and the abilty to post, get, update, and delete.
<img width="880" height="272" alt="image" src="https://github.com/user-attachments/assets/62abc055-14b7-411c-bae0-fe246a75e450" />

12. Runs `ctrl+c` to stop the sandman2 instance
