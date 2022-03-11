
latest = 2.0.3.1
dockerhub = dockerhub.moffitt.org/hpc
imagename = maxquant


latest: $(latest)
	@echo Running docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	@echo Run make push to push the images to the server.

2.0.3.1:
	docker compose -f maxquant-2.0.3.1/docker-compose.yml build

1.6.2.10:
	docker compose -f maxquant-1.6.2.10/docker-compose.yml build

push:
	docker push $(dockerhub)/$(imagename):1.6.2.10
	docker push $(dockerhub)/$(imagename):2.0.3.1
	docker push $(dockerhub)/$(imagename):latest

