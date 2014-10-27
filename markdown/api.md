class: title, center, middle

# Import/Export API for Robots

### Carson Gee and Brandon DeRosier


---


## Background - XML workflow

At MIT, we support and heavily utilize a direct XML course development
workflow:

1. A content developer merges a change into a production branch
2. The developer pushes the change to a GitHub/Enterprise repository
3. The change is published immediately to whatever edX stack they're developing
   against:
   1. A webhook fires a request to a **tool**
   2. Said **tool** checks out the repository and *imports the course
      automatically*

---


## Background - Tools to automate this workflow

- gitreload for residential
- git2edx for MOOC


---


## Rationale - Fragility at the import stage

- Authentication uses CSRF passed by cookie.
- It's not intended for robots.
- Subject to change as UI changes


---


## Design - Similar APIs in edX


---


## Design - Django rest framework

Other APIs using it:
- Mobile API?
- Notifier API?
- User API?


---


## Design - Authentication

- Don't use session authentication
- django-oauth2-provider?
- How to protect against CSRF without the cookie


---


## Design - Proposed API URLs

- Import URL
- Export URL


---


## Example usage - Authenticate and import a course


---


## Design - Versioning the URLs

