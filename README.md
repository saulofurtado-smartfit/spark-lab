# Abaixo, como foi criado o ambiente (obs: criar é diferente de apenas usar; depois faço um tutorial de como apenas usar)

user@machine:~$ cd project-dir

user@machine:~/project-dir$ python3 -m venv .venv

user@machine:~/project-dir$ source .venv/bin/activate

(.venv) user@machine:~/project-dir$ pip3 freeze

(.venv) user@machine:~/project-dir$ pip3 install pyspark numpy pandas arrow boto3 jupyterlab

(.venv) user@machine:~/project-dir$ pyspark

>>> exit()

(.venv) user@machine:~/project-dir$ jupyler-lab

http://localhost:8888/lab

File > Shut Down

(.venv) user@machine:~/project-dir$ pip3 freeze

(.venv) user@machine:~/project-dir$ pip3 freeze > requirements.txt

(.venv) user@machine:~/project-dir$ cat requirements.txt

(.venv) user@machine:~/project-dir$ mkdir src

(.venv) user@machine:~/project-dir$ jupyler-lab

Criar um notebook chamado ‘ingestao-smartsystem-plans’ na pasta src com o código abaixo na primeira célula: 

#---------- Libs
import numpy as np
import pandas as pd; pd.set_option('max_columns', None)
import pyspark
from pyspark import SparkConf
from pyspark.sql import SparkSession 
import pyspark.sql.types as T
import pyspark.sql.functions as F
#---------- SparkConf
conf = (SparkConf()
        .set('spark.sql.repl.eagerEval.enabled', True)
        .set('spark.sql.execution.arrow.pyspark.enabled', True)
        .set('spark.sql.session.timeZone', 'UTC')
        .set('spark.driver.memory','32G')
        .set('spark.ui.showConsoleProgress', True)
        .set('spark.driver.bindAddress', '127.0.0.1'))
#---------- SparkSession
spark = (SparkSession
         .builder
         .config(conf=conf)
         .master('local[*]')
         .appName('PySpark')
         .getOrCreate())

spark
