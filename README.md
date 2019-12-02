# Description

This sample demonstrates:

- Logging in to Auth0 using Redirect Mode
- Accessing profile information that has been provided in the ID token
- Gated content. The `/profile` route is not accessible without having first logged in
- Call external APIs secured with users access_token
- As API call the online REST API testing tool httpbin.org is used

## Project setup

```bash
npm install
```

### Compiles and hot-reloads for development

```bash
npm run serve
```

## Deployment

### Compiles and minifies for production

```bash
npm run build
```

### Docker build

To build and run the Docker image, run `exec.sh`

### Run your tests

```bash
npm run test
```

### Lints and fixes files

```bash
npm run lint
```

## Hosting

This app is hosted on https://pizza42.oauth.ninja

## Based on
- https://github.com/auth0-samples/auth0-vue-samples

## License

This project is licensed under the MIT license. See the [LICENSE](./LICENSE) file for more info.
