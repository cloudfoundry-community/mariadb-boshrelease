# BOSH Release for mariadb

## Usage

To use this bosh release, first upload it to your bosh:

```
bosh target BOSH_HOST
git clone git@github.com:cloudfoundry-community/mariadb-boshrelease.git
cd mariadb-boshrelease
bosh upload release releases/mariadb-1.yml
```

