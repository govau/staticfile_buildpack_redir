# Staticfile buildpack redir

A cloud foundry app to redirect all requests to another hostname.

## Example

We had a site deployed at https://dta.apps.staging.digital.gov.au, and it
is now being deployed at https://dta-website.apps.y.cld.gov.au.

For this simple example, we deploy to a cloud foundry with
`apps.staging.digital.gov.au` as the default shared domain.

```
$ Set our app name of the site to redirect from
APP_NAME=dta

# Login to cf if necessary and target the correct org and spacae
cf login -a https://api.system.staging.digital.gov.au

# push the redir app, but dont start it
cf push ${APP_NAME} --no-start

# Set where to redirect to
cf set-env ${APP_NAME} REDIRECT_TO "dta-website.apps.y.cld.gov.au"

# Start the app
cf start ${APP_NAME}

# test the redirect
curl -I https://dta.apps.staging.digital.gov.au/foo

# Response should redirect to https://dta-website.apps.y.cld.gov.au/foo

```
