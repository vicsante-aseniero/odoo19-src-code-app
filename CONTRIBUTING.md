# Contributing

Thank you for contributing — we welcome improvements, bug fixes and documentation updates.

Quick start
- Python: 3.11 (recommended)
- PostgreSQL: 13 or 14 (recommended)
- Clone including submodules:
```
git clone --recurse-submodules <repo-url>
cd <repo>
git submodule update --init --recursive
```

Local dev (example)
```
python -m venv .venv
source .venv/bin/activate
# install Odoo and project requirements per odoo/requirements.txt (if present)
pip install -r odoo/requirements.txt || echo "Install Odoo deps per upstream docs"
# prepare DB (see .devcontainer/odoo/instruction.txt for examples)
```

Environment and secrets
- Do not commit secrets. Use `.env` for local credentials and add it to `.gitignore`.
- Example `.env` located in `README.md`.

Submodules
- `extra-addons/openeducat_erp` is a git submodule. To update it:
```
git submodule update --remote extra-addons/openeducat_erp
# then commit the submodule pointer
git add extra-addons/openeducat_erp && git commit -m "Update openeducat_erp submodule"
```

Linting & formatting
- Use `ruff` and `black` (or preferred linters):
```
ruff check .
ruff format .
black .
```

Running tests
- If `pytest` is used in the repo, run:
```
pytest
```
- For Odoo module tests, use Odoo's test runner (example):
```
./odoo-bin --test-enable -i <module_name> --addons-path=./addons,./extra-addons,./tutorials/ --db-filter=odoo19dev
```

Development workflow
- Create a branch: `feature/<short-description>` or `fix/<short-description>`
- Make small, focused commits with conventional messages
- Open a pull request against `main` (or `develop` if used) with a clear description and testing steps

PR checklist
- [ ] Tests pass locally or in CI
- [ ] Linting/formatting passes
- [ ] No sensitive data committed
- [ ] Documentation updated where applicable
- [ ] Submodule updates included and justified

Reporting issues
- Create a clear issue with steps to reproduce, expected vs actual behavior, and logs if available.

CI & automation suggestions
- Add a CI job to run linters and tests on pushes and pull requests.
- Add a cron job to notify when submodules have new upstream commits.

Code of conduct
- Please follow a friendly, constructive tone in issues and PRs. Consider adding a `CODE_OF_CONDUCT.md` to formalize this.

Maintainers
- Maintainers/Owners: see `ANALYSIS.md` for owner suggestions per task.
