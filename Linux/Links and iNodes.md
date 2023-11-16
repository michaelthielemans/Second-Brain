#linux
## iNodes table

| number | metadata | block storage location | 
|--|--|--|
| 321 | owner, group, timestamp, size | block index 4343|


## Directory is a file

| Directory content | inode | 
|--|--|
|. | inode of the directory itself |
|..  | inode of upper level dir |
| namefolder1 | inode to folder1 |
|namefolder2 | inode to folder2 |
## Hard links

`ln <destination file> <linkname> `

## Soft links

`ln -s <destination file> <linkname>`

