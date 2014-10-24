class: title, center, middle

# Import/Export API for Robots

### Carson Gee and Brandon DeRosier ###

---

# Rationale

At MIT, we support and heavily utilize a direct XML course development
workflow:

1. A content developer merges a change into a production branch
2. The developer pushes the change to a GitHub/Enterprise repository
3. The change is published immediately to whatever edX stack they're developing
   against:
   1. A webhook fires a request to a **tool**
   2. Said **tool** checks out the repository and *imports the course
      automatically*
