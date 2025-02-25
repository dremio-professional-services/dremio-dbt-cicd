# dremio-dbt-cicd

## Requirements
- See: [dremio-dbt-exporter Requirements for SOURCE environment](https://github.com/dremio-professional-services/dremio-dbt-exporter?tab=readme-ov-file#requirements)
- In addition to the SOURCE environment privileges, sufficient `ALTER` and `SELECT` privileges on the relevant scopes in the TARGET environment are required
- "Read and write permissions" and "Allow GitHub Actions to create and approve pull requests" for [GitHub Actions Workflow](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#enabling-workflows-for-private-repository-forks) (-> Settings -> General -> Workflow permissions)

## Github Actions Variables and Secrets
- `DREMIO_SOURCE_ENV_URL` (Variable)
- `DREMIO_TARGET_ENV_HOST` (Variable)
- `DREMIO_USER` (Variable)
- `DREMIO_SOURCE_ENV_PAT` (Secret)
- `DREMIO_TARGET_ENV_PAT` (Secret)


## How to run
1. Specify Dremio Space (and Source) to be exported as a dbt model via `export_filter.json` and push the settings to GitHub
2. Under "Actions", select the workflow "STEP 1 - Run Dremio dbt export to git" and click "Run workflow"
3. Once the workflow job ran successfully, a new PR should be created under "Pull requests", if any changes to the models in `dbt_out_dir` were detected
4. This PR must be reviewed and approved before it gets merged into the `main` branch. New jobs will fail until the PR has been closed to avoid merge conflicts.
5. Under "Actions", select the workflow "STEP 2 - Run dbt to Dremio" and click "Run workflow"