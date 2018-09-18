# Shopify Theme Development
The release cycle would look like the following:  

1. Create **developerName** theme ID on your Shopify store  
2. Each developer downloads ThemeKit and updates environment settings to reflect the their theme ID  
3. Create pull request for new feature, bug fix, etc.  
4. Merge pull request into the master branch  
5. Deploy theme changes to your live store  

####Benefits:  
1. Teams can share progress and preview live work on Shopify servers  
2. Changes will never upload to the production store unless explicit `--env="production"` is added **AND** config.yml is setup with production theme-id  
3. Unlink Shopify Slate, wont require any additional tools to compile code since Shopify servers do all of the compiling.  

####Downside:  
1. Not true local development


# Breakdown:
## Create Developer Theme ID
Upload theme to shopify [ Dashboard->themes ]  
blankTheme.zip from Git repo is fine.  
Rename theme.  


## Developer Setup:
Make sure you have ThemeKit downloaded:  
https://shopify.github.io/themekit/  

Pull Git Repo
`git clone ...`  

### Configure Theme
Find the theme id of **your personal development theme** do not use [live] id  
`theme get --list`  
  
Rename config.yml.example to config.yml  
  
Update development section of config.yml with your theme id  
```
development:
  password: [password]
  theme_id: "[your-theme-id]"
  store: [store].myshopify.com
```

### Developing/Previewing
Preview changes on shopify
`theme open`

Automatic upload code changes:
`theme watch`

Manually upload code changes:
`theme deploy`

Create Pull Request for new feature, bug fix, etc



## Merging Into Live Theme
Pull master branch  

-----------------------
(if people still editing using Shopify.com instead of only via code):

Download all changes from Shopify live online:
`theme download`

Check if any changes to shopify online and update git master
```
git status
git commit -a -m ‘update git with changes to shopify website’
git push
```
-----------------------

Merge developers branch into master branch, fix conflicts, and push

Publish to shopify live store:
`theme deploy --env=”production”`



Example config.yml
```
development:
  password: [password]
  theme_id: "37624578121"
  store: [your-store].myshopify.com

production:
  password: [password]
  theme_id: "37626675273"
  store: [your-store].myshopify.com
```
