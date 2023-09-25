# Dev-ops-notes
## Docker

#### Docker caching
Using the `docker image history` command, you can see the command that was used to create each layer within an image.
  ```bash
  docker image history getting started
  ```
##### Layer caching
**Each comand** in the Dockerfile beacomes a new layer in the image.
Once a layer changes, all downstream layers have to be recreated as well, and this increases build times which is something we don't want.

Looking at the following Dockerfile used in the *getting-started* project, we see that whenever we make a change to the image, all the dependencies need to be installed. This is not very efficient ad doesn't make much sense to ship around the dependencies everytime we build.


To fix it, you need to restructure your Dockerfile to help support the caching of the dependencies. For Node-based applications, those dependencies are defined in the `package.json` file. You can copy only that file in first, install the dependencies, and then copy in everything else. Then, you only recreate the yarn dependencies if there was a change to the `package.json`.

1. Update the Dockerfile so that you first copy `package.json`, then install the dependencies and only after that copy everything else in the container:
  ```dockerfile
  # syntax=docker/dockerfile:1
  FROM node:18-alpine
  WORKDIR /app
  COPY package.json yarn.lock ./
  RUN yarn install --production
  COPY . .
  CMD ["node", "src/index.js"]
  ```
2. Create a file named `.dockerignore` in the same folder as the Dcokerfile with the following contents.
   ```node_moduls```
   this way we do not add the dependencies everytime

3. Build a new image using
   ```sh
   docker build -t getting-started .
   ```
4. Make a change somewhere in the file, for example in `src/static/index.html` and run `docker build -t getting-started .` again

5. You should notice that the build was much faster and that several steps are using previously cached layers. Now pushing, pulling, updates to the image will be much faster.
