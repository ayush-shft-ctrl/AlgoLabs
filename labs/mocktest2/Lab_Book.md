# Mock Test 2: Terminal Lab Mock Test

**Maximum Marks:** 40  
**Environment:** You will use the class lab server through the Terminal app on your Mac. Your username is studentNN, and your roll number is RollNo. Replace these with your own username (check your ZIP file name, e.g. student07) and your roll number (e.g. 20260101001) wherever they appear below.

| Question | Topic                              | Marks  |
| -------- | ---------------------------------- | ------ |
| Q1       | Text processing: merge, sort, uniq | 10     |
| Q2       | Archiving with tar                 | 10     |
| Q3       | File permissions                   | 10     |
| Q4       | Shell script: file information     | 10     |
|          | **Total**                          | **40** |

---

## Setup: connect to the lab server from your Mac

- Open **Terminal**, unzip the ZIP, protect the key and connect:

  ```bash
  cd ~/Downloads
  unzip -o Lab_4_studentNN_Access.zip
  cd Lab_4_studentNN_Access
  chmod 600 access/ssh_key
  ssh -i access/ssh_key studentNN@98.70.53.61    # type yes if asked
  ```

- When the prompt shows `studentNN@students-lab`, you are on the server. Go to your test folder and check grading:

  ```bash
  cd ~/lab-work/mocktest2
  check_lab mocktest2    # 0/40 before you start; run it any time
  ```

- If the connection drops, run `cd ~/Downloads/Lab_4_studentNN_Access` and the `ssh` command again. Do not share your key or ZIP.

---

## General Instructions

1. Work only on the lab server, inside `~/lab-work/mocktest2`. Your answers are graded there.
2. The main folder **`RollNo_Exam`** (your roll number followed by `_Exam`) is **already created** for you. It contains the folders `commands`, `scripts`, `outputs` and `secure`.
3. Most files you need are also already created, **empty**, with the exact name. Write your answers into these files; do not rename or move them.
4. A few things do **not** exist yet; you create them when a question asks: `outputs/commands_backup.tar.gz`, `outputs/restore/` and `outputs/diff_check.txt`.
5. Run every command from inside the main folder. All paths below are relative to it.
6. Do the questions **in order**: Q2 archives the files you write in Q1.
7. Do not add any other files to `commands/`, and do not delete files unless a question asks you to.
8. Run `check_lab mocktest2` at any time to see your score.

Go into the main folder first:

```bash
cd ~/lab-work/mocktest2/RollNo_Exam
```

```text
RollNo_Exam/
├── commands/   data files          (Q1, Q2)
├── outputs/    answers and outputs (Q2, Q3, Q4)
├── secure/     permission practice (Q3)
└── scripts/    shell scripts       (Q4)
```

---

## Q1. Text Processing: Merge, Sort and Count | Marks: 10

The files `commands/students1.txt` and `commands/students2.txt` are already created and empty. Fill them with exactly these lines.

`commands/students1.txt`:

```text
Riya
Aman
Neha
Karan
```

`commands/students2.txt`:

```text
Neha
Rahul
Aman
Priya
```

Then, from the main folder (every result file below is already created):

1. Combine both files, `students1.txt` first, and save the result in `commands/all_students.txt`.
2. Sort `all_students.txt` alphabetically and save the result in `commands/sorted_students.txt`.
3. Remove the duplicate names from `sorted_students.txt` and save the result in `commands/unique_students.txt`.
4. Count the lines in `all_students.txt` and save **only the number** (no file name) in `commands/student_count.txt`.

---

## Q2. Archiving with tar | Marks: 10

The file `commands/notes.txt` is already created and empty. Fill it with exactly these lines:

```text
Linux is an operating system
tar creates archives
gzip compresses files
```

Then run these commands from the main folder, so that every path inside the archive starts with `commands/`:

1. Create a gzip-compressed archive of the whole `commands/` folder and save it as `outputs/commands_backup.tar.gz`.
2. Without extracting it, list the contents of the archive and save the list in `outputs/archive_contents.txt`.
3. Create the folder `outputs/restore/` and extract the archive into it (you get `outputs/restore/commands/`).
4. Use `diff -r` to compare the original `commands/` folder with the extracted `outputs/restore/commands/`. Save the output in `outputs/diff_check.txt`. If the extraction is correct, this file is empty.

---

## Q3. File Permissions | Marks: 10

The folder `secure/` is already created with four empty files: `public.txt`, `private.txt`, `team.txt` and `deploy.sh`. Look at their current permissions first:

```bash
ls -l secure
ls -ld secure
```

Every file starts as `-rw-r--r--` and the folder as `drwxr-xr-x`. Use `chmod` to give them exactly these permissions:

| Target               | Who gets what                                                  | Result in `ls -l` |
| -------------------- | -------------------------------------------------------------- | ----------------- |
| `secure/private.txt` | owner: read, write · group: nothing · others: nothing          | `-rw-------`      |
| `secure/public.txt`  | everyone (owner, group, others): read only, nobody can write   | `-r--r--r--`      |
| `secure/team.txt`    | keep everything as it is, only **remove read for others**      | `-rw-r-----`      |
| `secure/deploy.sh`   | owner: read, write, execute · group: read, execute · others: nothing | `-rwxr-x---` |
| `secure/` (folder)   | owner: read, write, enter · group: read, enter · others: nothing | `drwxr-x---`    |

Then:

1. Save a long listing of the folder (`ls -l secure`) in `outputs/permissions_list.txt`.
2. Try to overwrite the read-only file with `cp secure/team.txt secure/public.txt`. Save the error message in `outputs/write_denied.txt`.

---

## Q4. Shell Script: File Information | Marks: 10

The script `scripts/file_info.sh` is already created and empty. It is run with the path of one file as its argument:

```bash
./scripts/file_info.sh commands/notes.txt
```

The script must:

1. Start with the shebang line `#!/usr/bin/env bash`.
2. If no argument is given, or the file does not exist, print `Error: file not found` to standard error and exit with status `1`.
3. Otherwise, print the file name, its number of lines and its number of words (use `wc`), exactly in this format, and exit with status `0`:

   ```text
   File: commands/notes.txt
   Lines: 3
   Words: 11
   ```

Make the script executable, then run it twice. Save the requested stream in the first file and the exit status (`$?`) in the second (all files are already created):

| Run                                           | Save                                      | Exit status                 |
| --------------------------------------------- | ----------------------------------------- | --------------------------- |
| `./scripts/file_info.sh commands/notes.txt`   | standard output → `outputs/q4_notes.txt`  | `outputs/q4_notes.status`   |
| `./scripts/file_info.sh commands/missing.txt` | standard error → `outputs/q4_missing.err` | `outputs/q4_missing.status` |

---

**End of Mock Test**
