Python/Django + JWT auth backend
================================

### Technical Stack

	- Python/Django: python 3.6,

	- Database: PostgreSQL

	- JWT auth based RESTful API

### Create server

	```
	$ python3.6 -m venv env3

	$ source env3/bin/activate

	$ pip install coreapi django djangorestframework djangorestframework-jwt

	$ pip freeze > requirements.txt

	$ django-admin startproject config .
	```

### Get static files

	```
	$ ./manage.py collectstatic
	```

### Migrate models into database
	```
	$ ./manage.py makemigrations
	```

### Create admin user on server

	```
	$ ./manage.py migrate

	$ ./manage.py createsuperuser
	```

### Pre-requirement

	1. Install GDAL library for GeoIP/GeoLocation support

	- MacOS
		```
		$ brew install postgis
		$ brew install gdal
		$ brew install libgeoip
		```

	- Ubuntu
		```
		$ sudo apt-get install binutils libproj-dev gdal-bin
		```

### Run server with command line
	```
	$ ./manage.py runserver 0.0.0.0:8000
	```

### Run server with Docker
```
$ docker network create --subnet=172.17.0.0/16 headshotnet

$ docker run -d \
	-e DATABASE_ENGINE=django.db.backends.postgresql_psycopg2 \
	-e DATABASE_NAME=headshot \
	-e DATABASE_USER_NAME=postgres \
	-e DATABASE_PASSWORD=postgres \
	-e DATABASE_HOST=206.189.193.17 \
	-e DATABASE_PORT=5432 \
	-p 8000:8000 \
	--net headshotnet \
	--ip 172.20.0.2 \
	--name headshot-backend \
	valeriia333/headshot-backend
```


### Server urls

- http://127.0.0.1:8000

- http://127.0.0.1:8000/api/auth/token/obtain/

- http://127.0.0.1:8000/api/echo

### Troubleshooting

- Remove all migrations
```
	$ find . -path "*/migrations/*.py" -not -name "__init__.py" -delete
	$ find . -path "*/migrations/*.pyc"  -delete
```