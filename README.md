## Telmekom-web-base3


### Backend


- U **home** folderu projekta napraviti direktorijum **storage**

bash```
mkdir ~/storage
```

klonirati **dev** branch ovog projekta

bash```
git clone --branch dev git@github.com:digital-cube/telmekom-web-base3.git
```

- U okviru **telmekom-web-base3** foldera klonirati **base3** (__work in progress__), i

bash```
cd telmekom-web-base3
git clone --branch BASE3_dev_tws git@github.com:digital-cube/BASE.git base
```

- Zatim ga linkovati posebno za svaki od mikroservisa

bash```
cd users && ln -sf ../base . && cd ..
cd blog && ln -sf ../base . && cd ..
```

- Kreirati virtual environment projekta

bash```
python3 -m venv .venv && .venv/bin/pip install wheel && .venv/bin/pip install -r requirements.txt
```
kao i pojedinacne virtual environmente za mikroservise 

bash```
cd users && python3 -m venv .venv && .venv/bin/pip install wheel && .venv/bin/pip install -r requirements.txt && cd ..
cd blog && python3 -m venv .venv && .venv/bin/pip install wheel && .venv/bin/pip install -r requirements.txt && cd ..
```

- Kao **postgres** superuser kreirati **telmekom** usera

__(psql client zahteva da u pg_hba.config fajlu postgres bude setovan kao trust)__

bash```
create role telmekom with login createdb password '123'
```
- I na kraju kao **telmekom** user kreirati baze koristeci **template1**

bash```
psql -U telmekom template1
create database telmekom_web_users;
create database telmekom_web_posts;
create database telmekom_web_photos;
create database telmekom_web_tags;
create database telmekom_web;
```

### Frontend 

- Kreirati folder za front (npr telmekom-website) u okviru home foldera

mkdir ~/telmekom-website

rsyncovati izbildani sadrzaj sa lokala (prilagoditi Nikolin primer ispod za stvarne lokalne putanje i putanje na serveru)

rsync -var -e 'ssh' /Users/nikolajovic/work/telmekom-web-base3/angular/dist telmekom.dev@telmekom.dev:/home/telmekomdev/telmekom-website --delete --exclude='browser/assets/uploaded-images'




## Work notes for the PyCharm 
--- 
opening project from pycharm

1. open every service and attach project, at the end open root foler and
attach it

 - open users service 
 - open posts service and choose Attach
 - ... open all other servies at the same way

 - open root foler and choose Attach (pycharm will group all services
   in root folder, but it will be independent when they starts)
