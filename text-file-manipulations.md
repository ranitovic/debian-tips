# Text File Manipulations

#### Add a space after comma, for example in MySQL dump files

```console
sed -i 's/,/, /g; s/,\s\+/, /g' dump.sql
```
