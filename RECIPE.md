# BOSH Release Requirements Checklist For Maria DB

##Packaging
  * Is there a usuable binary available?  NO
  * Where is the source code located?
    https://downloads.mariadb.org/
    https://downloads.mariadb.org/mariadb-galera/5.5.34/  #for clustering support
  * What are the compilation requirements on target platform?

```bash
    cmake -DCMAKE_INSTALL_PREFIX:PATH=/path/to/install/location
    make
    make install

    #alternate install option from source without requiring make install
    #db will run from source directory
    ./scripts/mysql_install_db --srcdir=$PWD --datadir=/path/to/data/dir --user=$LOGNAME
```

##Job Creation
  * How to run process? eg. start, stop, restart.Control Script? Helpful
  wrapper script? ({name}_ctl)
  ```bash
    #Starts mysql by changing to the install directory and then calling
    #mysqld_safe
    mysql.server start
    mysql.server stop
  ```
  * How to daemonize? mysqld_safe will daemonize automatically
  * How to configure pidfile? (/var/vcap/sys/run/{name})
  ```bash
   pid-file=/var/vcap/sys.run/mysql/your-db.pid #in my.conf
  ```
  * How to set logs dir? (/var/vcap/sys/log/{name}) Logs not enabled by default
  * How to storage (db) dir? (/var/vcap/store/{name})
  ```base
  data=/var/vcap/store/mysql
  ```
  * What do config files look like? https://gist.github.com/byllc/8871383
  * What is parameterizable? (jobs/{name}/spec -> properties: …)
  * How to cluster? Leader (Master) vs Followers (Slaves)
    Galera library
    https://mariadb.com/kb/en/getting-started-with-mariadb-galera-cluster/

  ```bash
    #to create a new cluster on the master config
    wsrep_cluster_address=gcomm://

    #to choose a cluster to join, DNS names work as well
    #you simply point to the master cluster ip
    wsrep_cluster_address=gcomm://xx.xx.xx.xx
  ```


