# Web-server for PRODRES

## Description:
    This is the web-server implementation of the
    [PRODRES](https://github.com/ElofssonLab/PRODRES) workflow.

    PRODRES is a fast way to obtain a Position-Specific Scoring Matrix (PSSM) or a
    jackhmmer-generated profile Hidden Markov Model (pHMM). By using the PFAM
    database as an intermediate step, we can speed up the process of profile
    creation by almost ten times if the query sequence has at least one hit in PFAM
    domains, while, at the same time, obtaining virtually the same profile as with
    a standard PSI-BLAST or jackhmmer search.

    The web-server is developed with Django (>=1.6.4)

    This software is open source and licensed under the GPL v3 license (a copy
    of the license is included in the repository)

    This implementation employs two queuing schemes for small jobs and large
    jobs respectively. For single-sequence jobs submitted via web-page, they
    will be run directly (and usually immediately after submission) at the
    front-end server. For multiple-sequence jobs or jobs submitted via the API
    (a Python script for the command-line use of the API is included in the
    package), they will be forwarded to the remote servers via the WSDL (Web
    Service Definition Language) service. Consequently, the web-server can
    handle jobs of all proteins from a proteome. 

    This implementation is suitable as as a base platform for bioinformatic
    prediction tools that need to be run for one or many sequences but the
    computational time for each sequence is short.

## Author
Nanjiang Shu

System developer at NBIS

Email: nanjiang.shu@scilifelab.se

## Reference

## Installation

1. Install dependencies for the web server
    * Apache
    * mod\_wsgi

2. Install the virtual environments by 

    $ bash setup_virtualenv.sh

3. Create the django database db.sqlite3

4. Run 

    $ bash init.sh

    to initialize the working folder

5. In the folder `proj`, create a softlink of the setting script.

    For development version

        $ ln -s dev_settings.py settings.py

    For release version

        $ ln -s pro_settings.py settings.py

    Note: for the release version, you need to create a file with secret key
    and stored at `/etc/django_pro_secret_key.txt`

6.  On the computational node. run 

        $ virtualenv env --system-site-packages

    to make sure that python can use all other system-wide installed packages

