# simple_drive
Use Google Drive API in the simplest way

## Installation
### Install from GitHub
```shell
pip install --upgrade git+https://github.com/tranngocminhhieu/simple-drive.git
```
### Install from PyPI
```shell
pip install --upgrade simple-drive
```

## Usage
### Import
```python
from simple_drive import Drive, Auth, MimeTypes, Roles
```

### Create auth info
#### From a service account
Read more: [How to create a Service Account](https://lucidgen.com/en/create-service-account-and-enable-google-cloud-api/)
```python
# Way 1
auth = Auth.from_service_account_file(file=YOUR_SERVICE_ACCOUNT_FILE)
# Way 2
auth = Auth.from_service_account_info(info=YOUR_SERVICE_ACCOUNT_INFO)
```
#### From local web server
```python
auth = Auth.local_web_server(client_secrets_file=YOUR_CLIENT_SECRETS_FILE)
```

### Use Drive API
```python
drive = Drive(auth_info=auth)
```

#### Create a file or folder
```python
# mime_type = MimeTypes.FOLDER
# mime_type = MimeTypes.SHEETS
# ...
drive.create(name, mime_type, dest_folder_id=None)
```

#### Delete a file or folder
```python
drive.delete(file_id)
```

#### Move a file or folder
```python
drive.move(file_id, dest_folder_id)
```

#### Upload a file
```python
drive.upload(file, dest_folder_id=None, rename=None)
```

#### Copy a file
Not support folder yet.
```python
drive.copy(file_id, name_prefix='Copy of ', name_suffix='', dest_folder_id=None)
```

#### Rename a file or folder
```python
drive.rename(file_id, name)
```

#### Get a file or folder info
```python
drive.get_file_info(file_id, fields='*')
```

#### List files related to this account
```python
drive.list_files(title_contains=None, owner_email=None, folder_id=None, custom_filter=None)
```

#### Get the account storage quota
```python
drive.storage_quota()
```

#### Get permission of a file or folder
```python
drive.get_permission_info(file_id)
```

#### Add permission to a file or folder
```python
# role = Roles.VIEWER
# role = Roles.EDITOR
# role = Roles.COMMENTER
drive.add_permission(file_id, email, role)
```

#### Remove a permission from a file or folder
Please provide either `email` or `permission_id`.
```python
drive.remove_permission(file_id, email=None, permission_id=None)
```

#### Transfer ownership of a file or folder to an email
Support emails in organization.
```python
drive.transfer_ownership(file_id, email)
```