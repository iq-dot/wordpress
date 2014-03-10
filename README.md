Wordpress on OpenShift
======================

The backend database is MySQL and the database name is the 
same as your application name (using getenv('OPENSHIFT_APP_NAME')). You can name
your application whatever you want.  However, the name of the database will always
match the application so you might have to update .openshift/action_hooks/build.


Running on OpenShift
----------------------------

Note: When you upload plugins and themes, they'll get put into your OpenShift data directory
on the gear ($OPENSHIFT_DATA_DIR).  If you'd like to check these into source control, download the 
plugins and themes directories and then check them directly into php/wp-content/themes, php/wp-content/plugins.

Notes
=====

GIT_ROOT/.openshift/action_hooks/deploy:
    This script is executed with every 'git push'. By default, this script will create
    the database tables that this example uses.

    If you need to modify the schema, you could create a file 
    GIT_ROOT/.openshift/action_hooks/alter.sql and then use
    GIT_ROOT/.openshift/action_hooks/deploy to execute that script (make sure to
    back up your application + database w/ 'rhc app snapshot save' first :) )

Security Considerations
-----------------------
Consult the WordPress documentation for best practices regarding securing your wordpress installation.  OpenShift 
automatically generates unique secret keys for your deployment into wp-config.php, but you may feel more
comfortable following the WordPress documentation directly.
