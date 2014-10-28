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
  2. **POST** login fields to `/login_post` for session cookie
  3. **POST** course archive to `/import/<course_id>/<filename>`


---


## **Rationale** > Inherent Fragility at the Import Stage

- Authentication uses CSRF passed by cookie.
- It's not intended for robots.
- Subject to change as UI changes


---


## **Design** > Similar APIs in edX


---


## **Design** > Django Rest Framework

Other APIs using it:
- Mobile API?
- Notifier API?
- User API?


---


## **Design** > Authentication

- Don't use session authentication
- django-oauth2-provider?
- How to protect against CSRF without the cookie


---


## **Design** > Proposed API URLs

- Import URL
- Export URL


---


## **Design** > Versioning the URLs


---


## **Example usage** > Authenticate and Import

