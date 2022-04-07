@keith
DevOps corner
https://drive.google.com/file/d/1lG21JYekY3OXSYrczLZLEXepGxymf589/view?usp=sharing

1. Create a shared env file as the canonical version
2. Mount a network drive
  * keybase (kbfuse)
  * s3 (s3fuse)
3. Symlink the network copy to local drive
4. Check the symlink in
5. Separate files for each env


Other options:
* wrap a secrets manager
* wrap 1 password

Q: How to deal with needing specific env vars in a one-time setup script?
Chad: Get them from a running node in that env

Q: How do we handle that some env vars are SECRET (keys and passwords) and some are just CONFIG (urls and flags)?
Chad: Treat them all as secret.  Config values are just lower risk secrets that tell you something about the app (much like leaking a Gemfile)

Important consideration: How hard is it for devs to change production values?  If it's hard to change prod secrets and everyting is a secret, they'll feel forced to workaround the mechanism.