# convenience makefile

.PHONY: run
run:
	@docker run -it --rm -v "$(pwd)":/app -p 5000:5000 karantan/simple-web-app pipenv run flask run --host=0.0.0.0
