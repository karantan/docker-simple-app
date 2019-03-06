# convenience makefile

.PHONY: run
run:
	# "$(pwd)" in bash == "$(shell pwd)" in Makefile
	@docker run -it --rm -v "$(shell pwd)":/app -p 5000:5000 karantan/simple-web-app pipenv run flask run --host=0.0.0.0
