# SG-VPN 10.1 — Wokku deployment

Node.js gateway package prepared for Wokku's Node.js buildpack.

## Deploy

1. Extract this ZIP.
2. Push the contents of this folder to a GitHub repository (the `package.json`, `server.js`, and `Procfile` must be at the repository root).
3. In Wokku, create an app and connect the repository, or deploy it using Wokku's Git remote workflow.
4. Use the Node.js buildpack / automatic Node.js detection. The start command is `npm start`.
5. Open the generated HTTPS app URL. Check `/health` (if enabled by the app) and `/api/status` for service status.

## Runtime

- Node.js 18 or newer
- Wokku provides `PORT`; the app binds to `0.0.0.0`.
- WebSocket connections are served on the same HTTP server (the app's documented `/direct` endpoint).
- Do not set a fixed port in Wokku.

## Important networking note

This app exposes its web interface and WebSocket upgrade through the HTTP app endpoint. Wokku's standard app URL is not automatically a public raw TCP/UDP port mapping. The gateway's outbound TCP/UDP behavior also depends on Wokku network egress policy and the target server. Test the actual VPN client/protocol after deployment; a healthy web page alone does not prove all tunnel traffic works.
