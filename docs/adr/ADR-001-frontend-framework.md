ADR-001 — Frontend Framework
Date: 18/06/26
Status: Accepted

Context:
Rippl is a web application requiring user authentication, dynamic 
dashboards, saved scenario data, and AI-generated content rendered 
per-user. The frontend must support component-based UI, client-side 
interactivity, and ideally share a codebase with backend logic to 
keep solo development manageable. We need to select a frontend 
approach before development begins.

Decision:
We will use Next.js (App Router) as the frontend framework, 
deployed on Vercel. Next.js was chosen for its built-in server-side 
rendering, file-based routing, and ability to handle both frontend 
and lightweight backend logic in a single codebase.

Alternatives Considered:

1. Plain React (no framework)
   Rejected because React alone has no built-in routing, no 
   server-side rendering, and no backend capability. We would 
   need to separately add React Router, a separate build tool, 
   and a standalone backend service — adding complexity without 
   added benefit for our use case.

2. HTML + CSS + vanilla JavaScript
   Rejected because Rippl requires authentication, shared state 
   across views (user profile data feeding multiple scenarios), 
   reusable UI components (comparison tables, charts), and a 
   backend for data and AI calls. Vanilla JS would require 
   manually building all of this from scratch, which does not 
   scale well past a simple static site.

Consequences:

Positive:
- Authenticated dashboard (scenarios, profile, saved results) can 
  be built as a dynamic, component-based application
- Frontend and lightweight backend logic share one codebase, 
  reducing context-switching for a solo developer
- Built-in SSR improves initial load performance and SEO for 
  public-facing pages (e.g. waitlist landing page)
- Deployment to Vercel is near-automatic, reducing DevOps overhead

Negative / Risks:
- API routes run as serverless functions with execution time 
  limits — heavy computation (tax engine, 5-year projections) 
  must be benchmarked to stay within limits
- Introduces a dependency on Vercel's platform and pricing model
- Adds framework concepts (server vs client components, hydration) 
  that increase the learning curve compared to plain React
- May require extracting the scenario engine into a separate 
  backend service later if serverless constraints become limiting
