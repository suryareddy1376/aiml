
  # Quickstart (From Scratch)

  Use this guide when sharing the project as a zip file with a friend.

  ## 1. Prerequisites

  Install these first:
  1. Node.js 18+
  2. npm 9+
  3. Python 3.10+
  4. A Supabase project (URL, anon key, service role key)

  ## 2. Unzip and Open Project

  1. Unzip the project.
  2. Open terminal in the project root folder: AI Education Guide.

  ## 3. Install Dependencies

  Run in order:

  ```bash
  cd client
  npm install

  cd ../server
  npm install

  cd ../ml
  pip install -r requirements.txt
  ```

  ## 4. Create Environment Files

  Create these files with your own values.

  ### client/.env

  ```env
  VITE_SUPABASE_URL=your_supabase_url
  VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
  VITE_API_URL=http://localhost:5005/api
  ```

  ### server/.env

  ```env
  SUPABASE_URL=your_supabase_url
  SUPABASE_SERVICE_KEY=your_supabase_service_role_key
  ML_SERVER_URL=http://localhost:5001
  JWT_SECRET=replace_with_random_secret
  PORT=5005
  CORS_ORIGIN=http://localhost:5173
  DATA_GOV_API_KEY=optional
  ```

  ### ml/.env (optional)

  ```env
  PORT=5001
  ```

  ## 5. Setup Supabase Database

  1. Open Supabase Dashboard.
  2. Go to SQL Editor.
  3. Run the full content of supabase_schema.sql.
  4. If permission errors appear later, run fix_permissions.sql.

  ## 6. Train ML Model (Required First Time)

  From project root:

  ```bash
  cd ml/model
  python train.py
  ```

  This creates/updates the prediction model file used by ml/app.py.

  ## 7. Run All Services

  Open 3 terminals.

  ### Terminal A: ML server

  ```bash
  cd ml
  python app.py
  ```

  ### Terminal B: Backend API server

  ```bash
  cd server
  npm run dev
  ```

  ### Terminal C: Frontend app

  ```bash
  cd client
  npm run dev
  ```

  Open the app at:
  http://localhost:5173

  ## 8. Basic Health Checks

  1. API health: http://localhost:5005/health
  2. ML health: http://localhost:5001/health

  If both return status ok, backend services are running correctly.

  ## 9. Test Checklist (End-to-End)

  Run these tests in sequence:
  1. Register a new student user.
  2. Login and open College Search.
  3. Open one college detail page.
  4. Save it to favourites and verify in Favourites page.
  5. Add 2 or more colleges to Compare and open Compare page.
  6. Test PDF export in Detail and Compare pages.
  7. Open Career Guide and verify unique career cards load.
  8. Test Request College page by submitting one request.

  Admin flow test:
  1. Promote one user to admin in Supabase profiles table.
  2. Login via /admin/login.
  3. Open Admin Dashboard and verify requests list loads.
  4. Approve a student request and check the college appears in search.
  5. Open Manage Colleges, edit a college, save changes.
  6. Delete a college from admin page and verify removal.

  ## 10. Promote Admin (SQL)

  Run in Supabase SQL Editor:

  ```sql
  update public.profiles
  set role = 'admin'
  where email = 'admin@example.com';
  ```

  ## 11. Useful Commands

  ### Client

  ```bash
  cd client
  npm run dev
  npm run build
  npm run lint
  npm run test:scoring
  ```

  ### Server

  ```bash
  cd server
  npm run dev
  npm run start
  ```

  ### ML

  ```bash
  cd ml
  python app.py

  cd model
  python train.py
  ```

  ## 12. Common Fixes

  1. If career model version warning appears:
    Retrain using python ml/model/train.py.

  2. If admin requests fail to load:
    Ensure college_requests table/policies are applied and restart server.

  3. If CORS blocked error appears:
    Add frontend origin to CORS_ORIGIN in server/.env and restart server.

  4. If python command uses wrong interpreter:
    Use your virtual environment python explicitly.

  ## 13. Share Checklist (Before Sending Zip)

  1. Remove secrets from all .env files.
  2. Keep only template/example values.
  3. Ensure README and this quickstart are included.
  4. Ensure model is trained or mention train step clearly.

  Project is ready for handoff after these steps.
