
latest = 2022.02.0-443
dockerhub = dockerhub.moffitt.org/hpc
imagename = rstudio-server


latest: $(latest)
	@echo Running docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	@echo Run make push to push the images to the server.

2022.02.0-443:
	docker compose -f rstudio-server-2022.02.0-443/docker-compose.yml build

v2021.09.2:
	docker compose -f rstudio-server-v2021.09.2/docker-compose.yml build

push:
	docker push $(dockerhub)/$(imagename):2022.02.0-443
	docker push $(dockerhub)/$(imagename):latest

