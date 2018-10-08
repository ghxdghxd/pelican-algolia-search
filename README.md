# 配置文件

1. 添加ALGOLIA_APP_ID，ALGOLIA_SEARCH_API_KEY，ALGOLIA_ADMIN_API_KEY，ALGOLIA_INDEX_NAME到 .env 文件
2. 添加以下代码到pelicanconf.py

```python
# algolia search config
import os
ENV = os.path.join(os.environ['HOME'], ".env")

if os.path.exists(ENV):
    print('Importing environment from ', ENV)
for line in open(ENV):
    var = line.strip().split('=')
    if len(var) == 2:
        key, value = var[0].strip(), var[1].strip()
        os.environ[key] = value
ALGOLIA_APP_ID = os.getenv('ALGOLIA_APP_ID', None)
ALGOLIA_SEARCH_API_KEY = os.getenv('ALGOLIA_SEARCH_API_KEY', None)
ALGOLIA_ADMIN_API_KEY = os.getenv('ALGOLIA_ADMIN_API_KEY', None)
ALGOLIA_INDEX_NAME = os.getenv('ALGOLIA_INDEX_NAME', None)
```

# Algolia Search integration for Pelican

This [Pelican](http://docs.getpelican.com) plugin automatically indexes your posts with the  [Algolia](https://www.algolia.com) cloud service.

You can find a live example [here](https://tested-for-you.surge.sh/).

Each time you rebuild your site the plugin will update the indexes on the Algolia servers and remove any deleted documents.

## Installation & Configuration

**Create a free account with Algolia:**

> You do not need a credit card to create an account and it will be enabled immediately.

**Clone this repository and add it to your plugin folder:**

```bash
cd plugins
git clone https://github.com/srault95/pelican-algolia-search.git
```

**Install requirements:**

```bash
pip install algoliasearch beautifulsoup4
```

**Enable & configure the plugin in your pelicanconf.py:**

```python
PLUGINS = [
    #...
    'algolia_search'
]

ALGOLIA_APP_ID = "[YOUR ALGOLIA APPID]"
ALGOLIA_SEARCH_API_KEY = "[YOUR ALGOLIA SEARCH API KEY]"
ALGOLIA_ADMIN_API_KEY = "[YOUR ALGOLIA ADMIN API KEY]"
ALGOLIA_INDEX_NAME = 'demoblog'
```

**Build you own search page:**

There are many ways to integrate the Algolia search widgets in your website. I chose to use [vue-instantsearch](https://community.algolia.com/vue-instantsearch).

I completely replaced the `index.html` template to put the search box on the index page. ([index.html](https://github.com/srault95/tested-for-you/blob/master/pelican/themes/alchemy/templates/index.html))

The [Algolia documentation](https://www.algolia.com/doc/tutorials/search-ui/instant-search/build-an-instant-search-results-page/instantsearchjs/)
 has all the necessary information and examples to get started.

**Rebuild your website:**

```bash
pelican
```
