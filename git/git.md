

* set remote repository
…or create a new repository on the command line
echo "# note" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:lrh/note.git
git push -u origin master

