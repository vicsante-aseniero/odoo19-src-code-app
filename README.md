# Odoo 19 Community — Source Code Project

Summary
- Odoo 19 Community source included in `./odoo` (branch `19`).
- Third-party education module: `openeducat_erp` (git submodule) found at `./extra-addons/openeducat_erp` — https://github.com/openeducat/openeducat_erp (https://openeducat.org).
- Odoo developer tutorials are available in `./tutorials` (see Odoo docs: https://www.odoo.com/documentation/19.0/developer/tutorials/setup_guide.html).

Repository layout (important paths)
- `odoo/` — Odoo 19 community source (branch `19` expected)
- `addons/` — local custom/additional addons
- `extra-addons/openeducat_erp/` — git submodule for OpenEduCat ERP
- `tutorials/` — Odoo tutorial modules
- `config/` — configuration files (e.g., `odoo-cmd.conf`)
- `.devcontainer/odoo/` — development container setup and helper scripts

Quick start (developer)
1. Clone including submodules:
```
 git clone --recurse-submodules <repo-url>
 # or, if already cloned:
 git submodule update --init --recursive
```

2. Prepare Postgres (example dev container setup uses `postgres-dev`):
```
# copy SQL and apply (example)
docker cp ./.devcontainer/odoo/setup.sql postgres-dev:/tmp/odoo-setup.sql
docker exec -it postgres-dev psql -U postgres -d postgres -f /tmp/odoo-setup.sql

# check postgres readiness
pg_isready -d odoo19dev -h postgres-dev -p 5432 -U odoo_user
```

3. Start Odoo (first-time initialisation):
```
./odoo-bin -i all --addons-path=./addons/,./extra-addons/openeducat/,./tutorials/    --database=odoo19dev --db_user=odoo_user --db_password=<your_password> --dev=all
```

Or to update modules while using config:
```
./odoo-bin -u all -c ./config/odoo-cmd.conf --dev=all
```

4. Kill port if Odoo gets stuck:
```
sudo lsof -i :8069
sudo kill -9 <PID>
fuser -n tcp -k 8069
```

Submodule notes
- `openeducat_erp` is a git submodule; update with:
```
git submodule update --remote extra-addons/openeducat_erp
git add extra-addons/openeducat_erp && git commit -m "Update openeducat_erp submodule"
```

Security & configuration
- Avoid committing secrets. Use environment variables or a `.env` and secure config management for DB credentials.
- Verify Postgres version compatibility (use recommended Postgres for Odoo 19).

Contributing & next steps
- Add `CONTRIBUTING.md` and specify Python/Postgres versions and formatting/lint rules.
- Consider adding `docker-compose` or simple setup scripts for reproducible dev environments.

Links
- Odoo: https://github.com/odoo/odoo (branch 19)
- OpenEduCat: https://github.com/openeducat/openeducat_erp
- Tutorials: https://www.odoo.com/documentation/19.0/developer/tutorials/setup_guide.html
