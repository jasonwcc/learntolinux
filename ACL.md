# Commands
- setfacl
- getfacl

## Create bunch of users and groups
	group1
	group2
	user1:group1
	user2:group2
	user3:group1
	user4:group2


## Copy acl 
	getfacl file-A | setfact --set-file=- file-B
	similar to chmod
	chmod --reference=directory2 directory
	chmod --reference=file2 file


## Recursive ACL Modifications
	setfacl -R -m u:user3:rx /test2

## Delete ACLs
	setfacl -x u:user2,g:group2 /test1/script1.sh

## Delete all ACLs
	setfacl -b /test1 # Remove all ACLs 


## Setting mask = maximum permissions
``` bash
	mkdir /test1
	echo "You able to exec $0" >> /test1/script1.sh

	setfacl -m u:user1:rwx /test1/script1.sh
	setfacl -m u:user3:rx /test1/script1.sh
	setfacl -m g:group2:rwx /test1/script1.sh
	
	getfacl /test1/script1.sh
getfacl: Removing leading '/' from absolute path names
`#- file: test1/script1.sh
- owner: root
- group: root
user::rw-
user:user1:rwx
user:user3:r-x
group::r--
group:group2:rwx
mask::rwx
other::r--

	NOTICE: 
	- mask default to rwx, hence everyone should be getting to whatever permission given to them
``` 
## Test
	su - user1
	/test1/script1.sh
	NOTE: 
	- should be successful

	setfacl -m m::r-- /test1/script1.sh
	getfacl /test1/script1.sh
getfacl: Removing leading '/' from absolute path names
# file: test1/script1.sh
# owner: root
# group: root
user::rw-
user:user1:rwx			#effective:r--
user:user3:r-x			#effective:r--
group::r--
group:group2:rwx		#effective:r--
mask::r--
other::r--

	NOTICE:
	- even though user1 has rwx, but effective permission can only read, same goes to group2 and 	user3

## Further Test
	su - user1
	/test1/script1.sh
	NOTE: 
	- should get permission denied
...


# Controlling Default ACL File Permissions
- Ensure file and directories create within a directory inherit the correct perrmission

- Test without setting default
```
	rm -r /test1; mkdir /test1

	setfacl -m u:user1:rwx  /test1
	setfacl -m g:group2:rwx  /test1


	touch /test1/file1; mkdir /test1/dir1
	getfacl -R /test1
getfacl: Removing leading '/' from absolute path names
# file: test1
# owner: root
# group: root
user::rwx
user:user1:rwx
group::r-x
group:group2:rwx
mask::rwx
other::r-x

# file: test1/file1
# owner: root
# group: root
user::rw-
group::r--
other::r--

# file: test1/dir1
# owner: root
# group: root
user::rwx
group::r-x
other::r-x
```
- Add default named user1 with read-only and execute permission on subdirectories
```
	setfacl -m d:u:user1:rwx /test1
	getfacl -R /test1
getfacl: Removing leading '/' from absolute path names
# file: test1
# owner: root
# group: root
user::rwx
user:user1:rwx
group::r-x
group:group2:rwx
mask::rwx
other::r-x
default:user::rwx
default:user:user1:rwx
default:group::r-x
default:mask::rwx
default:other::r-x
# newly added default entries

# file: test1/file1
# owner: root
# group: root
user::rw-
group::r--
other::r--

# file: test1/dir1
# owner: root
# group: root
user::rwx
group::r-x
other::r-x
```
- Test create new file & dir and see if acl is inherited
```
	touch /test1/file2
	mkdir /test1/dir2

	getfacl -R /test1/{file,dir}2
# file: test1/file2
# owner: root
# group: root
user::rw-
user:user1:rwx			#effective:rw-
group::r-x			#effective:r--
mask::rw-
other::r--

# file: test1/dir2
# owner: root
# group: root
user::rwx
user:user1:rwx
group::r-x
mask::rwx
other::r-x
default:user::rwx
default:user:user1:rwx
default:group::r-x
default:mask::rwx
default:other::r-x
``` 
- Now login as user1, attempt create files in subdir
	su - user1
	cd /test1/dir1/
	touch a
	Error: Permission denied

	cd /test1/dir2/
	touch a
	OK

- Remove default ACL entries
	setfacl -Rx d:u:user1 /test1





