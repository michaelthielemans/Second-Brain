#Git
# Cloning a git repo

1. git clone https://github.com/michaelthielemans/Second-Brain.git
or
2. git clone git@github.com:michaelthielemans/Second-Brain.git

# How to push to a github repo

1. ==pushing has to be done with SSH==
2. generate a rsa ssh key on your laptop: [[SSH configuration]]
	1. (old computers) `ssh-keygen -t rsa -C "Comment to identify the key"
	2. `ssh-keygen -t ed25519 -C "michaelthielemans@gmail.com"
	3. choose where the private and public key needs to be stored (textfile)
	4. open the \*.pub file and copy the content
	5. go to github and add a ssh key to your repo
4. `git push git@github.com:michaelthielemans/Second-Brain.git`
1. once github has a sshkey, more users can use the same ssh key

Check which remotes are configured
`git remote -v`


## Linking a local repo to a remote repo (github)

#### 1. Make sure you have a valid local repository
```
	git status
```
#### 2. Link the local repo to the remote repo

```
git remote add origin git@github.com:michaelthielemans/IoT-individual-project.git
```

You can replace the name 'origin' by another name if you want , this name just defines the remote url on you git instance
#### 3. Align the local main branch to the remote main branch
	If you have not yet defined the name of the local 'master' or 'main branch' you can do it by:
```
git branch -m main
```

##### Push your 'main' branch to the main branch at the remote
```
git push -u origin main
```
push it to the -upstream to the remote (->origin) main branch
if you have done this once, git knows that your main is linked to their main.

##### I you want to align the main branches (local<->remote) without pushing anything

```
git push --set-upstream origin main
```