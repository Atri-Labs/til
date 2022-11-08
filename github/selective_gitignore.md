# How to make .gitignore ignore everything except a few files

Assume the following directory structure:

```
project
│   README.md
│   file001.txt    
│
└───folder1
│   │   file011.txt
│   │   file012.txt
│   │
│   └───subfolder1
│       │   file111.txt
│       │   file112.txt
│       │   ...
│   
└───folder2
    │   file021.txt
    │   file022.txt
```
### How to ignore the entire folder?

If we want to ignore the entire `folder1` and all its constituent files, we need to write the following in `.gitignore` file.

```
folder1
```
### How to ignore all files except one in a folder?

If we want to ignore the entire `folder2` and all its constituent files except `file022.txt`, we need to write the following in `.gitignore` file.

```
folder2
!file022.txt
```
### How to ignore all files except one in a nested folder?

In case of a nested folder, we need to negate at each level.

For example, if we want to commit only `folder1/subfolder1/file112.txt` and ignore everything else in `folder1`, we need to write the following in `.gitignore` file.

```
folder1/*
!folder1/subfolder1
folder1/subfolder1/*
!folder1/subfolder1/file112.txt
```

- The first line in the code block above will ignore all the files inside `folder1`. 
- However, because of the second line, `subfolder1` will now be tracked. 
- We now need to ignore all the files inside this folder which we achieve by the third line. 
- The fourth line adds an exception for `file112.txt`.