### Assignment
* Use a Jekyll "Static Site Generator" to start a local web server.
* soruce code is in the course repo under `bindmount-sample-1` (我放在src底下)
* edit files with editor on the host using native tools
* start container with `docker run -p 80:4000 -v $(pwd):/site bretfisher/jekyll-serve`