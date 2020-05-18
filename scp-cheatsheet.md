## scp commands

Basic Syntax

```
$ scp source_file_path destination_file_path
```
Parameters

```diff
-r      # transfer directory 
-v      # see the transfer details
-C      # copy files with compression
-l 800  # limit bandwith with 800
-p      # preserving the original attributes of the copied files
-q      # hidden the output
```

### Uploading

Single file
```
$ scp ~/my_local_file.txt user@remote_host.com:/some/remote/directory
```

Multiple files
```
$ scp foo.txt bar.txt username@remotehost:/path/directory/
```

### Downloading

Single file
```
$ scp user@remote_host.com:/some/remote/directory ~/my_local_file.txt
```

Multiple files
```
$ scp username@remotehost:/path/directory/\{foo.txt,bar.txt\} .
```


### Extra Options

#### Verbose Output

```
$ scp -v source_file_path destination_file_path
```

#### Copy Entire Directory (Recursively)

```
$ scp -r source_file_path destination_file_path
```

#### Speed Up Transfer with Compression

```
$ scp -C source_file_path destination_file_path
```

#### Specify Identity File

```
$ scp -i private_key.pem ~/test.txt root@192.168.1.3:/some/path/test.txt
```
