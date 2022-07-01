
latest = 2.3
dockerhub = dockerhub.moffitt.org/hpc
imagename = majiq
MAJIQ_URL = `cat majiq_url.env`


latest: $(imagename)-$(latest)
	@echo Running docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	@echo Run make push to push the images to the server.

majiq-2.3: 
	docker compose build --build-arg MAJIQ_URL=$(MAJIQ_URL) $@

push: latest
	docker push $(dockerhub)/$(imagename):$(latest)
	docker push $(dockerhub)/$(imagename):latest
