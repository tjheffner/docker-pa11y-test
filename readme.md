# pa11y + results dashboard in docker

in your project root add the two containers in this repo to your project's relevant docker-compose.yml

the first service (pa11y) is what is actually running the tool and generating the results. this container should be run every time you want updated results (docker-compose run pa11y). it searches inside of ./tests/pa11y for a configuration file and checks against any defined urls.

the second service (dashboard) is a container that hosts a simple webpack-dev-server that eats the generated results (report.json). thanks to hot module reloading, this service doesn't need re-run every time, it will update the state with the new generated results after each pa11y run.

# quick start

edit .pa11yci with your desired rules & testing urls. at a minimum the urls array **must** be defined.

    docker-compose run pa11y
    docker-compose run dashboard

page has been updated with new elements, or .pa11yci has new defined urls to test:

    docker-compose run pa11y

the dashboard output will say it's available at 0.0.0.0:8080, but that is only inside of the docker container. and seeing as how that doesn't have a browser you can use, the link is _actually_ available at `www.pa11y.vm:8080/` by default. the port is necessary to see the dashboard.