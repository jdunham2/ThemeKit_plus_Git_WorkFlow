# Release cycle for teams using Shopify themeKit/Git
The release cycle would look like the following:  

1. Create **developerName** theme ID on your Shopify store  
2. Each developer downloads ThemeKit and updates environment settings to reflect the their theme ID  
3. Create pull request for new feature, bug fix, etc.  
4. Merge pull request into the master branch  
5. Deploy theme changes to your live store  

#### Benefits:  
1. Teams can preview work and share progress on Shopify servers
2. Changes will never upload to the production store unless explicit `--env="production"` is added **AND** config.yml is setup with production theme-id  
3. Unlike Shopify Slate, doesn't require any additional tools or configuration to compile code
4. Shopify servers do all of the compiling.

#### Downside:  
1. Not true local development


# Breakdown:
## Download ThemeKit
https://shopify.github.io/themekit/#installation

## Setup API access
https://shopify.github.io/themekit/#get-api-access

## Create Developer Theme ID
Upload blank theme to shopify [ Dashboard->themes ]  
Rename theme to **developerName**  


## Clone Production Site from Git
Pull Git Repo
`git clone ...`  

### Configure Theme
Copy config.yml.example to config.yml

Find the theme id of **your personal development theme** do not use [live] id  
`theme get --list`  
  
Update development section of config.yml with your theme id  
```
development:
  password: [password]
  theme_id: "[your-theme-id]"
  store: [store].myshopify.com
```

### Developing and Previewing
Automatic upload code changes:
`theme watch`  
or  
Manually upload code changes:
`theme deploy`  

Preview changes on shopify
`theme open`

#### Create Pull Request for new feature, bug fix, etc



## Merging Into Live Theme
1. Pull master branch  
  * #### Additional WF if still editing using Shopify.com instead of only via code:
  * Download all changes from Shopify live online:
  * `theme download --env='production'`
  * Check if any changes to shopify online and update git master
2. Merge developers branch into master branch, fix conflicts, and push
3. Publish to shopify live store:
`theme deploy --env='production'`



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
