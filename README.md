# CI/CD GCP Example

This is an example of an implementation of a simple CI/CD pipeline using Cloud Build in GCP. 

Simple actions are defined in the Makefile: 
```
build-local:
	docker build -f Dockerfile -t testwebserver .

run-local:
	docker run --name=testwebserver --restart unless-stopped -p 3000:3000 -d -t testwebserver

lint-local:
	docker container run testwebserver pylint --disable=R,C hello.py

test-local:
	docker container run testwebserver python -m pytest -vv test_hello.py

# Trigger cloudbuild: 
cloud-build:
	gcloud builds submit --config cloudbuild.yaml

```
