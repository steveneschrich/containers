
latest = 4.1
dockerhub = dockerhub.moffitt.org/hpc
imagename = r


latest: $(latest)
	@echo Running docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	@echo Run make push to push the images to the server.

4.1:
	docker compose -f r-4.1/docker-compose.yml build
push:
	docker push $(dockerhub)/$(imagename):4.1
	docker push $(dockerhub)/$(imagename):latest
