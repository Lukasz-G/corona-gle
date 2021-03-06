# Scraping DOIs elsevier
The script for scraping has been coded to write the results in a file, or in a database.

In both versions, the input file is declared in a variable called "file\_"

## File output
Writes the output in a file named [input_file]_res.csv.
Because this version is really slow, it's recomended to use the version that writes into a database

## Database output
This version is much faster.
In a first phase it populates the database with the DOIs and the sha values of the papers. The conditions to execute this phase are:
- the number of lines of the input file are different than the number of documents in the database
- it only inserts if the document it hasn't been registered in the database already (this can be improved to make it faster)

It uses a config file located in the same folder.

# Misc
## Command start mongodb container with persistance
`docker run -d -v \`pwd\`/database:/data/db -p 127.0.0.1:27017-27019:27017-27019 mongo`

Due to the value of the param `-p` the container is only accesible from the local machine.

## Export and export content mongo

`mongoexport --db papers --collection papers_elsevier -o /data/db/export_elsevier.json --jsonArray`

`mongoimport --db papers --collection papers_elsevier --/drop --file /data/db/export_elsevier.json --jsonArray`