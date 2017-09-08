Fluent batch jobs
-----------------

Η υποβολή εργασιών επίλυσης που χρησιμοποιούν το λογισμικό Fluent προϋποθέτει ότι έχετε ήδη στον τοπικό σας υπολογιστή ένα μοντέλο `model.jou` σε Fluent και θέλετε να το επιλύσετε στην υποδομή του υπολογιστικού πλέγματος. Πρέπει να διαμορφώσετε ένα αρχείο μέ κάποιο όνομα, π.χ. job.sh και να το προσαρμόσετε στα δεδομένα που αφορούν στο πρόβλημά σας.

* Αλλάξτε τη γραμμή `#$ -M chfrag ΑΤ central.ntua.gr` βάζοντας το δικό σας email για να λαμβάνετε ειδοποιήσεις σχετικά με την πορεία της επίλυσης.

```bash
#!/bin/bash
#
#$ -cwd
#$ -M chfrag ΑΤ central.ntua.gr (όπου ΑΤ θέλει το @ χωρίς κενά)
#$ -m bae
#$ -S /bin/bash
#$ -o out.txt
#$ -e err.txt
#$ -notify
# -- Use the following, so you can catch the errors thrown by SGE if your job fails to submit
#$ -w e


PATH=/ansys_inc/v170/fluent/bin:$PATH
MYINPUTFILE=/home/chfrag/Fluent_Batch/model.jou
NSLOTS=12

fluent 3d -ssh -sge -sgeckpt fluent_ckpt -g -t$NSLOTS -i $MYINPUTFILE
```