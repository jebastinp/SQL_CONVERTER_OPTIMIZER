-- Drop the old trigger and function, we'll recreate properly
DROP TRIGGER IF EXISTS on_auth_user_created ON auth.users;
DROP FUNCTION IF EXISTS public.handle_new_user();

-- Recreate with proper permissions
CREATE OR REPLACE FUNCTION public.handle_new_user()
RETURNS TRIGGER
LANGUAGE plpgsql
SECURITY DEFINER
SET search_path = public
AS $$
BEGIN
  INSERT INTO public.profiles (id, email, full_name)
  VALUES (
    NEW.id,
    NEW.email,
    COALESCE(NEW.raw_user_meta_data->>'full_name', split_part(NEW.email, '@', 1))
  )
  ON CONFLICT (id) DO NOTHING;
  RETURN NEW;
EXCEPTION
  WHEN OTHERS THEN
    -- Don't block signup if profile creation fails for any reason
    RAISE WARNING 'handle_new_user failed: %', SQLERRM;
    RETURN NEW;
END;
$$;

-- Recreate the trigger
CREATE TRIGGER on_auth_user_created
  AFTER INSERT ON auth.users
  FOR EACH ROW EXECUTE FUNCTION public.handle_new_user();

-- Grant permission for the trigger to write to profiles
GRANT INSERT ON public.profiles TO supabase_auth_admin;
GRANT USAGE ON SCHEMA public TO supabase_auth_admin;


 GET /_next/static/chunks/fallback/webpack.js?ts=1779327340493 500 in 29ms
 GET /_next/static/chunks/fallback/main.js?ts=1779327340493 500 in 26ms
 GET /_next/static/chunks/fallback/pages/_app.js?ts=1779327340493 500 in 26ms
 GET /_next/static/chunks/fallback/pages/_error.js?ts=1779327340493 500 in 25ms
 GET /_next/static/chunks/fallback/react-refresh.js?ts=1779327340493 500 in 25ms







 jebastin@Jebastins-MacBook-Air routeflow-final % bash start.sh
=========================================
  RouteFlow AI — Starting
=========================================

✓ Python 3.9 found
✓ Node v24.8.0 found

[SETUP] Creating Python virtual environment…
[SETUP] Installing Python packages (this takes 1–2 minutes)…
[SETUP] Backend ready

[SETUP] Installing Node packages (this takes 1–2 minutes)…
[SETUP] Frontend ready

=========================================
  Starting both servers…
=========================================
  Backend:  http://localhost:8000
  Frontend: http://localhost:3000
  Diagnostic page: http://localhost:3000/diagnostic

Press Ctrl+C to stop both servers.

[FRONTEND] 
[FRONTEND] > routeflow-frontend@4.0.0 dev
[FRONTEND] > next dev
[FRONTEND] 
[BACKEND]  INFO:     Will watch for changes in these directories: ['/Users/jebastin/Downloads/routeflow-final/backend']
[BACKEND]  INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
[BACKEND]  INFO:     Started reloader process [41282] using WatchFiles
[FRONTEND]   ▲ Next.js 14.2.13
[FRONTEND]   - Local:        http://localhost:3000
[FRONTEND]   - Environments: .env.local
[FRONTEND] 
[FRONTEND]  ✓ Starting...
[FRONTEND]  ✓ Ready in 3.2s
[BACKEND]  INFO:     Started server process [41308]
[BACKEND]  INFO:     Waiting for application startup.
[BACKEND]  INFO:     Application startup complete.
[FRONTEND]  ○ Compiling / ...
[FRONTEND]  ✓ Compiled / in 1329ms (438 modules)
[FRONTEND]  GET / 200 in 1458ms
[FRONTEND]  ✓ Compiled /_error in 117ms (440 modules)
[FRONTEND]  GET /apple-touch-icon-precomposed.png 404 in 141ms
[FRONTEND]  GET /apple-touch-icon.png 404 in 135ms
[FRONTEND]  ✓ Compiled /dashboard in 151ms (468 modules)
[FRONTEND]  ✓ Compiled /orders in 255ms (490 modules)
[FRONTEND]  ✓ Compiled /drivers in 165ms (502 modules)
[FRONTEND]  ✓ Compiled /routes in 409ms (524 modules)
[FRONTEND]  ✓ Compiled /analytics in 126ms (530 modules)
[BACKEND]  🚀 RouteFlow backend up
[BACKEND]     CORS: ['http://localhost:3000', 'http://127.0.0.1:3000']
[BACKEND]     Supabase: https://dxppvsnorhwznthqalph.supabase.co
[BACKEND]     ORS: set
[BACKEND]     OR-Tools: installed
[BACKEND]  INFO:     127.0.0.1:58224 - "OPTIONS /geocode/batch HTTP/1.1" 200 OK
[BACKEND]  INFO:     127.0.0.1:58224 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58227 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58231 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58239 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58442 - "OPTIONS /geocode/batch HTTP/1.1" 200 OK
[BACKEND]  INFO:     127.0.0.1:58442 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized
[BACKEND]  INFO:     127.0.0.1:58450 - "POST /geocode/batch HTTP/1.1" 401 Unauthorized


