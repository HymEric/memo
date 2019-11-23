### 1. Large File problem
Example to address (Windows)
```shell
# clone the github repo to local
git clone xxxxxx
cd xxxxxx
# initialize LFS
git lfs install
# add tracker of your Big_File (this command can run many time to add different files)
git lfs track ".wav"
# add all files or you can just add your Big_Files
git add .
git commit -m "yyyy"
# convert your large files to lfs type which can be used
java -jar path_to_bfg/bfg-1.12.15.jar --convert-to-git-lfs "*.{wav,h5}" --no-blob-protection
# run and see your files have been tracked, if nothing, maybe you encountered an problem
git lfs lf-files
# push
git push origin master
```
Reference: [Git Large File Storage (LFS)](<https://git-lfs.github.com/>) and  [Git LFS support](<https://github.com/rtyley/bfg-repo-cleaner/releases/tag/v1.12.5>).
