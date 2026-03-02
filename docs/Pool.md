# The Pool

The Pool provides you with permanent global storage space on Amazon S3, accessible across all
of your tiles and notebooks.

If you have access to the Pool, then it will appear in your sidebar.
Clicking on it brings up a tree-like image of your pool storage.

You can use the menus to add and delete things from your storage, rename things, etc.

Any files or folders that start with a "." are hidden in the pool view by default.
But there's a switch at the top that can make them visible.

## Accessing pool files from python

From notebooks and tiles, you can access pool files. One tricky thing is that S3 has some peculiarities.
In some ways it behaves like a normal filesystem,
but there are some differences. For example, in actuality, there is no such thing as an empty folder.

However, there is a python library called `s3fs` that provides a filesystem-like interface to S3.
This makes things pretty easy. To get started you do something like this:

```python
import s3fs
s3 = s3fs.S3FileSystem()
my_home = "s3://tactic-user-storage/users/bsherin"
with s3.open(f'{my_home}/myfile.txt', 'r') as f:
    contents = f.read()
```

In some cases, you don't have to do anything special at all. For example, if you read a pandas csv
with `pd.read_csv()`, you can just give it the path to your pool file, and it will read it in without any special handling.
This is because pandas uses s3fs under the hood when it sees a path that starts with "s3://".

Note that your paths will always start with "s3://tactic-user-storage/users/yourusername" and you can
only access files within that directory (though you can create subdirectories within it).

For convenience, you can also access the s3fs file system with `self.pool`. When you do that, you don't have to include 
the "s3://tactic-user-storage/users/yourusername" part of the path. So you can do something like this:

```python
with self.pool.open('myfile.txt', 'r') as f:
    contents = f.read()
```

There is also a tile option called {ref}`pool_select. <pool-select>` which allows
the user to select a file or folder from their pool.
