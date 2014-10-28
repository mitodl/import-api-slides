class: title, center, middle

# Import/Export API for Robots

### Carson Gee and Brandon DeRosier


---


## **Background** > The Git-based XML Workflow

### At MIT, we support and heavily utilize a direct XML course development workflow:

1. A content developer merges a change into a production branch
2. The developer pushes the change to a GitHub/Enterprise repository
3. The change is published immediately to whatever edX stack they're developing
   against:
   1. A webhook fires a request to a **tool**
   2. Said **tool** checks out the repository and *imports the course
      automatically*

Currently, there are two different tools that consume these webhook payloads..

---


## **Background** > The Webhook Consumers

### gitreload - *for **residential** courses*
- Hosted on our app boxes alongside the LMS
- Runs the `course_import` Django management command

### git2edx - *for **MOOCs** on edx.org*
- Runs on it's own VM
- Imports the course on **studio.edx.org** :
  1. **GET** `/signin` for CSRF token cookie
  2. **POST** `/login_post` with login fields for session cookie
  3. **POST** `/import/<course_id>/<filename>` with course archive


---


## **Rationale** > Inherent Fragility at the Import Stage

### Not intended for robots
- Must obtain CSRF token via arbitrary request intended for browsers (returns HTML)
- Sessions for authentication

### Subject to change as UI changes
- Modeled around user interaction
- **No API Versioning = No Real Support**


---

class: center, middle

## **Design** > The Analytics Data API As a Model

### Intended for robots
- Uses Django Rest Framework
- Token authentication
- API versioning
- Returns JSON and CSV


---


## **Design** > Django Rest Framework

- Supports token auth and oauth2 out of the box

Other APIs using it:
- Mobile API?
- Notifier API?
- User API?


---


## **Design** > Authentication

Token authentication?

Need good vs. of Token 


---


## **Design** > API URLs

### Import:
```python
POST | PUT import/ (org/course/run) | (course-v1:org+course+run)
```
- Multipart form post

### Export:
```sh
GET export/ (org/course/run) | (course-v1:org+course+run)
```
- HTTP_ACCEPT = 'application/x-tgz'


---


## **Design** > Versioning the URLs

### Similar to the Analytics Data API

In Studio's URLs:
```python
urlpatterns = patterns(
    '',
    url(r'^api/v0/', include('api.v0.urls', namespace='v0')),
)
```
- Solidify support


---


## **Example usage** > Authenticate and Import

Walkthrough:
- Authenticate
- Import
