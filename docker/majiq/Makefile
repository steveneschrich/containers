
latest = 2.3
dockerhub = dockerhub.moffitt.org/hpc
imagename = majiq


latest: $(latest)
	@echo Running docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	@echo Run make push to push the images to the server.

2.3:
	docker compose -f majiq-2.3/docker-compose.yml build
push:
	docker push $(dockerhub)/$(imagename):2.3
	docker push $(dockerhub)/$(imagename):latest
