# packtpub-crawler

### Download FREE eBook every day from [www.packtpub.com](https://www.packtpub.com/packt/offers/free-learning)

This crawler automates the following step:

* grab the hidden form parameters
* access to private account
* claim the daily free eBook
* parse title, description and useful information
* download favorite format *.pdf .epub .mobi*
* download source code and book cover
* upload files to Google Drive
* notify via email

#### Default command
```bash
# upload pdf to drive and notify via email
python script/spider.py -c config/prod.cfg -u drive -n
```

#### Other options
```bash
# download all format
python script/spider.py --config config/prod.cfg --all

# download only one format: pdf|epub|mobi
python script/spider.py --config config/prod.cfg --type pdf

# download also additional material: source code (if exists) and book cover
python script/spider.py --config config/prod.cfg -t pdf --extras
# equivalent (default is pdf)
python script/spider.py -c config/prod.cfg -e

# download and then upload to Drive (given the download url anyone can download it)
python script/spider.py -c config/prod.cfg -t epub --upload drive
python script/spider.py --config config/prod.cfg --all --extras --upload drive
```

#### Configuration
You need to create `config/prod.cfg` file with your Packt Publishing credential, look at `config/prod_example.cfg` for a [sample](https://github.com/niqdev/packtpub-crawler/blob/master/config/prod_example.cfg).

From documentation, Drive API requires OAuth2.0 for authentication, so to upload files you should:

* Go to [APIs Console](https://code.google.com/apis/console) and make a new project named **PacktpubDrive**
* On *Services* menu, turn Drive API on
* On *API Access* menu, create OAuth client ID
  * Application type: Installed application
  * Installed application type: Other
* Click *Download JSON* and save the file `config/client_secrets.json`.
* Documentation: [OAuth](https://developers.google.com/api-client-library/python/guide/aaa_oauth), [Quickstart](https://developers.google.com/drive/v3/web/quickstart/python), [example](https://github.com/googledrive/python-quickstart) and [permissions](https://developers.google.com/drive/v2/reference/permissions)

If you want to *send* a notification via email using Gmail you have to [allow "less secure apps"](https://www.google.com/settings/security/lesssecureapps) on your account.

#### Development (only for spidering)
Run a simple static server with
```
node dev/server.js
```
and test the crawler with
```
python script/spider.py --dev --config config/dev.cfg --all
```

#### Possible improvements
* compress files before upload
* add uploading service for [Dropbox](https://www.dropbox.com/developers/core/start/python)
* log to file and console: [example](http://stackoverflow.com/questions/4675728/redirect-stdout-to-a-file-in-python)
* cron
