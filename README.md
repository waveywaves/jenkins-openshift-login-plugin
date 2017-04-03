openshift-login
===============

A Jenkins plugin which lets you login to Jenkins with your account on your OpenShift installation. Focuses on enabling SSO for Jenkins within your cluster.


The primary scenario is using this plugin when Jenkins is running in a OpenShift pod, and the jobs with Jenkins operate against the
same OpenShift cluster that Jenkins is running in.  In this scenario, no additional configuration is required, but you must be running agaist v1.4 of OpenShift/Origin (https://github.com/openshift/origin/tree/release-1.4).

Otherwise, for development purposes, or for scenarios where the OpenShift pod defaults do not apply, the configuration parameters are:

* service account directory:  The directory to load service account information from. Three files are referenced:  'namespace', 'ca.crt', and 'token'. They correspond to the OpenShift project, certificate, and authentication token for the service account.
* service account name:  override for the service account name used when authenticating users against OAuth (default derived from token / client secret)
* server prefix:  URI for the OpenShift OAuth endpoint
* redirect URL: URL for the OpenShift API server
* client ID:  override for the ID for the OpenShift OAuth client (default derived from service account information)
* client secret:  override for the service account token (to change permissions for the OAuth client during the OAuth authentication flows)

NOTE:  On the OAuth redirect flow during login from a browser, the construction of the redirect URL back to Jenkins when
authentication is successful examines the following elements in this order:

* first the `from` query parameter of the initial login URL is examined to see if it is a valid URL
* second the `referer` header of the initial login URL is examined to see if it is a valid URL
* lastly, the root URL for the Jenkins instance is used; if you have explicitly configured a root URL for your Jenkins
server, then you must ensure that URL has been added to the OAuth list of allowed redirect URLs on the service account
used for authenticating users 
