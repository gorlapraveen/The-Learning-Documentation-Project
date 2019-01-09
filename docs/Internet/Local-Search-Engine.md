


## Searx

**Install `searx` in your local system and make `firefox` to use it through your localhost for browsing Internet**

Initially I followed basic installation as described in https://github.com/asciimoo/searx . It includes

## Installation

clone source: `git clone https://github.com/asciimoo/searx.git && cd searx`
install dependencies: `./manage.sh update_packages`
edit your settings.yml (set your secret_key!) ##Actuall no need, unless you host this as online for others user to access, you can give any arbitary key as described in https://github.com/asciimoo/searx/issues/1473 
run `python searx/webapp.py` to start the application

By Default searx is available at `localhost:8888` 
 1. Go to firefox
 2. Enter `localhost:8888` in the search bar
 3. `searx` search engine is available as shown below and you can search the web. 