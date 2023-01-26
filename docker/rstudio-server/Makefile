latest = 2022.12.0-353
dockerhub = dockerhub.moffitt.org/hpc
imagename = rstudio-server


latest: $(latest)
	@echo Running docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	@echo Run make push to push the images to the server.

2022.12.0-353:
	docker compose build $(imagename)-$@

2022.07.2-576:
	docker compose build $(imagename)-$@

2022.07.1-554:
	docker compose build $(imagename)-$@

2022.02.3-492:
	docker compose build $(imagename)-$@

2022.02.2-485:
	docker compose build $(imagename)-$@

2022.02.0-443:
	docker compose build $(imagename)-$@

v2021.09.2:
	docker compose build $(imagename)-$@

push: latest
	docker push $(dockerhub)/$(imagename):$(latest)
	docker push $(dockerhub)/$(imagename):latest

