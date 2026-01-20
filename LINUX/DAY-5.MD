# Day-5


## Delving Deep into the Linux File System — Practical Notes for Students

This chapter teaches everyday file-system operations you will use frequently: how to move around, create and manage files/directories, view and edit file contents, and safely copy/move/delete files. Each section contains commands and simple examples you can try in the terminal.

---

## 1. Navigating the File System

Purpose: find where you are, list contents, and move between folders.

Basic commands
- Print current directory:
  ```bash
  pwd
  # Example output: /home/rajat
  ```
- List files and directories:
  ```bash
  ls
  ls -l        # long listing: permissions, owner, size, date
  ls -la       # include hidden files (those starting with .)
  ls -lh       # human-readable sizes (K, M, G)
  ```
- Change directory:
  ```bash
  cd /path/to/dir
  cd ~         # go to your home directory
  cd -         # go to previous directory
  cd ..        # go up one level (parent)
  ```
- Show tree view (install if needed: apt install tree):
  ```bash
  tree -L 2 ~/projects
  ```
- Quick navigation helpers:
  - `Tab` for auto-completion of filenames and directories.
  - `pushd /path` and `popd` to use a directory stack (helpful when switching contexts).
  - `cd -` returns to the last directory.

Example session:
```bash
pwd                  # /home/rajat
ls -la               # show files, including .bashrc
cd Documents
pwd                  # /home/rajat/Documents
cd ~/projects/myapp
```

---

## 2. File and Directory Management

Create, inspect, rename, change ownership, and set permissions.

- Create directory:
  ```bash
  mkdir mydir
  mkdir -p parent/child/grandchild   # -p creates parents as needed
  ```
- Remove directory:
  ```bash
  rmdir emptydir       # only removes if directory is empty
  rm -r dir_to_remove  # recursive delete (use with care)
  ```
- Create an empty file (or update timestamp):
  ```bash
  touch notes.txt
  ```
- Rename or move files/directories:
  ```bash
  mv oldname.txt newname.txt
  mv ~/downloads/report.pdf ~/documents/  # move file to folder
  ```
- Copy files and directories:
  ```bash
  cp file.txt /path/to/destination/
  cp -r myproject/ ~/backup/myproject/    # copy directory recursively
  ```
- Inspect file or directory metadata:
  ```bash
  stat file.txt
  ls -l file.txt
  ```
- Change permissions:
  ```bash
  chmod 644 file.txt      # rw-r--r--
  chmod +x script.sh      # make executable
  ```
- Change owner and group (requires sudo for other users):
  ```bash
  sudo chown rajat:staff /var/www/html -R
  ```

Safety tip: always `ls` the path before `rm -r`. Use `echo` to preview destructive commands:
```bash
echo rm -rf /some/path
```

---

## 3. Viewing and Editing Files

Quickly read files, follow logs, search inside files, and edit content.

- View entire file:
  ```bash
  cat file.txt
  ```
- Page through long files:
  ```bash
  less /var/log/syslog    # use Space to page, / to search, q to quit
  ```
- Show start or end of file:
  ```bash
  head -n 20 file.txt     # first 20 lines
  tail -n 20 file.txt     # last 20 lines
  tail -f /var/log/syslog # follow new lines in real time
  ```
- Search inside files:
  ```bash
  grep 'ERROR' app.log
  grep -Ri 'TODO' ~/projects
  ```
- Simple edits (text editors):
  - nano (beginner friendly)
    ```bash
    nano ~/projects/notes.md
    ```
  - vim (power user — steeper learning curve)
    ```bash
    vim ~/scripts/deploy.sh
    ```
- Quick text transformations:
  ```bash
  sed -n '1,50p' file.txt         # show lines 1-50
  awk '{print $1, $3}' data.csv   # print columns 1 and 3
  ```

Example: inspect and follow a web server log
```bash
sudo less /var/log/nginx/error.log
# or follow in real time
sudo tail -f /var/log/nginx/error.log
```

Always back up configuration files before editing:
```bash
sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
sudo nano /etc/nginx/nginx.conf
# after changes:
sudo systemctl reload nginx
```

---

## 4. Copy, Move, and Delete Files — Practical Patterns

Common operations and safer alternatives.

Copying
- Basic copy:
  ```bash
  cp source.txt destination.txt
  ```
- Preserve attributes (mode, timestamps, links):
  ```bash
  cp -a /source/dir /dest/dir
  ```
- Use rsync for large or repeated copies (recommended):
  ```bash
  rsync -avh --progress ~/projects/myapp/ ~/backup/myapp/
  ```

Moving / Renaming
- Move or rename:
  ```bash
  mv file.txt /other/place/
  mv oldname.txt newname.txt
  ```
- Move directory:
  ```bash
  mv ~/downloads/myfolder ~/projects/
  ```

Deleting (be careful!)
- Remove a single file:
  ```bash
  rm filename.txt
  ```
- Remove multiple files:
  ```bash
  rm file1 file2 file3
  ```
- Recursive and force remove (dangerous):
  ```bash
  rm -rf /path/to/dir
  ```
  - Double-check path; avoid running as root unless necessary.

Safer delete workflow
1. List files to confirm:
   ```bash
   ls -la /path/to/dir
   ```
2. Use `trash` / `gio trash` (desktop environments) or move to a temporary folder:
   ```bash
   mkdir -p ~/trash; mv ~/projects/oldproj ~/trash/
   ```
3. When certain, remove permanently.

Example: backup, then remove
```bash
cp -r ~/projects/demo ~/backup/demo-$(date +%F)
rm -rf ~/projects/demo
```

---

## 5. Quick Exercises (Try in your terminal)

1. Navigate and inspect:
   ```bash
   pwd
   ls -la
   cd /tmp
   mkdir -p ~/lab/demo
   ```
2. Create, edit, and view:
   ```bash
   touch ~/lab/demo/notes.txt
   echo "First note" > ~/lab/demo/notes.txt
   cat ~/lab/demo/notes.txt
   nano ~/lab/demo/notes.txt   # add another line, save
   ```
3. Copy and verify:
   ```bash
   cp -a ~/lab/demo ~/lab/demo-backup
   ls -la ~/lab
   ```
4. Safe remove:
   ```bash
   mv ~/lab/demo ~/lab/demo-to-delete
   ls -la ~/lab
   # after confirming contents:
   rm -r ~/lab/demo-to-delete
   ```

---

## 6. Quick Reference Cheat-sheet

Navigation:
- pwd, ls, ls -la, cd, cd -, tree

Create / Remove:
- mkdir -p, rmdir, rm -r (use safely), touch

Inspect:
- stat, ls -l, file, du -sh, df -h

View & Search:
- cat, less, head, tail, tail -f, grep -R

Edit:
- nano, vim, sed, awk

Copy / Move:
- cp, cp -r, cp -a, rsync -avh, mv

Permissions & Ownership:
- chmod, chown, chgrp

Safety:
- Always verify with ls before rm
- Backup config files before editing
- Prefer rsync for large or incremental copies

---