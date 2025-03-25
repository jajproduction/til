# Export Database

Exporting your MariaDB database is a great approach for transferring both schema and data to another computer. MariaDB is compatible with `mysqldump`, so you can use it to export your data and then import it on the other computer.

1. Export the Database

On the original computer, use the `mysqldump` command to create a dump file:

```bash
mysqldump -u your_user -p your_database_name > your_database_dump.sql
```

- Replace `your_user` with your MariaDB username.
- Replace `your_database_name` with the name of your database.
- This will prompt you for your password and create a file called `your_database_dump.sql` containing both the schema and data.

2. Transfer the Dump File

Move the `your_database_dump.sql` file to the other computer. You can use USB, cloud storage, or a file transfer tool like `scp` to move it.

3. Import the Database on the New Computer

On the new computer, first make sure MariaDB is installed and running. Then, use the following command to import the dump file:

```bash
mysql -u your_user -p your_database_name < your_database_dump.sql
```

- If the database does not already exist, create it first:

```bash
CREATE DATABASE your_database_name
```

4. Verifying the Import

After importing, verify the data by checking a few tables in MariaDB or using Prisma to ensure everything it set up as expected.
