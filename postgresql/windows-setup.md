# Windows Setup

**Install**:

Look for latest versions.

- postgresql.exe
- pgadmin.exe

If you are using WSL follow these steps:

1. Make Sure PostgreSQL Listens on All Interfaces

Open `postgresql.conf` (on Windows):

```sh
C:\Program Files\PostgreSQL\15\data\postgresql.conf
```

Find this line:

```sh
#listen_addresses = 'localhost'
```

And change it to:

```sh
listen_addresses = '*'
```

2. Allow Local Connections in `pg_hba.conf`

Edit `pg_hba.conf` (same folder as `postgresql.conf`):

Add this line at the bottom:

```sh
host    all             all             0.0.0.0/0               md5
```

3. Restart PostgreSQL Server

After making config changes, restart the PostgreSQL service:

- Open Services (Win+R → `services.msc`)
- Find PostgreSQL, right-click → Restart

4. Use Windows Host IP (not localhost) in WSL

Inside WSL, `localhost` refers to WSL itself, not Windows.

To connect to the Windows-hosted PostgreSQL from WSL, use Windows' local IP.

Get it with:

```sh
cat /etc/resolv.conf | grep nameserver
```

You'll see something like:

```sh
nameserver 172.24.176.1
```

Use that **IP** in your Prisma `.env` file:

```sh
DATABASE_URL="postgresql://postgres:your_password@172.24.176.1:5432/your_db"
```

5. Firewall May Be Blocking Port 5432

Make sure Windows Firewall isn’t blocking PostgreSQL’s port:

- Go to Windows Defender Firewall
- Advanced Settings → Inbound Rules
- Add a new rule:
  - Port: 5432
  - Allow connection
  - For all profiles
  - Name it like "PostgreSQL WSL Access"

6. Test Prisma

```sh
npx prisma migrate dev
```
