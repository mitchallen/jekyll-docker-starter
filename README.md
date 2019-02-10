# jekyll-docker-starter

How to create, build and serve a jekyll site using docker.

## Usage

```
git clone https://github.com/mitchallen/jekyll-docker-starter.git
cd jekyll-docker-starter
```

### Remove root .gitignore

This starter project has a __.gitignore__ file to make sure
that my test folders don't get published with the repo.

```
rm .gitignore
```

* * *

## Docker Compose

### Step 1 - Create site

```
docker-compose -f docker-compose-manage.yml run blog-create
```

This will create two new folders:

* __blog-site/__
* __vendor/__

See also:

* __blog-site/\_posts__ - where you put new posts
* __blog-site/\_config.yml__ - site config (build after change)

### Step 2 - Serve site on localhost

```
docker-compose up 
```

Browse to: http://localhost:4000/

* * *

## Build

### Build after changing ./site/\_config.yml

```
docker-compose run blog jekyll build
```

### Generate a production build

```
JEKYLL_ENV=production docker-compose run blog jekyll build
```

* * *

### docker-compose cleanup

```
docker-compose down
```

### Start over

This step will remove previous attempts (if any):

__WARNING: THIS WILL DELETE ANY POSTS OR CONFIG CHANGES YOU MADE.__

```
rm -rf blog-site && rm -rf vendor
```

After running this step, you will need to recreate the site.

* * *

## Kubernetes / docker stack alternative

This part is for advanced users who have kubernetes installed.

You still need to run the step above to create a site locally

## docker stack serve

```
docker stack deploy -c docker-compose.yml blogstack
```

May default to kubernetes if installed, if not:

```
docker stack deploy --orchestrator=kubernetes -c docker-compose.yml blogstack
```

### Additional commands

```
kubectl get all
kubectl get pods
docker stack ls
```

## Viewing the logs

```
kubectl get pods
kubectl logs (pod-id)
kubectl logs -f (pod-id) ## tail log
```

## Docker Stack Cleanup

```
docker stack rm blogstack
```

* * *

## References

* https://jekyllrb.com/docs/usage/
