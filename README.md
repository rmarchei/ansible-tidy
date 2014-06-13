ansible-tidy
============

Tidy module for Ansible, inspired by Puppet's tidy module. Remove unwanted files based on specific criteria.  
Multiple criteria are AND’d together

New in version: 1.7

<table>
<tr>
<th class="head">parameter</th>
<th class="head">required</th>
<th class="head">default</th>
<th class="head">choices</th>
<th class="head">comments</th>
</tr>
<tr>
<td>age</td>
<td>no</td>
<td>0</td>
<td><ul></ul></td>
<td>Tidy files whose age is equal to or greater than the specified time.  
You can choose seconds, minutes, hours, days, or weeks by specifying the first letter of any of those words (e.g., ‘1w’). Specifying 0 will remove all files.</td>
</tr>
<tr>
<td>force</td>
<td>no</td>
<td></td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>Force removal of non empty directories</td>
</tr>
<tr>
<td>matches</td>
<td>no</td>
<td></td>
<td><ul></ul></td>
<td>One or more (shell type) file glob patterns, which restrict the list of files to be tidied to those whose basenames match at least one of the patterns specified.  
Multiple patterns can be specified using a list.</td>
</tr>
<tr>
<td>path</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>Path to the file or directory to manage. Must be fully qualified.</td>
</tr>
<tr>
<td>recurse</td>
<td>no</td>
<td>no</td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>If target is a directory, recursively descend into the directory looking for files to tidy.</td>
</tr>
<tr>
<td>rmdirs</td>
<td>no</td>
<td>no</td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>Tidy directories in addition to files; that is, remove directories whose age is older than the specified criteria.  This will only remove empty directories, so all contained files must also be tidied before a directory gets removed.</td>
</tr>
<tr>
<td>silent</td>
<td>no</td>
<td>no</td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>Silently ignore failed commands.</td>
</tr>
<tr>
<td>size</td>
<td>no</td>
<td>0</td>
<td><ul></ul></td>
<td>Tidy files whose size is equal to or greater than the specified size.  
Unqualified values are in bytes, but b, k, m, g, and t can be appended to specify bytes, kilobytes, megabytes, gigabytes, and terabytes, respectively.  
Size is not evaluated for directories.</td>
</tr>
<tr>
<td>timestamp</td>
<td>no</td>
<td>atime</td>
<td><ul><li>atime</li><li>mtime</li><li>ctime</li></ul></td>
<td>Set the mechanism for determining age. Default is atime.</td>
</tr>
</table>  


* Examples:

```
# Recursively delete on /tmp files older than 4 weeks
- tidy: path="/tmp" age="4w" recurse=yes

# Recursively delete on /tmp files older than 4 weeks and equal or greater than 1 megabyte
- tidy: path="/tmp" age="4w" size="1m" recurse=yes

# Recursively delete on /var/tmp files and empty directories with last access time greater than 3600 seconds
- tidy: path="/var/tmp" age="3600" timestamp=atime rmdirs=yes recurse=yes

# Delete on /var/log files equal or greater than 10 megabytes ending with .log or .log.gz
- tidy: path="/var/tmp" matches="*.log","*.log.gz" size="10m"
```


