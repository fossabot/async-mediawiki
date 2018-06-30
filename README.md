# async-mediawiki
An asynchronous python libary to get mediawiki content

# Installation

It requires Python 3.5 or above and aiohttp

`pip3 install async-mediawiki`

# Usage
```python

import async_mediawiki as mediawiki
w = mediawiki.MediaWiki("https://en.wikipedia.org/w/api.php")
html = await w.get_html("Chemistry") #page html when rendered 
md = await w.get_markdown("Chemistry") #markdown, what you see when editing a page
text = await w.get_text("Chemistry") #pure text without html and markdown
await w.close() #close the session


#login to the wiki to make changes under a specific user
await w.login("username", "password")

#create an account
await w.create_account("username", "password", userEmail="email (optional)", userRealName="real name (optional)") 

#to edit a page or create it if it doesn't exist
await w.edit_page("Page Title", "My content", token="my edit token")
#edit token is anonymous when not specified, otherwise auto-generated as the logged in user if not given an explicit one

#you can also use this
w = mediawiki.MediaWiki()
print(await w.get_markdown("https://wiki.guildwars.com/api.php?action=query&titles=Ranger&prop=revisions&rvprop=content&format=json&formatversion=2"))
#the libary handles the URLs automatically when provided a base URL to the API

```
