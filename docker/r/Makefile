
latest = 4.2.2
dockerhub = dockerhub.moffitt.org/hpc
imagename = r


latest: $(imagename)-$(latest)
	@echo Running docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	docker tag $(dockerhub)/$(imagename):$(latest) $(dockerhub)/$(imagename):latest
	@echo Run make push to push the images to the server.

r-4.1:
	docker compose build  $@

r-4.2.1:
	docker compose build $@

r-4.2.2:
	docker compose build $@

push: latest
	docker push $(dockerhub)/$(imagename):$(latest)
	docker push $(dockerhub)/$(imagename):latest
