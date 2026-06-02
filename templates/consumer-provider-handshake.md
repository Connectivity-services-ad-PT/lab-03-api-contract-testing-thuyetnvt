# Consumer-Provider Handshake

## General Information

- Lab: FIT4110 Lab 03
- Date: 2026-06-02
- Provider team: AI Vision (B4)
- Consumer team: Camera Stream (B2)
- Provider service: ai-vision
- Consumer service: camera-stream

## Contract

- Contract file: `contracts/ai-vision.openapi.yaml`
- Mock base URL: `http://localhost:4010`
- Auth method: Bearer token via `Authorization: Bearer {{authToken}}`
- Tested endpoint: `POST /vision/detect`

## Smoke Test

### Request

```http
POST /vision/detect
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
  "cameraId": "CAM-B2-001",
  "correlationId": "corr-camera-smoke-0001",
  "capturedAt": "2026-05-19T03:30:00Z",
  "imageUrl": "https://storage.smart-campus.local/frames/cam-b2-001/smoke.jpg",
  "motionScore": 0.87,
  "priority": "high"
}
```

### Expected Response

```json
{
  "detectionId": "det-20260519-0001",
  "correlationId": "corr-20260519-0001",
  "status": "completed",
  "riskLevel": "high",
  "confidence": 0.94,
  "objects": []
}
```

## Result

- [x] Consumer can call provider mock successfully.
- [x] Consumer can parse required fields: `detectionId`, `riskLevel`, `confidence`.
- [x] Consumer understands provider 4xx/5xx errors through Problem Details.
- [x] Newman report or CLI log is available in `reports/`.

## Contract Change Notes

| Item | Before | After | Agreed by |
|---|---|---|---|
| Detect endpoint | Lab 3 sample used `/detect` | Lab 2 contract uses `/vision/detect` | Provider + Consumer |
| Request fields | Lab 3 sample used `camera_id`, `image_url` | Lab 2 contract uses `cameraId`, `correlationId`, `capturedAt`, `imageUrl`, `motionScore` | Provider + Consumer |
| Error response | Generic sample errors | `application/problem+json` from Lab 2 contract | Provider + Consumer |

## Sign-off

- Provider representative: AI Vision (B4) - agreed
- Consumer representative: Camera Stream (B2) - agreed
