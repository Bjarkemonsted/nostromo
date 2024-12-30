# nostromo
Project for minor security tools for network admins



# nostromo project & onedrivesharepoint app setup

## Create virtual environment and install django

To get started, create a virtual environment. Make sure you have virtualenv installed

```sh
virtualenv --version
```

Install Django and create the basicss, including superuser. Dont be that guy, remember your superuserpassword ¯\_(ツ)_/¯.
Django 4.2 for LTS.


```sh
virtualenv nostromo -p python3
cd nostromo
source bin/activate
pip install Django==4.2
django-admin startproject nostromo .
cd nostromo
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

After the server runs, you can access the website and the admin panel.

Go to: [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

To log in to admin:

Go to: [http://127.0.0.1:8000/admin/](http://127.0.0.1:8000/admin/)

## Create Application onedrivesharepoint

```sh
django-admin startapp onedrivesharepoint
```

## onedrivesharepoint - Keep track of shared files/acces from onedrive and sharepoint.

Gather following information using Microsoft Graph API for the following details about OneDrive and SharePoint shared items.
- **Data to show from Microsoft Graph API:**

## Microsoft Graph API Data

Gather information about OneDrive and SharePoint shared items using Microsoft Graph API:

| Description             | Type      | MG API Name                  | Notes                          |
|-------------------------|-----------|-----------------------------|--------------------------------|
| Link                   | Text      | `webUrl`                     | Link to the shared item.       |
| Name (file/folder/etc) | Text      | `name`                       |                                |
| Shared by              | Text      | `owner`                      |                                |
| Shared with Names      | Text      | Derived from `sharedBy`      | Use directory lookup if needed.|
| Shared with Emails     | Email     | `grantedToIdentitiesV2`      | Extract emails.                |
| ShareStartDate         | DateTime  | `createdDateTime`            |                                |
| ShareEndDate (if any)  | DateTime  | `expirationDateTime`         |                                |


***other details for first go?***

All data should be available/saved in django admin, and there shall be a view the user showing details in a more fashionable way.

### To investigate
- How often do I update data?
- How long will data take to retrieve?
- How to make sure I only get changes since last query.


### For later...

- Revoke access for specific links/users
- Send a warning email to person who shared file if there is no expiry or other issues
- Show access, accessed and download details (could be quite query heavy!)
