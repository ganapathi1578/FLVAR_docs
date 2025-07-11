Perfect. Below is your **API Documentation** in **Markdown format**, **split by logical sections**. Each section has a structured table based on the format you provided.


---

# 🧾 AR House Module – API Documentation

> 📄 File: `views.py`
> 🛡 All secured endpoints require `@require_api_key` unless mentioned.
> 🗃 CSRF exempted endpoints marked with `@csrf_exempt`.


---

## 🎯 Section 1: Models & Activation

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 36 | views.py | `/api/models/` | List all ML models | GET | None | JSON: list of models | `list_models()` | JsonResponse |
| 55 | views.py | `/api/models/activate/` | Activate a model by ID | POST | `model_id` (form-data) | JSON: message, model_name | `activate_model()` | JsonResponse |


---

## 📅 Section 2: Dates & Cameras

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 119 | views.py | `/api/dates/` | List all available dates | GET | None | JSON: dates list | `list_dates()` | JsonResponse |
| 157 | views.py | `/api/dates/<date_str>/cameras/` | List cameras on a date | GET | URL param: `date_str` | JSON: list of cameras | `list_cameras_for_date()` | JsonResponse |


---

## 🎞 Section 3: Stream / Metadata APIs

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 186 | views.py | `/api/streams/<date_str>/<camera_id>/metadata_index/` | Get `metadata_index.json` | GET | URL params: date, camera | JSON | `metadata_index()` | JsonResponse |
| 216 | views.py | `/api/streams/<date_str>/<camera_id>/playlist/` | Get proxied playlist URL | GET | URL params | JSON: HLS URL | `playlist_redirect()` | JsonResponse |
| 257 | views.py | `/api/streams/<date_str>/<camera_id>/recent/` | List last N segments | GET | Query: `count=N` | JSON: segment files list | `list_recent_segments()` | JsonResponse |
| 284 | views.py | `/api/streams/manifest/` | Get manifest of all streams | GET | None | JSON: { "YYYY-MM-DD": \[cams\] } | `all_streams_manifest()` | JsonResponse |


---

## 🔑 Section 4: Authentication & Users

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 331 | views.py | `/api/register/` | Get or register API key | POST | `username`, `password` (form-data) | JSON: api_key, username | `register_or_get_key()` | JsonResponse |
| 368 | views.py | `/api/view-api-key/` | View API key (logged in) | POST | API Key in header | JSON: api_key, created_at | `view_api_key()` | JsonResponse |
| 387 | views.py | `/api/regenerate-api-key/` | Regenerate API key | POST | `username`, `password` | JSON: regenerated key | `regenerate_api_key()` | JsonResponse |
| 314 | views.py | `/api/create-user/` | Create user (admin only) | POST | `username`, `password`, `email` | JSON: success message | `create_user()` | JsonResponse |


---

## 🗨️ Section 5: Feedback APIs

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 408 | views.py | `/api/feedback/` | Submit feedback & trim video | POST | JSON: start_time, end_time, video_url, feedback | JSON: success, trimmed_video path | `handle_feedback()` | JsonResponse |
| 542 | views.py | `/api/feedbacks/` | List all feedback entries | GET | API Key | JSON: list of feedback entries | `get_feedbacks()` | JsonResponse |


---

## 🎥 Section 6: Camera Management

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 561 | views.py | `/api/cameras/add/` | Add a new camera | POST | JSON: `source`, optional `name` | JSON: Camera details | `add_camera()` | JsonResponse |
| 593 | views.py | `/api/cameras/<camera_id>/edit/` | Edit existing camera | POST | JSON: name/source/is_turned_on | JSON: updated camera info | `edit_camera()` | JsonResponse |
| 629 | views.py | `/api/cameras/<camera_id>/delete/` | Delete camera | POST | None | JSON: success message | `delete_camera()` | JsonResponse |
| 648 | views.py | `/api/cameras/<camera_id>/toggle/` | Toggle on/off status | POST | None | JSON: toggled state | `toggle_camera()` | JsonResponse |
| 669 | views.py | `/api/cameras/list/` | List all cameras | POST | None | JSON: list of all cameras | `list_cameras()` | JsonResponse |
| 689 | views.py | `/api/cameras/<camera_id>/` | Get specific camera details | POST | None | JSON: camera details | `get_camera()` | JsonResponse |


---

## 🚨 Section 7: Triggers

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 710 | views.py | `/api/triggers/add/` | Add new trigger text | POST | JSON: `trigger_text` | JSON: created trigger | `add_trigger()` | JsonResponse |
| 734 | views.py | `/api/triggers/list/` | Get trigger list (optional filter) | POST | Query param: `active=1` | JSON: trigger list | `get_triggers()` | JsonResponse |
| 753 | views.py | `/api/triggers/delete/` | Delete trigger | POST | JSON: `trigger_id` | JSON: deletion status | `delete_trigger()` | JsonResponse |
| 784 | views.py | `/api/triggers/toggle/` | Toggle active/inactive | POST | JSON: `trigger_id`, `is_active` | JSON: updated trigger | `toggle_trigger()` | JsonResponse |


---

## 🧠 Section 8: Event Logs

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 827 | views.py | `/api/events/inspect/` | Filter and inspect events | POST | JSON: filters (date, person, action, etc.) | JSON: list of event logs | `inspect_events()` | JsonResponse |
| 885 | views.py | `/api/events/metadata/` | Get options for filters | GET | None | JSON: lists of actions, persons, etc. | `get_events_metadata()` | JsonResponse |


---

Perfect. Below is your **API Documentation** for the `trainningspace` app in **Markdown format**, **split by logical sections**. Each section has a structured table for clarity.


---

# 🧾 TrainningSpace – Model Marketplace Proxy API Documentation


---

## 🌐 Section 1: Model Marketplace

| Line | File | Endpoint | Purpose | Method | Request Data | Response | Receiver | Sender |
|----|----|----|----|----|----|----|----|----|
| 13 | views.py | `/trainningspace/model_marketplace/` | Fetch all public models | GET | Headers: house ID & auth hash | JSON: list of public models | `proxy_fetch_public_models()` | JsonResponse |
| 63 | views.py | `/trainningspace/model_details/` | Fetch specific model by ID | POST | JSON: `model_id`, headers | JSON: model details | `proxy_fetch_model_by_id()` | JsonResponse |

Perfect. Below is your **API Documentation** for the `orchestrator` app in **Markdown format**, split by **logical sections** with a structured table format for clarity.


---

# 🧠 Orchestrator – Model Container Management API Documentation

> \
> \
> \
> 📄 File: `orchestrator/views.py`🛡 Secured endpoints use `@require_api_key` unless otherwise specified.🐳 Uses Docker internally to manage model containers.🔐 Authenticated via config-loaded `house_id` and `secret_key` → `X-House-ID` + `X-Auth-Hash`


---

## ⚙️ Section 1: Model Container Lifecycle

| Line | Endpoint | Purpose | Method | Request JSON | Response | View Class |
|----|----|----|----|----|----|----|
| 29 | `/api/orchestrator/pull/` | Pull image tarball and start container | POST | `{ "model_id": "<model_id>" }` | ModelContainer JSON | `PullAndStartAPI` |
| 59 | `/api/orchestrator/start/` | Start existing stopped container | POST | `{ "model_id": "<model_id>" }` | ModelContainer JSON | `StartAPI` |
| 94 | `/api/orchestrator/stop/` | Stop a running container | POST | `{ "model_id": "<model_id>" }` | ModelContainer JSON | `StopAPI` |
| 128 | `/api/orchestrator/delete/` | Delete container and DB record | DELETE | `{ "model_id": "<model_id>" }` | HTTP 204 No Content | `DeleteAPI` |


---

## 🔁 Section 2: Version Management

| Line | Endpoint | Purpose | Method | Request JSON | Response | View Class |
|----|----|----|----|----|----|----|
| 167 | `/api/orchestrator/switch/` | Switch to a different model version | POST | `{ "model_id": "...", "version_id": "..." }` | Updated container JSON | `SwitchVersionAPI` |
| 307 | `/api/orchestrator/versions/` | Get remote + local version info & active state | POST | `{ "model_id": "<model_id>" }` | Merged model info | `FilteredModelDetailWithContainerInfoAPI` |


---

## 📋 Section 3: Listing and Sync

| Line | Endpoint | Purpose | Method | Request JSON | Response | View Class |
|----|----|----|----|----|----|----|
| 242 | `/api/orchestrator/` | List all local model containers | GET | None | List of ModelContainer objects | `ListAPI` |
| 274 | `/api/orchestrator/models/` | Sync local model IDs with marketplace metadata | POST | None | Merged model + local status | `ModelListByIdsAPI` |


---


