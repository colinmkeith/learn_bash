Shell Expansion
===============

Bash has a lot of amazing built-in functionality that can help manipulate your variables.

This can save you a lot of time and resources, using shell expansion instead of running scripts.


1. Devise a way to rename all files call *.mak* to *.mk*


A. You can find files matching specific criteria using:

````find . -name '*.mak' -print````

We can manipulate these using shell expansion if we stick them into a Bash variable which we can do with a for-each loop.
In this case the shell expansion is a simple regexp search-and-replace using

````${ var / search / replace }````

Putting all of that together


````for file in $(find . -name '*.mak' -print); 
    do
      mv $file ${file/.mak/.mk};
    done````

A. Using pipes:

We get the list from ````find```` as above, but use sed to create two names, x1.mak and x1.mk.
We then pipe two names at a time to ````xargs```` using the ````-n2```` switch:

````find . -name '*.mak' -print |sed 's/^\(.*\)\.mak$/& \1\.mk/' |xargs -n2 mv````


Warning: This breaks horribly on files with white spaces.
