Sometimes you may want to create temporary file or directories for the life
of the process and then you want them deleted once the process terminates or
the file is closed. This
is very useful to store some metadata or temporary data but you don't want the
data to persist in the filesystem. We can achieve that by creating temporary
file which is available in almost all languages such as Python and C. The way
temporary file works is as follows:

- Creates a file with random name 
- Make the file mode "wb+" which means create it for reading/writing and
  truncate if it exists
- Unlink the file right after creation. This will guarantee that the file will
  be deleted after the process terminates
- Return the file object to the caller

Once we close the file or all the process(es) that has a reference to the file
terminates, the file will be removed. The same thing applies to temporary
directories.

Example in Python:
```python
import tempfile

# Create temp file 
fp = tempfile.TemporaryFile()

# Write to the file
fp.write("First write!")

# Read from the beginning
fp.seek(0)
fp.read()   #=> "First write!"

# Now the file will be closed and removed
fp.close()
```
