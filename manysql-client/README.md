## manysql-client Docker image!

### Why did I make this?

To be able to execute remote queries on a machine where only Docker is available (by choice, by constraint, or both).
True, the use cases could be acheived by many other means. But I find this way the cleanest and have grown to love it!

What I've included: mysql client, psql client, sqlite3, pip, and alembic. I chose these as they're most common, all work with Alembic, and because I didn't want TOO huge of an image.
Adding more clients is easy, simply update the `apk add` command on line 4 of the Dockerfile.

### How to use

Run the desired command immediately after the image name in `docker run` syntax.

Hiding the `docker run` commands in a shell/python script would be even better. That's on my TODO list.

For now, here are some examples:

```
jambii@patience ~/docker/manysql-client (master)
 🌈6⤳ sudo docker run manysql-client mysql --version
mysql  Ver 15.1 Distrib 10.1.26-MariaDB, for Linux (x86_64) using readline 5.1

jambii@patience ~/docker/manysql-client (master)
 🌈0⤳ sudo docker run manysql-client psql --version
psql (PostgreSQL) 9.6.5

jambii@patience ~/docker/manysql-client (master)
 🌈4⤳ sudo docker run manysql-client sqlite --version
3.20.1 2017-08-24 16:21:36 8d3a7ea6c5690d6b7c3767558f4f01b511c55463e3f9e64506801fe9b74dce34

jambii@patience ~/docker/manysql-client (master)
 🌈8⤳ sudo docker run manysql-client pip --version
pip 9.0.1 from /usr/lib/python2.7/site-packages (python 2.7)

jambii@patience ~/docker/manysql-client (master)
 🔥2⤳ sudo docker run manysql-client alembic --version
usage: alembic [-h] [-c CONFIG] [-n NAME] [-x X] [--raiseerr]
               {branches,current,downgrade,edit,heads,history,init,list_templates,merge,revision,show,stamp,upgrade}
```

You may also chain together commands by passing them through Bash.
Bash could also be used to investigate the container's insides in a pinch if file structure is not immediately clear from build step.

```
jambii@patience ~/docker/manysql-client (master)
 🌈5⤳ sudo docker run manysql-client bash -c "mysql --version && psql --version && alembic upgrade"
mysql  Ver 15.1 Distrib 10.1.26-MariaDB, for Linux (x86_64) using readline 5.1
psql (PostgreSQL) 9.6.5
usage: alembic upgrade [-h] [--sql] [--tag TAG] revision
alembic upgrade: error: too few arguments
```


### How to modify 

Todo: words about ONBUILD, venvs, volume mount, resource allocation


---


#### Use cases:

- Preforming remote upgrades/hotfixes/actions on-the-go, as part of a deploy, build, or test processes

- Automation flexibility or alert response; one could configure the tool in a reactionary way to run hotfix/repair commands and/or collect data on incidents

- Gathering data from a client and reporting it elsewhere, for personal debugging, or as part of everyday monitoring/testing



### What this is NOT:

- Not a replacement for serving data to clients.

- Not a replacement for long-term storage or monitoring; though, it is still possible to benefit from mounted volumes if you configure the container to leave behind mounted directory contents. I will work on providing examples of such.
