# lit staging


ssh leader@80.238.231.10

ssh leader@101.46.57.158
cd frappe-bench
ls
cd sites
ls
cd production-bench
ls
cd sites
cd ..
come to production-bench

cd production-bench
cd apps
cd foxerp
git status

git pull upstream <branch name>

cd leaderit
git pull upstream <branch name>

bench --site leaderstaging15.foxerp.com migrate

bench --site leaderstaging15.foxerp.com clear-cache

bench --site leaderstaging15.foxerp.com clear-website-cache
bench --site leaderstaging15.foxerp.com  build
bench restart



install and create new app


bench --site <domain name> install-app <app name>

