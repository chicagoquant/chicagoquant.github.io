
copy commits to another unrelated repo

```
cd SRC_DIR
git format-patch -o /tmp/some-temp-dir-for-patches --root START_COMMIT..LAST_COMMIT

cd DST_DIR
git am --3way /tmp/some-temp-dir-for-patches/*patch 
```

interactive rebase including first commit
```
git rebase -i --root
```

create empty branch, with no commits
```
git checkout --orphan NEW_BRANCH_NAME
# note it adds all the current files / dirs to index
git reset
git clean
```

add an empty commit
```
git commit --allow-empty -m "Initial commit (empty)"
```
