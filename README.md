Django on OpenShift Express
============================

OSQA is the free, open source Q&A system you've been waiting for. Your OSQA site is more than just an FAQ page, it is a full-featured Q&A community. Users earn points and badges for useful participation, and everyone in the community wins. 

This git repository helps you get up and running quickly with a OSQA system on OpenShift Express.  The project name used in this repo is 'osqa' but you can feel free to change it.  Right now the backend is sqlite3 and the database runtime is @ $OPENSHIFT_DATA_DIR/sqlite3.db.

When you push this application up for the first time, the sqlite database is copied from wsgi/osqa/sqlite3.db. You can delete the database from your git repo after the first push (you probably should for security). If you do anything that requires an alter table, you could add the alter statements in GIT_ROOT/.openshift/action_hooks/alter.sql and then use GIT_ROOT/.openshift/action_hooks/deploy to execute that script (make sure to back up your database with rhc-snapshot first)


Running on OpenShift
----------------------------

Create an account at http://openshift.redhat.com/

Create a wsgi-3.2 application

    rhc-create-app -a osqa -t wsgi-3.2

Add this upstream seambooking repo

    cd osqa
    git remote add upstream -m master git@github.com:lulinqing/OSQA.git
    git pull -s recursive -X theirs upstream master
    
Then push the repo upstream

    git push

That's it, you can now checkout your application at (default admin account is admin/admin):

    http://osqa-$yournamespace.rhcloud.com

