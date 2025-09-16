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



## install and create new app
```bash
bench get-app --branch <branchname> <repourl>
```
```bash
bench --site <domainname> install-app <appname>
```

```bash
bench --site <domainname> migrate
```
```bash
bench --site <domainname> build
```
bench restart
