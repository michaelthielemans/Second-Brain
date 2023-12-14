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



