# AddEtckeeperGitRemoteForEtcBackup
Created Thursday 28 April 2022

Overview
--------

Tracking configuration changes in etckeeper is great, but even better is storing in an off-system private repository, preferably one with a decent web interface to the repo (makes browsing the repo much friendlier). Ideally you will have a local git server for this rather than some cloud service.

Since we only commit interactively (that is etckeeper autocommits are disabled), we don't store passwords or use a passwordless SSH key on the system, which would be required if push without human intervention were required. Thils will mean you need enter the appropriate password on push.

Common configuration
--------------------


1. Set up a repo on your git server for receiving the etckeeper push (e.g. ``https://gitserver.example.com/example-com-etckeeper/systemname.git`` where example-com``-etckeeper`` is an 'organization' which grants push access to ``youruserid`` on the ``systemname.git`` repository. The owner of ``example-com-etckeeper`` would ideally *not* be ``youruserid``).


Case 1: Connection and authentication via HTTPS
-----------------------------------------------

### If git server has a private (self-signed) CA certificate


1. Put the CA certificate for the server in ``/etc/etckeeper/git-ssl/ca-private.your-server.example.com.pem``
2. Configure git to use the certificate for ``gitserver.example.com by executing:``

	etckeeper vcs config http.https://gitserver.example.com/.sslCAInfo /etc/etckeeper/git-ssl/ca-private.your-server.example.com.pem # Adjust using your git server and system certificate name


### For any git via HTTPS connection

If you have two factor authentication enabled on your git server, or are just following best practices, you may need or want to use a revokable 'token' instead your main login password. Depending on the git system in use you may be able to limit the access granted to the token more precisely than with the main account password.


1. Convenience option: Configure the username of the account to use when pushing by executing:

	etckeeper vcs config credential.https://gitserver.example.com youruserid # Adjust using your git server and git userid

 2. Add your git server as a 'remote' to the local etckeeper repo:
	etckeeper vcs remote add origin https://gitserver.example.com/example-com-etckeeper/systemname.git # Adjust using your git server and system name
 

3. Push the repo so far to ``gitserver.example.com`` and make your 'origin' remote the default 'upstream' for the 'main' branch

	etckeeper vcs push --set-upstream origin main # If your primary branch is not 'main' use yours (e.g. 'master' is still common)


You will be prompted for the password for the account you configured in step ``1.`` above (``youruserid``). Use the token instead of a password if you generated one, otherwise use your account password (if you account has two factor authentication enabled, using your account password will likely fail and you will need to generate a token; details depend on your git server).

If all is well you will see the usual git push messages on the terminal.

Case 2: Connection and authentication via SSH
---------------------------------------------


1. Make sure you have have the private key for the public key you have at ``gitserver.example.com`` (not a real server)

 2. Add your git server as a 'remote' to the local etckeeper repo:
	etckeeper vcs remote add origin ssh://git@gitserver.example.com/example-com-etckeeper/systemname.git # Adjust using your git server and system name
 

3. Push the repo so far to ``gitserver.example.com`` and make your 'origin' remote the default 'upstream' for the 'main' branch

	etckeeper vcs push --set-upstream origin main # If your primary branch is not 'main' use yours (e.g. 'master' is still common)

   Unless you have an ssh-agent active and have previously connected to this server on this host, you will be prompted for the password for the SSH private key associated with the public key on ``gitserver.example.com``. If you enter it correctly, you should see the usual git push messages on the console.

Finalize common configuration
-----------------------------

### If you added a private (self-signed) CA certificate, above

Commit your certificate:
	etckeeper commit "Add self-signed CA for gitserver.example.com"


### In all cases


1. Enable push on commit by editing ``/etc/etckeeper/etckeeper.conf`` to contain:

	PUSH_REMOTE="origin"


2. Test by committing this change by executing:

	etckeeper commit "Enable push to gitserver (origin) on commit"

   You should be prompted for the necessary credentials, and if entered corectly you should see the usual git push messages on the console.

Finally, commit to LBU
----------------------
Execute:
	lbu commit


