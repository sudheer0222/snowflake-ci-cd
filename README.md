# Snowflake CI/CD Migration Pipeline

This repository automates Snowflake SQL migrations using GitHub Actions and the official [Snowflake CLI](https://docs.snowflake.com/en/developer-guide/snowcli).

## Folder Structure

```
.
├── .github/
│   └── workflows/
│       └── snowflake-migrations.yml
├── .snowflake/
│   └── config.toml
└── migration-scripts/
    ├── v1/
    ├── v2/
    └── v3/
```

- **migration-scripts/**: Place your versioned SQL migration scripts here (e.g., `v1/001_init.sql`).
- **.snowflake/config.toml**: Snowflake CLI connection configuration.
- **.github/workflows/snowflake-migrations.yml**: GitHub Actions workflow for migrations.

## Usage

### 1. Configure Connections

Edit `.snowflake/config.toml` and define your environments (e.g., `preprodconnection`).

### 2. Add Secrets

In your GitHub repository, add the following secrets (for each environment as needed):

- `SNOWFLAKE_CONNECTIONS_MYCONNECTION_AUTHENTICATOR`
- `SNOWFLAKE_CONNECTIONS_MYCONNECTION_USER`
- `SNOWFLAKE_CONNECTIONS_MYCONNECTION_ACCOUNT`
- `SNOWFLAKE_CONNECTIONS_MYCONNECTION_PRIVATE_KEY_RAW`

### 3. Running the Pipeline

- On every push to `main`, the workflow runs automatically.
- You can also trigger it manually and select the target environment.

### 4. How It Works

- The workflow checks out your code, sets up the Snowflake CLI, and runs all SQL scripts in each versioned folder in order using the selected connection.

## Example: Adding a Migration

1. Add a new folder (e.g., `v4`) under `migration-scripts/`.
2. Place your `.sql` migration files inside.
3. Commit and push to `main` to trigger the workflow.

---

**For more details, see the workflow file at `.github/workflows/snowflake-migrations.yml`.**