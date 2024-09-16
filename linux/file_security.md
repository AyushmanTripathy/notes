# FILE SECURITY

### Using ls -l

- 10 character
- 1st for file type
- then user, group, others permissions

```
- rw- rw- r--
```

- each group is represent by 3 bits
- number from bits will then give

```
rw- => 110 => 6
rwxrwxr-x => 775
```

### Using chmod

-   three user categories
    1. user (u)
    2. group user (g)
    3. everybody else (o)
-   R option for recusive
-   -   or - for adding or removing
-   NOTE: directories need to have `x`

```
chmod u+x,g-x -R foo.txt
```

### Common Code

| code | on        | description                                                                                          |
| ---- | --------- | ---------------------------------------------------------------------------------------------------- |
| 400  | file      | To protect a file against accidental overwriting.                                                    |
| 500  | directory | To protect yourself from accidentally removing, renaming or moving files from this directory.        |
| 600  | file      | A private file only changeable by the user who entered this command.                                 |
| 644  | file      | A publicly readable file that can only be changed by the issuing user.                               |
| 660  | file      | Users belonging to your group can change this file, others don't have any access to it at all.       |
| 700  | file      | Protects a file against any access from other users, while the issuing user still has full access.   |
| 755  | directory | For files that should be readable and executable by others, but only changeable by the issuing user. |
| 775  | file      | Standard file sharing mode for a group.                                                              |
| 777  | file      | Everybody can do everything to this file.                                                            |
