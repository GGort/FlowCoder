# Dockerfile
FROM node:21-bookworm as base


# Change our current working directory
WORKDIR /usr/src/app

# Copy over `package.json` and lock files to optimize the build process
# Yarn V3
RUN corepack enable && yarn set version berry

COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "yarn.lock", "./"]
RUN yarn && yarn install

# Copy over rest of the project files
COPY . .

# Expose port 3000 for the SvelteKit app and 24678 for Vite's HMR
EXPOSE 3000

FROM base as dev
EXPOSE 24678
# Set the Node environment to development to ensure all packages are installed
ENV NODE_ENV development

# Run `yarn dev` and set the host to 0.0.0.0 so we can access the web app from outside
CMD ["yarn", "dev", "--host", "--port", "3000"]

FROM base as prod
RUN yarn build
