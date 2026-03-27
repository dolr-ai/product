## Overview

V3 API for direct video uploads to Storj storage. Videos are immediately available after upload and asynchronously synced to IC canisters.

**Base URL**: `https://yral-upload-video.go-bazzinga.workers.dev`

---

## Endpoints

### 1. Get Upload URL

**Endpoint**: `POST /get_upload_url_v3`

**Description**: Returns a pre-signed upload URL for direct video upload to Storj storage.

**Request Body**:
```json
{
  "publisher_user_id": "7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe"
}
```

**Parameters**:
- `publisher_user_id` (required, string): Internet Computer principal of the publisher

**Response**:
```json
{
  "success": true,
  "message": null,
  "data": {
    "uid": "495873ac7b174011b3f9dffaec9c24ef",
    "upload_url": "https://storj-interface.yral.com/duplicate_raw/upload?publisher_user_id=7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe&video_id=495873ac7b174011b3f9dffaec9c24ef&is_nsfw=false",
    "scheduled_deletion": null,
    "watermark": null
  }
}
```

**Response Fields**:
- `uid` (string): Unique video identifier (32-char hex, CF Streams compatible)
- `upload_url` (string): Pre-signed URL for uploading video binary
- `scheduled_deletion` (null): Always null for Storj uploads
- `watermark` (null): Always null for Storj uploads

---

### 2. Update Video Metadata

**Endpoint**: `POST /update_metadata_v2`

**Description**: Finalizes the video upload by adding metadata. Triggers asynchronous upload to IC canister.

**Request Body**:
```json
{
  "video_uid": "495873ac7b174011b3f9dffaec9c24ef",
  "delegated_identity_wire": {
    "pubkey": [/* Uint8Array */],
    "inner_der": [/* Uint8Array */],
    "expires_at": 1700000000000000000
  },
  "meta": {
    "description": "My awesome video",
    "title": "Awesome Video",
    "tags": "awesome,video,yral"
  },
  "post_details": {
    "video_uid": "495873ac7b174011b3f9dffaec9c24ef",
    "description": "My awesome video",
    "is_nsfw": false,
    "creator_consent_for_inclusion_in_hot_or_not": true,
    "hashtags": ["awesome", "video", "yral"]
  }
}
```

**Parameters**:
- `video_uid` (required, string): Video UID from `/get_upload_url_v3`
- `delegated_identity_wire` (required, object): IC delegated identity
  - `pubkey` (Uint8Array): Public key bytes
  - `inner_der` (Uint8Array): DER-encoded delegation chain
  - `expires_at` (number): Expiration timestamp in nanoseconds
- `meta` (optional, object): Custom metadata
  - `description` (string): Video description
  - `title` (string): Video title
  - `tags` (string): Comma-separated tags
- `post_details` (required, object): Video post details
  - `video_uid` (string): Must match the video_uid parameter
  - `description` (string): Video description
  - `is_nsfw` (boolean): NSFW flag (default: false)
  - `creator_consent_for_inclusion_in_hot_or_not` (boolean): Consent flag
  - `hashtags` (array): Array of hashtag strings

**Response**:
```json
{
  "success": true,
  "message": null,
  "data": null
}
```

**What Gets Stored Where**:
- **Storj metadata**: `description`, `title`, `tags`, `post-details` (~318 bytes)
  - `delegated-identity` is excluded to avoid command-line size limitations
- **Queue message**: Full `delegated-identity` + `post-details` for IC canister upload

**Side Effects**:
1. Finalizes video upload to Storj with metadata
2. Enqueues message for asynchronous IC canister upload
3. Emits video upload events
4. Marks post as published on IC

---

## Complete Upload Flow

### Step 1: Get Upload URL
```bash
curl -X POST https://yral-upload-video.go-bazzinga.workers.dev/get_upload_url_v3 \
  -H "Content-Type: application/json" \
  -d '{
    "publisher_user_id": "7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe"
  }'
```

**Returns**: `uid` and `upload_url`

---

### Step 2: Upload Video Binary
```bash
curl -X POST "{upload_url}" \
  -H "Content-Type: video/mp4" \
  --data-binary @video.mp4
```

**Note**: Use the exact `upload_url` returned from Step 1

---

### Step 3: Finalize with Metadata
```bash
curl -X POST https://yral-upload-video.go-bazzinga.workers.dev/update_metadata_v2 \
  -H "Content-Type: application/json" \
  -d '{
    "video_uid": "495873ac7b174011b3f9dffaec9c24ef",
    "delegated_identity_wire": {
      "pubkey": [/* Uint8Array */],
      "inner_der": [/* Uint8Array */],
      "expires_at": 1700000000000000000
    },
    "meta": {
      "description": "My video description",
      "title": "My Video Title",
      "tags": "tag1,tag2,tag3"
    },
    "post_details": {
      "video_uid": "495873ac7b174011b3f9dffaec9c24ef",
      "description": "My video description",
      "is_nsfw": false,
      "creator_consent_for_inclusion_in_hot_or_not": true,
      "hashtags": ["tag1", "tag2", "tag3"]
    }
  }'
```

**Result**: Video is immediately available on Storj and queued for IC upload

---

## Error Responses

```json
{
  "success": false,
  "message": "Error description",
  "data": null
}
```

**HTTP Status Codes**:
- `200 OK`: Request processed (check `success` field)
- `400 Bad Request`: Invalid request or operation failed

---

## Video ID Format

32-character hex string (UUID v4 simple format):
```
495873ac7b174011b3f9dffaec9c24ef
```

---

## Asynchronous Processing

After calling `/update_metadata_v2`, the following happens asynchronously:

1. **Queue Message Created**: `UploadVideoStorj` message with `delegated_identity_json` and `post_details_json`
2. **Queue Handler**: Reconstructs metadata and uploads to IC canister
3. **Events Emitted**: Video upload events sent to EventService
4. **Post Published**: Post marked as published on IC

**Timeline**: IC canister upload typically completes within seconds

---

## Metadata Size Limits

**Storj metadata**: Recommended max ~500 bytes
- Large metadata (>1000 bytes) can cause `uplink` command failures
- `delegated-identity` (~1700 bytes) is intentionally excluded from Storj metadata

**Queue metadata**: No size limits (uses individual JSON string fields)

---

## Key Differences from V1/V2

| Feature | V1/V2 (CF Streams) | V3 (Storj Direct) |
|---------|-------------------|-------------------|
| Upload method | GET endpoint | POST endpoint |
| Video availability | After CF processing (~60s) | Immediate |
| Publisher ID | Not required | Required upfront |
| Storage | CF Streams → Storj | Direct to Storj |
| Webhooks | Required | Not needed |
| Cost | CF Streams + Storj | Storj only |

---

## Video Playback & Consumption

### Getting Video URLs

Videos uploaded via V3 are stored on Storj and can be accessed directly via Storj LinkShare CDN URLs.

**Video URL Format**:
```
https://link.storjshare.io/raw/{access_grant}/{bucket}/{publisher_user_id}/{video_id}.mp4
```

**SFW Videos**:
```
https://link.storjshare.io/raw/jx6vm3ebgb4gt3gfkmcrw62bl7rq/yral-videos/{publisher_user_id}/{video_id}.mp4
```

**NSFW Videos**:
```
https://link.storjshare.io/raw/jwait7tp3civp6cbaot4zzjbheqq/yral-nsfw-videos/{publisher_user_id}/{video_id}.mp4
```

**Parameters**:
- `publisher_user_id`: The IC principal of the video publisher
- `video_id`: The 32-char hex video ID returned from `/get_upload_url_v3`

**Example URLs**:
```
# SFW Video
https://link.storjshare.io/raw/jx6vm3ebgb4gt3gfkmcrw62bl7rq/yral-videos/7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe/495873ac7b174011b3f9dffaec9c24ef.mp4

# NSFW Video
https://link.storjshare.io/raw/jwait7tp3civp6cbaot4zzjbheqq/yral-nsfw-videos/7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe/495873ac7b174011b3f9dffaec9c24ef.mp4
```

### Playing Videos

**Direct Playback (SFW)**:
```html
<video controls>
  <source src="https://link.storjshare.io/raw/jx6vm3ebgb4gt3gfkmcrw62bl7rq/yral-videos/7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe/495873ac7b174011b3f9dffaec9c24ef.mp4" type="video/mp4">
</video>
```

**JavaScript**:
```javascript
// Build video URL based on NSFW status
const STORJ_SFW_BASE = "https://link.storjshare.io/raw/jx6vm3ebgb4gt3gfkmcrw62bl7rq/yral-videos";
const STORJ_NSFW_BASE = "https://link.storjshare.io/raw/jwait7tp3civp6cbaot4zzjbheqq/yral-nsfw-videos";

const baseUrl = isNsfw ? STORJ_NSFW_BASE : STORJ_SFW_BASE;
const videoUrl = `${baseUrl}/${publisherUserId}/${videoId}.mp4`;

const videoElement = document.createElement('video');
videoElement.src = videoUrl;
videoElement.controls = true;
document.body.appendChild(videoElement);
```

**cURL Download**:
```bash
# Download SFW video
curl "https://link.storjshare.io/raw/jx6vm3ebgb4gt3gfkmcrw62bl7rq/yral-videos/7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe/495873ac7b174011b3f9dffaec9c24ef.mp4" \
  -o video.mp4
```

### Video Storage Buckets

Videos are stored in different Storj buckets based on NSFW status:

- **SFW Videos**: `yral-videos` bucket
- **NSFW Videos**: `yral-nsfw-videos` bucket

**Storj Path Format**:
```
sj://{bucket}/{publisher_user_id}/{video_id}.mp4
```

**Examples**:
```
sj://yral-videos/7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe/495873ac7b174011b3f9dffaec9c24ef.mp4
sj://yral-nsfw-videos/7lb6r-7touy-3rnnc-tihkp-aq33u-kfvwl-hb7ir-ugaie-ngani-xlxdp-6qe/495873ac7b174011b3f9dffaec9c24ef.mp4
```

### Video Availability

- **Immediate**: Videos are available for playback immediately after Step 2 (binary upload) completes
- **No waiting**: Unlike CF Streams, no processing delay or webhook polling required
- **Direct streaming**: Videos can be streamed directly from Storj interface
- **Global CDN**: Storj provides distributed access globally

### Best Practices for Clients

1. **Construct URLs dynamically**: Build download URLs using `publisher_user_id`, `video_id`, and `is_nsfw` flag
2. **Cache video metadata**: Store video IDs and publisher IDs from IC canister queries
3. **Handle NSFW properly**: Respect the `is_nsfw` flag when constructing URLs
4. **Use video tags**: HTML5 `<video>` tag supports direct Storj URLs with streaming
5. **Progressive download**: Videos support range requests for seeking/progressive playback
