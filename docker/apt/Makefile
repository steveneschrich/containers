latest = 2.11.4
dockerhub = dockerhub.moffitt.org/hpc
imagename = apt

latest: $(latest)
	@echo Running docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	@echo Run make push to push the images to the server.

2.11.4: 
	docker compose build $(imagename)-$@

push: latest
	docker push $(dockerhub)/$(imagename):$(latest)
	docker push $(dockerhub)/$(imagename):latest