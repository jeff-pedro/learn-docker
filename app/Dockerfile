# syntax=docker/dockerfile:1

ARG NODE_VERSION=18.0.0

FROM node:${NODE_VERSION}-alpine as base
WORKDIR /app
EXPOSE 3000
ENV YARN_CACHE_FOLDER=/root/.yarn

FROM base as dev
RUN --mount=type=bind,source=package.json,target=package.json \
    --mount=type=bind,source=package-lock.json,target=package-lock.json \
    --mount=type=cache,target=/root/.yarn \
    yarn install --frozen-lockfile
USER node
COPY . .
CMD [ "yarn", "run", "dev" ]


FROM base as prod
RUN --mount=type=bind,source=package.json,target=package.json \
    --mount=type=bind,source=package-lock.json,target=package-lock.json \
    --mount=type=cache,target=/root/.yarn \
    yarn install --prod --frozen-lockfile
USER node
COPY . .
CMD [ "node", "/src/index.js" ]


FROM base as test
ENV NODE_ENV test
RUN --mount=type=bind,source=package.json,target=package.json \
    --mount=type=bind,source=package-lock.json,target=package-lock.json \
    --mount=type=cache,target=/root/.yarn \
    yarn install --frozen-lockfile
USER node   
COPY . .
# Run test
USER root
RUN yarn run test
# Create image with node user
USER node
