### 18F Projects

We have hundreds of repos and have released dozens of tools but they're hard to find unless you know where to look (or what you're looking for.)

We are now creating a way to surface and discover the projects that 18F works on. You will be able to easily find how each engagement and repo works, who works on it, and how to contact the team that created it.

This is an ongoing **work in progress!!!** Our [Wiki](https://github.com/18F/projects/wiki) contains research notes and drafts that you might find helpful if you're also thinking about discovery.

#### Dependencies

- Python 3.5.0
- [Postgresql](http://www.postgresql.org/download/)

#### Running Locally

```sh
$ virtualenv -p python3.5 venv
$ source venv/bin/activate
$ pip install -r requirements.txt

$ createdb 18fprojects

$ python manage.py migrate
$ python manage.py runserver
```

Fixtures containing all possible federal clients and 18F business units are included.
To load:

```sh
$ python manage.py loaddata projects/fixtures/*.json
```

Sample project data may also be imported from a CSV file. If you are in 18F, export the first sheet of [this Google spreadsheet](https://docs.google.com/spreadsheets/d/1tCGfeLIzcRwyXXrNkxljRp0TTTQcxzojhFsNooe0UOs/edit#gid=0) as a CSV, then run the following command:

```sh
$ python manage.py import_projects filename.csv
```

To load data from our S3 bucket, the following env vars are needed:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_BUCKET
```

#### Using Docker (optional)

A Docker setup potentially makes development and deployment easier.

To use it, install [Docker][] and [Docker Compose][]. (If you're on OS X or
Windows, you'll also have to explicitly start the Docker Quickstart Terminal,
at least until [Docker goes native][].)

Then run:

```sh
docker-compose run app python manage.py migrate
```

Once the above command is successful, run:

```sh
docker-compose up
```

This will start up all required servers in containers and output their
log information to stdout. If you're on Linux, you should be able
to visit http://localhost:8000/ directly to access the site. If you're on
OS X or Windows, you'll likely have to visit port 8000 on the IP
address given to you by `docker-machine ip default`. (Note that this
hassle will go away once [Docker goes native][] for OS X/Windows.)

##### Accessing the app container

You'll likely want to run `manage.py` to do other things at some point.
To do this, it's probably easiest to run:

```sh
docker-compose run app bash
```

This will run an interactive bash session inside the main app container.
In this container, the `/projects` directory is mapped to the root of
the repository on your host; you can run `manage.py` from there.

Note that if you don't have Django installed on your host system, you
can just run `python manage.py` directly from outside the container--the
`manage.py` script has been modified to run itself in a Docker container
if it detects that Django isn't installed.

[Docker]: https://www.docker.com/
[Docker Compose]: https://docs.docker.com/compose/
[Docker goes native]: https://blog.docker.com/2016/03/docker-for-mac-windows-beta/

#### Public domain

This project is in the worldwide [public domain](LICENSE.md).   As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within   the United States, and copyright and related rights in the work worldwide are waived through   the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).  
>
> All contributions to this project will be released under the CC0 dedication. By submitting a   pull request, you are agreeing to comply with this waiver of copyright interest.
