# shutil

#### shutil.move
```python
>>> shutil.move( 'asis.what', 'tobe.what' )

>>> help( shutil.move )
move(src, dst, copy_function=<function copy2 at 0x...>)
    Recursively move a file or directory to another location. This is
    similar to the Unix "mv" command. Return the file or directory's
    destination.

    If the destination is a directory or a symlink to a directory, the source
    is moved inside the directory. The destination path must not already
    exist.

    If the destination already exists but is not a directory, it may be
    overwritten depending on os.rename() semantics.

    If the destination is on our current filesystem, then rename() is used.
    Otherwise, src is copied to the destination and then removed. Symlinks are
    recreated under the new name if os.rename() fails because of cross
    filesystem renames.

    The optional `copy_function` argument is a callable that will be used
    to copy the source or it will be delegated to `copytree`.
    By default, copy2() is used, but any function that supports the same
    signature (like copy()) can be used.
    
    A lot more could be done here...  A look at a mv.c shows a lot of
    the issues this implementation glosses over.
```
