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




"""JWT verification using Supabase JWT secret."""
import os
import jwt
from typing import Optional


def verify_user_jwt(token: str) -> Optional[dict]:
    secret = os.getenv("SUPABASE_JWT_SECRET", "")
    if not secret or not token:
        return None
    try:
        payload = jwt.decode(
            token,
            secret,
            algorithms=["HS256"],
            options={"verify_aud": False},
        )
        if not payload.get("sub") and payload.get("role") not in ("authenticated", "service_role"):
            return None
        return payload
    except jwt.ExpiredSignatureError:
        print("[auth] Token expired")
        return None
    except jwt.InvalidSignatureError:
        print("[auth] Invalid signature — check SUPABASE_JWT_SECRET")
        return None
    except Exception as e:
        print(f"[auth] JWT decode failed: {type(e).__name__}: {e}")
        return None



DROP TABLE IF EXISTS driver_positions CASCADE;
DROP TABLE IF EXISTS delivery_stops CASCADE;
DROP TABLE IF EXISTS routes CASCADE;
DROP TABLE IF EXISTS orders CASCADE;
DROP TABLE IF EXISTS drivers CASCADE;
DROP TABLE IF EXISTS geocode_cache CASCADE;
DROP TABLE IF EXISTS profiles CASCADE;
DROP FUNCTION IF EXISTS public.handle_new_user CASCADE;


DROP TABLE IF EXISTS driver_positions CASCADE;
DROP TABLE IF EXISTS delivery_stops CASCADE;
DROP TABLE IF EXISTS routes CASCADE;
DROP TABLE IF EXISTS orders CASCADE;
DROP TABLE IF EXISTS drivers CASCADE;
DROP TABLE IF EXISTS geocode_cache CASCADE;
DROP TABLE IF EXISTS profiles CASCADE;
DROP FUNCTION IF EXISTS public.handle_new_user CASCADE;



-- RouteFlow AI — Simplified Schema
-- Run this ENTIRE file in Supabase SQL Editor.

CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
CREATE EXTENSION IF NOT EXISTS "pgcrypto";

-- ============================================================
-- TABLES
-- ============================================================

CREATE TABLE IF NOT EXISTS profiles (
  id            UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  email         TEXT NOT NULL,
  full_name     TEXT,
  company_name  TEXT,
  depot_lat     NUMERIC(10,7) DEFAULT 51.5095,
  depot_lng     NUMERIC(10,7) DEFAULT -0.1245,
  depot_address TEXT DEFAULT 'Central Depot, Covent Garden, London',
  depot_postcode TEXT DEFAULT 'WC2E 8RF',
  avg_speed_kmh NUMERIC(5,2) DEFAULT 22.0,
  fuel_price_gbp NUMERIC(5,3) DEFAULT 1.480,
  vehicle_kml   NUMERIC(5,2) DEFAULT 9.0,
  created_at    TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE IF NOT EXISTS drivers (
  id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  user_id         UUID NOT NULL REFERENCES profiles(id) ON DELETE CASCADE,
  name            TEXT NOT NULL,
  phone           TEXT,
  vehicle         TEXT,
  capacity        INT NOT NULL DEFAULT 30,
  color           TEXT DEFAULT '#5b8cff',
  access_token    TEXT UNIQUE DEFAULT encode(gen_random_bytes(16), 'hex'),
  current_lat     NUMERIC(10,7),
  current_lng     NUMERIC(10,7),
  last_seen       TIMESTAMPTZ,
  created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX IF NOT EXISTS drivers_user_idx ON drivers(user_id);
CREATE INDEX IF NOT EXISTS drivers_token_idx ON drivers(access_token);

CREATE TABLE IF NOT EXISTS orders (
  id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  user_id         UUID NOT NULL REFERENCES profiles(id) ON DELETE CASCADE,
  customer_name   TEXT NOT NULL,
  address         TEXT NOT NULL,
  phone           TEXT,
  lat             NUMERIC(10,7),
  lng             NUMERIC(10,7),
  geocoded        BOOLEAN DEFAULT FALSE,
  status          TEXT NOT NULL DEFAULT 'pending',
  created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX IF NOT EXISTS orders_user_idx ON orders(user_id);

CREATE TABLE IF NOT EXISTS geocode_cache (
  id            UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  query         TEXT NOT NULL UNIQUE,
  lat           NUMERIC(10,7) NOT NULL,
  lng           NUMERIC(10,7) NOT NULL,
  created_at    TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX IF NOT EXISTS geocode_query_idx ON geocode_cache(query);

CREATE TABLE IF NOT EXISTS routes (
  id                UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  user_id           UUID NOT NULL REFERENCES profiles(id) ON DELETE CASCADE,
  driver_id         UUID NOT NULL REFERENCES drivers(id) ON DELETE CASCADE,
  status            TEXT NOT NULL DEFAULT 'planned',
  depot_lat         NUMERIC(10,7) NOT NULL,
  depot_lng         NUMERIC(10,7) NOT NULL,
  distance_km       NUMERIC(8,2),
  duration_minutes  NUMERIC(8,1),
  fuel_saved_gbp    NUMERIC(8,2),
  baseline_km       NUMERIC(8,2),
  created_at        TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX IF NOT EXISTS routes_user_idx ON routes(user_id);
CREATE INDEX IF NOT EXISTS routes_driver_idx ON routes(driver_id);

CREATE TABLE IF NOT EXISTS delivery_stops (
  id            UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  route_id      UUID NOT NULL REFERENCES routes(id) ON DELETE CASCADE,
  order_id      UUID NOT NULL REFERENCES orders(id) ON DELETE CASCADE,
  user_id       UUID NOT NULL REFERENCES profiles(id) ON DELETE CASCADE,
  sequence      INT NOT NULL,
  eta_clock     TEXT,
  completed_at  TIMESTAMPTZ,
  status        TEXT NOT NULL DEFAULT 'pending',
  customer_token TEXT DEFAULT encode(gen_random_bytes(12), 'hex'),
  UNIQUE(route_id, sequence)
);
CREATE INDEX IF NOT EXISTS stops_route_idx ON delivery_stops(route_id);
CREATE INDEX IF NOT EXISTS stops_token_idx ON delivery_stops(customer_token);

CREATE TABLE IF NOT EXISTS driver_positions (
  id          UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  driver_id   UUID NOT NULL REFERENCES drivers(id) ON DELETE CASCADE,
  user_id     UUID NOT NULL REFERENCES profiles(id) ON DELETE CASCADE,
  lat         NUMERIC(10,7) NOT NULL,
  lng         NUMERIC(10,7) NOT NULL,
  recorded_at TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX IF NOT EXISTS positions_driver_time_idx ON driver_positions(driver_id, recorded_at DESC);

-- ============================================================
-- AUTO-CREATE PROFILE ON SIGNUP (with proper permissions)
-- ============================================================

DROP TRIGGER IF EXISTS on_auth_user_created ON auth.users;
DROP FUNCTION IF EXISTS public.handle_new_user();

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
    RAISE WARNING 'handle_new_user failed: %', SQLERRM;
    RETURN NEW;
END;
$$;

CREATE TRIGGER on_auth_user_created
  AFTER INSERT ON auth.users
  FOR EACH ROW EXECUTE FUNCTION public.handle_new_user();

GRANT INSERT ON public.profiles TO supabase_auth_admin;
GRANT USAGE ON SCHEMA public TO supabase_auth_admin;

-- ============================================================
-- RLS
-- ============================================================

ALTER TABLE profiles         ENABLE ROW LEVEL SECURITY;
ALTER TABLE drivers          ENABLE ROW LEVEL SECURITY;
ALTER TABLE orders           ENABLE ROW LEVEL SECURITY;
ALTER TABLE routes           ENABLE ROW LEVEL SECURITY;
ALTER TABLE delivery_stops   ENABLE ROW LEVEL SECURITY;
ALTER TABLE driver_positions ENABLE ROW LEVEL SECURITY;
ALTER TABLE geocode_cache    ENABLE ROW LEVEL SECURITY;

DROP POLICY IF EXISTS profiles_self ON profiles;
CREATE POLICY profiles_self ON profiles FOR ALL USING (id = auth.uid()) WITH CHECK (id = auth.uid());

DROP POLICY IF EXISTS drivers_own ON drivers;
CREATE POLICY drivers_own ON drivers FOR ALL USING (user_id = auth.uid()) WITH CHECK (user_id = auth.uid());

DROP POLICY IF EXISTS drivers_public_read ON drivers;
CREATE POLICY drivers_public_read ON drivers FOR SELECT USING (true);

DROP POLICY IF EXISTS drivers_anon_update ON drivers;
CREATE POLICY drivers_anon_update ON drivers FOR UPDATE USING (true);

DROP POLICY IF EXISTS orders_own ON orders;
CREATE POLICY orders_own ON orders FOR ALL USING (user_id = auth.uid()) WITH CHECK (user_id = auth.uid());

DROP POLICY IF EXISTS orders_public_read ON orders;
CREATE POLICY orders_public_read ON orders FOR SELECT USING (true);

DROP POLICY IF EXISTS routes_own ON routes;
CREATE POLICY routes_own ON routes FOR ALL USING (user_id = auth.uid()) WITH CHECK (user_id = auth.uid());

DROP POLICY IF EXISTS routes_public_read ON routes;
CREATE POLICY routes_public_read ON routes FOR SELECT USING (true);

DROP POLICY IF EXISTS stops_own ON delivery_stops;
CREATE POLICY stops_own ON delivery_stops FOR ALL USING (user_id = auth.uid()) WITH CHECK (user_id = auth.uid());

DROP POLICY IF EXISTS stops_public_read ON delivery_stops;
CREATE POLICY stops_public_read ON delivery_stops FOR SELECT USING (true);

DROP POLICY IF EXISTS stops_anon_update ON delivery_stops;
CREATE POLICY stops_anon_update ON delivery_stops FOR UPDATE USING (true);

DROP POLICY IF EXISTS positions_own ON driver_positions;
CREATE POLICY positions_own ON driver_positions FOR ALL USING (user_id = auth.uid()) WITH CHECK (user_id = auth.uid());

DROP POLICY IF EXISTS positions_public_read ON driver_positions;
CREATE POLICY positions_public_read ON driver_positions FOR SELECT USING (true);

DROP POLICY IF EXISTS positions_anon_insert ON driver_positions;
CREATE POLICY positions_anon_insert ON driver_positions FOR INSERT WITH CHECK (true);

DROP POLICY IF EXISTS geocode_read ON geocode_cache;
CREATE POLICY geocode_read ON geocode_cache FOR SELECT USING (true);
DROP POLICY IF EXISTS geocode_insert ON geocode_cache;
CREATE POLICY geocode_insert ON geocode_cache FOR INSERT WITH CHECK (true);

-- ============================================================
-- Realtime
-- ============================================================

DO $$ BEGIN
  ALTER PUBLICATION supabase_realtime ADD TABLE driver_positions;
EXCEPTION WHEN duplicate_object THEN NULL; END $$;
DO $$ BEGIN
  ALTER PUBLICATION supabase_realtime ADD TABLE delivery_stops;
EXCEPTION WHEN duplicate_object THEN NULL; END $$;

-- Done.

final test : 

   ALTER TABLE drivers ADD COLUMN IF NOT EXISTS start_address TEXT;
   ALTER TABLE drivers ADD COLUMN IF NOT EXISTS start_lat NUMERIC(10,7);
   ALTER TABLE drivers ADD COLUMN IF NOT EXISTS start_lng NUMERIC(10,7);




Each request must have own request id and each id must be tracked in log along with each log must be written in a seperate file , All the credentials must load from env file and each table must have uuid(to frontend) and id(primary key for mapping) and a seperate code if needed, No constants should be hardcoded it should be in constants file and all the api key must be in .env file -- Follow strictly , Dont change the existing code logics just change the code as per the folder structure that has been provided to you along with the instructions provided to you , USE SOLID principles properly and write functions in async await do dependency injection,repository pattern and create a single instance for db and pass it over there




From Settings → API

Project URL — looks like https://abcdefgh.supabase.co
anon public key — long JWT starting with eyJhbG...
service_role secret key — long JWT starting with eyJhbG... (keep secret, backend only)
JWT Secret — scroll down to "JWT Settings", reveal & copy


From Cloudflare R2 dashboard (separate from Supabase)

Account ID
Access Key ID + Secret Access Key (R2 → Manage R2 API Tokens → Create with Object Read & Write)
Bucket name (you can use tarel-products or whatever)
Public URL (R2 → your bucket → Settings → Public Access — enable, copy the pub-xxx.r2.dev URL)

From Settings → Database → Connection string

Session pooler URL (port 5432) — looks like postgresql://postgres.[ref]:[password]@aws-0-[region].pooler.supabase.com:5432/postgres

Query 1 — Extensions (run first, once)
sql-- Required extensions
create extension if not exists "uuid-ossp";
create extension if not exists "pgcrypto";

Query 2
-- ============================================================================
-- Tarel v2 schema
-- Every table: id (BIGSERIAL PK), uuid (frontend), code (human-readable),
-- created_at, updated_at
-- ============================================================================

-- ── Users ───────────────────────────────────────────────────────────────────
create table if not exists public.users (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  supabase_id   uuid not null unique,
  name          varchar(120) not null,
  email         varchar(255) not null unique,
  role          varchar(16) not null default 'user' check (role in ('user','admin')),
  profile_photo varchar(500),
  phone         varchar(30),
  address_line1 varchar(255),
  locality      varchar(120),
  city          varchar(120),
  postcode      varchar(12),
  user_code     varchar(16) unique,
  is_active     boolean not null default true,
  last_sign_in_at timestamptz,
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);
create index if not exists idx_users_supabase_id on public.users(supabase_id);
create index if not exists idx_users_email on public.users(email);

-- ── Categories ──────────────────────────────────────────────────────────────
create table if not exists public.categories (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  name          varchar(120) not null,
  slug          varchar(140) not null unique,
  description   text,
  is_active     boolean not null default true,
  sort_order    integer not null default 0,
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);

-- ── Products ────────────────────────────────────────────────────────────────
create table if not exists public.products (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  name          varchar(160) not null,
  slug          varchar(180) not null unique,
  description   text,
  price_per_kg  double precision not null,
  half_kg_price double precision,
  one_kg_price  double precision,
  image_url     varchar(500),
  image_key     varchar(500),
  stock_kg      double precision not null default 0,
  is_dry        boolean not null default false,
  is_active     boolean not null default true,
  category_id   bigint not null references public.categories(id) on delete restrict,
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);
create index if not exists idx_products_slug on public.products(slug);
create index if not exists idx_products_category on public.products(category_id);

-- ── Cut & clean options ─────────────────────────────────────────────────────
create table if not exists public.cut_clean_options (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  label         varchar(200) not null,
  is_active     boolean not null default true,
  sort_order    double precision not null default 0,
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);

-- ── Delivery settings ───────────────────────────────────────────────────────
create table if not exists public.delivery_settings (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  cutoff_day    integer not null default 4,
  delivery_day  integer not null default 2,
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);

-- Seed default delivery window (Thursday cutoff, Wednesday delivery)
insert into public.delivery_settings (cutoff_day, delivery_day)
select 4, 2
where not exists (select 1 from public.delivery_settings);

-- ── Orders ──────────────────────────────────────────────────────────────────
create table if not exists public.orders (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  user_id       bigint not null references public.users(id) on delete restrict,
  status        varchar(20) not null default 'pending'
                check (status in ('pending','paid','processing','out_for_delivery','delivered','cancelled')),
  total_amount  double precision not null default 0,
  order_date    date not null default current_date,
  delivery_date date,
  delivery_slot varchar(60),
  notes         text,
  cancelled_at  timestamptz,
  paid_at       timestamptz,
  delivered_at  timestamptz,
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);
create index if not exists idx_orders_user on public.orders(user_id);
create index if not exists idx_orders_status on public.orders(status);
create index if not exists idx_orders_delivery_date on public.orders(delivery_date);

-- ── Order items ─────────────────────────────────────────────────────────────
create table if not exists public.order_items (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  order_id      bigint not null references public.orders(id) on delete cascade,
  product_id    bigint not null references public.products(id) on delete restrict,
  product_name  varchar(160) not null,
  qty_kg        double precision not null,
  price_per_kg  double precision not null,
  line_total    double precision not null,
  cut_clean_label varchar(200),
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);
create index if not exists idx_order_items_order on public.order_items(order_id);

-- ── Support messages ────────────────────────────────────────────────────────
create table if not exists public.support_messages (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  user_id       bigint not null references public.users(id) on delete cascade,
  subject       varchar(160) not null,
  message       text not null,
  response      text,
  status        varchar(16) not null default 'open' check (status in ('open','pending','closed')),
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);

-- ── Delivery orders (legacy ops scheduling) ─────────────────────────────────
create table if not exists public.delivery_orders (
  id              bigserial primary key,
  uuid            uuid not null unique default gen_random_uuid(),
  code            varchar(32) unique,
  customer_name   varchar(120) not null,
  customer_phone  varchar(30) not null,
  item_type       varchar(10) not null,
  item_name       varchar(160) not null,
  quantity_kg     numeric(6,2) not null,
  order_date      date not null,
  delivery_date   date not null,
  status          varchar(10) not null default 'active',
  cancelled_at    timestamptz,
  created_at      timestamptz not null default now(),
  updated_at      timestamptz not null default now()
);

-- ── Site settings (key/value) ───────────────────────────────────────────────
create table if not exists public.site_settings (
  id            bigserial primary key,
  uuid          uuid not null unique default gen_random_uuid(),
  code          varchar(32) unique,
  key           varchar(80) not null unique,
  value         text,
  created_at    timestamptz not null default now(),
  updated_at    timestamptz not null default now()
);


Query 4 — Disable RLS on these tables
We're verifying tokens in the FastAPI backend and going through the connection pooler as postgres, so we don't need Supabase's row-level security here.

alter table public.users             disable row level security;
alter table public.categories        disable row level security;
alter table public.products          disable row level security;
alter table public.cut_clean_options disable row level security;
alter table public.delivery_settings disable row level security;
alter table public.orders            disable row level security;
alter table public.order_items       disable row level security;
alter table public.support_messages  disable row level security;
alter table public.delivery_orders   disable row level security;
alter table public.site_settings     disable row level security;

Query 5 — Create the first admin (run AFTER you sign up)

First, sign up normally through your app at /register (or Authentication → Users → Add user in Supabase dashboard) using your own email.
Then run this, replacing the email:

sqlupdate public.users
set role = 'admin'
where email = 'your-email@example.com';


create or replace function public.set_updated_at()
returns trigger language plpgsql as $$
begin
  new.updated_at = now();
  return new;
end;
$$;

do $$
declare
  t text;
begin
  for t in
    select unnest(array[
      'users','categories','products','cut_clean_options','delivery_settings',
      'orders','order_items','support_messages','delivery_orders','site_settings'
    ])
  loop
    execute format('drop trigger if exists trg_%I_updated_at on public.%I', t, t);
    execute format(
      'create trigger trg_%I_updated_at before update on public.%I
       for each row execute function public.set_updated_at()', t, t
    );
  end loop;
end$$;























Here’s your complete prompt to give to Claude:

TAREL FISH DELIVERY — COMPLETE INTERNAL MANAGEMENT SYSTEM

PROJECT OVERVIEW

Build a complete internal web application for a fish and meat delivery business operating in Scotland (Edinburgh, Glasgow, Livingston, Bathgate, Inverness routes). The team receives orders via WhatsApp, processes them manually, generates invoices, and delivers weekly. This app replaces their entire Excel workflow.

Tech Stack: Flask + PostgreSQL + HTML/CSS/JS (mobile-first, no React framework needed)

BUSINESS RULES (CRITICAL — embed these everywhere)

	•	Freight surcharge: £1.50 per kg (fish only, NOT meat/goat products)
	•	Small order charge: £2.00 extra if order total is under £30
	•	Inverness delivery charge: £13.00 flat
	•	Profit split: Martin 50% / Danny 40% / Ministry 10%
	•	Two vendors: Avra Impex (primary) and Global Food (secondary)
	•	Two drivers: Martin (Edinburgh/Livingston/Bathgate routes) and Danny (Glasgow route)
	•	Delivery cycle: Orders taken Monday–Friday, delivered following Wednesday
	•	Customer ID format: AreaCode + Year + Number (e.g. ED26105, GL26052, BA26113)
	•	Payment reference format: AreaCode + Year + Number (e.g. EH26210, IN26030)
	•	Bank details on every invoice: Daniel Maria Lazar / Sort: 80-48-88 / Account: 13616562
	•	Pricing: each fish has a 1kg price AND a half kg price (half kg costs more per kg as a markup strategy)
	•	Price calculation: 2kg = 1kg + 1kg price; 1.5kg = 1kg price + half kg price

DATABASE SCHEMA

-- Users (internal team)
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  username VARCHAR(50) UNIQUE,
  password_hash VARCHAR(255),
  role VARCHAR(20), -- 'admin', 'martin', 'danny', 'team'
  created_at TIMESTAMP DEFAULT NOW()
);

-- Customers
CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  customer_id VARCHAR(20) UNIQUE, -- e.g. ED26105
  name VARCHAR(150),
  phone VARCHAR(30),
  address TEXT,
  area VARCHAR(100),
  postcode VARCHAR(15),
  notes TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Fish/Product Master
CREATE TABLE fish_master (
  id SERIAL PRIMARY KEY,
  fish_name VARCHAR(200), -- full name e.g. "(1kg) King Fish (Slice)"
  english_name VARCHAR(150),
  tamil_name VARCHAR(150),
  malayalam_name VARCHAR(150),
  size VARCHAR(10), -- '1kg' or '0.5kg'
  avra_impex_price DECIMAL(10,2), -- vendor cost
  global_food_price DECIMAL(10,2), -- vendor 2 cost
  selling_price DECIMAL(10,2), -- customer price
  cut_type VARCHAR(100), -- e.g. "Steak", "Clean and Cut"
  is_fish BOOLEAN DEFAULT TRUE, -- FALSE for goat/meat products
  is_active BOOLEAN DEFAULT TRUE
);

-- Delivery Weeks
CREATE TABLE delivery_weeks (
  id SERIAL PRIMARY KEY,
  week_start DATE,
  week_end DATE,
  delivery_date DATE, -- the Wednesday
  status VARCHAR(20) DEFAULT 'open', -- 'open', 'vendor_report_sent', 'delivered', 'closed'
  created_at TIMESTAMP DEFAULT NOW()
);

-- Orders (one per customer per week)
CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  customer_id INTEGER REFERENCES customers(id),
  delivery_week_id INTEGER REFERENCES delivery_weeks(id),
  payment_reference VARCHAR(30),
  order_date DATE,
  delivery_date DATE,
  driver VARCHAR(50), -- 'Martin' or 'Danny'
  route VARCHAR(50), -- 'Edinburgh', 'Glasgow', 'Inverness', 'Livingston', 'Bathgate'
  delivery_stop_number INTEGER,
  status VARCHAR(30) DEFAULT 'received', 
  -- statuses: received, availability_confirmed, invoice_sent, payment_pending, payment_received, payment_verified, delivered
  delivery_instructions TEXT,
  order_platform VARCHAR(50) DEFAULT 'WhatsApp',
  raw_whatsapp_text TEXT, -- original message pasted by team
  created_by INTEGER REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW()
);

-- Order Items (one row per fish per order)
CREATE TABLE order_items (
  id SERIAL PRIMARY KEY,
  order_id INTEGER REFERENCES orders(id),
  fish_master_id INTEGER REFERENCES fish_master(id),
  fish_name VARCHAR(200), -- stored at time of order
  quantity_kg DECIMAL(10,3),
  unit_price DECIMAL(10,2),
  line_total DECIMAL(10,2),
  cut_instructions TEXT,
  availability_status VARCHAR(20) DEFAULT 'pending', -- 'pending', 'available', 'not_available'
  availability_checked_by INTEGER REFERENCES users(id),
  availability_checked_at TIMESTAMP
);

-- Invoices
CREATE TABLE invoices (
  id SERIAL PRIMARY KEY,
  order_id INTEGER REFERENCES orders(id),
  invoice_number VARCHAR(30),
  subtotal DECIMAL(10,2),
  freight_surcharge DECIMAL(10,2),
  delivery_charge DECIMAL(10,2),
  total DECIMAL(10,2),
  generated_at TIMESTAMP,
  sent_at TIMESTAMP,
  sent_by INTEGER REFERENCES users(id)
);

-- Payments
CREATE TABLE payments (
  id SERIAL PRIMARY KEY,
  order_id INTEGER REFERENCES orders(id),
  invoice_id INTEGER REFERENCES invoices(id),
  amount DECIMAL(10,2),
  payment_mode VARCHAR(50), -- 'Bank Transfer', 'Cash', 'UPI'
  payment_name VARCHAR(150), -- name used on bank transfer
  payment_received_date DATE,
  payment_verified_by INTEGER REFERENCES users(id),
  payment_verified_at TIMESTAMP,
  status VARCHAR(20) DEFAULT 'pending', -- 'pending', 'received', 'verified'
  screenshot_path TEXT
);

-- Expenses
CREATE TABLE expenses (
  id SERIAL PRIMARY KEY,
  expense_date DATE,
  description VARCHAR(200),
  amount DECIMAL(10,2),
  payment_status VARCHAR(20) DEFAULT 'paid',
  delivery_week_id INTEGER REFERENCES delivery_weeks(id),
  created_by INTEGER REFERENCES users(id)
);

-- Income
CREATE TABLE income (
  id SERIAL PRIMARY KEY,
  income_date DATE,
  description VARCHAR(200),
  amount DECIMAL(10,2),
  fish_profit DECIMAL(10,2),
  delivery_week_id INTEGER REFERENCES delivery_weeks(id)
);

-- Vendor Reports
CREATE TABLE vendor_reports (
  id SERIAL PRIMARY KEY,
  delivery_week_id INTEGER REFERENCES delivery_weeks(id),
  generated_at TIMESTAMP,
  generated_by INTEGER REFERENCES users(id),
  sent_at TIMESTAMP,
  report_data JSONB -- aggregated fish totals
);

-- Delivery Routes
CREATE TABLE delivery_stops (
  id SERIAL PRIMARY KEY,
  delivery_week_id INTEGER REFERENCES delivery_weeks(id),
  order_id INTEGER REFERENCES orders(id),
  stop_number INTEGER,
  route VARCHAR(50),
  driver VARCHAR(50)
);


COMPLETE MODULE SPECIFICATIONS

MODULE 1: AUTHENTICATION

	•	Session-based login with bcrypt password hashing
	•	Roles: admin, martin, danny, team
	•	Login page: clean, mobile-friendly, show company name “TAREL”
	•	Session timeout after 8 hours
	•	Login audit log

MODULE 2: DASHBOARD (Homepage after login)

Show these cards at the top:

	•	This week’s orders count
	•	Pending availability checks
	•	Unpaid invoices count
	•	Friday vendor report status (ready / not ready)

Below that show:

	•	Recent orders list (last 10)
	•	Quick action buttons: “New Order”, “Check Availability”, “Generate Vendor Report”
	•	Pending payments needing verification

MODULE 3: ORDER INTAKE (Most important module)

Page: New Order

Step 1 — Paste WhatsApp Chat:

	•	Large textarea where team pastes the raw WhatsApp message
	•	Button: “Parse Order with AI”
	•	Call Claude API (claude-sonnet-4-20250514) with this system prompt:

You are an order processing assistant for a fish and meat delivery business called TAREL.
Extract order details from this WhatsApp message and return ONLY valid JSON with no markdown.

Return this exact structure:
{
  "customer_name": "",
  "phone": "",
  "items": [
    {
      "fish_name": "",
      "quantity_kg": 0.0,
      "cut_instructions": "",
      "packing_size": ""
    }
  ],
  "delivery_instructions": "",
  "notes": ""
}

Rules:
- quantity_kg should always be a number (0.5 for half kg, 1 for 1kg, etc.)
- If cut not mentioned, use "Clean and Cut"
- Extract phone number if present in message
- fish_name should match common fish names as closely as possible


Step 2 — Review & Confirm:

	•	Show parsed results in editable form fields
	•	Customer search/autocomplete from customers table by name or phone
	•	If new customer, show “Add New Customer” form inline
	•	Fish name dropdown linked to fish_master table
	•	Quantity field with +/- buttons
	•	Add/remove item rows
	•	Auto-calculate line totals as user fills in
	•	Delivery week selector (auto-selects current open week)
	•	Driver auto-assigned based on customer area, but overridable
	•	Submit saves order with status “received”
	•	Auto-send WhatsApp message template (via Meta Cloud API):
“Hi [Name], thank you for your order! We are checking availability and will confirm shortly. - TAREL Team”

MODULE 4: ORDER PIPELINE

Page: All Orders

Kanban-style status board OR filterable table with these columns:

	•	Customer name
	•	Items ordered (summary)
	•	Total amount
	•	Driver
	•	Payment status (badge)
	•	Order status (badge)
	•	Actions

Filter by: week, driver, route, payment status, order status

Status badges:

	•	🟡 Received
	•	🔵 Availability Confirmed
	•	📄 Invoice Sent
	•	⏳ Payment Pending
	•	✅ Payment Verified
	•	🚚 Delivered

Order Detail Page (click any order):

	•	Full customer details
	•	All order items with availability status per item
	•	Invoice section
	•	Payment section
	•	Timeline of status changes

MODULE 5: AVAILABILITY CHECK

Page: Availability Check (Weekly)

Show all orders for the current week grouped by fish type.

For each fish, show:

	•	Fish name
	•	All customers who ordered it and qty
	•	Total kg needed
	•	Toggle per item: ✅ Available / ❌ Not Available

When team member marks an item:

	•	If Available → system queues WhatsApp confirmation message
	•	If Not Available → system queues WhatsApp “sorry” message

WhatsApp messages (send via Meta Cloud API):

	•	Available: “Hi [Name], great news! Your order of [fish] is confirmed. We will deliver on [delivery date]. - TAREL”
	•	Not Available: “Hi [Name], unfortunately [fish] is not available this week. We apologise for the inconvenience. - TAREL”

Button: “Send All Pending WhatsApp Messages” — sends queued messages in batch

MODULE 6: INVOICE GENERATOR

Per Order Invoice:

Auto-calculate:

For each item:
  line_total = quantity_kg × unit_price

subtotal = sum of all line_totals

freight_surcharge:
  fish_only_kg = sum of kg for items where is_fish = TRUE
  freight = fish_only_kg × 1.50

delivery_charge:
  if route == 'Inverness': delivery_charge = 13.00
  elif subtotal < 30: delivery_charge = 2.00
  else: delivery_charge = 0.00

TOTAL = subtotal + freight_surcharge + delivery_charge


Invoice PDF format (match exact style from Delivery Form sheet):

TAREL - [DELIVERY DATE] DELIVERY INVOICES

STOP [N] - [Customer Name]

CUSTOMER DETAILS
Name:              [Customer Name]
Payment Reference: [Payment Ref]
Phone:             [Phone]
Address:           [Full Address]

ORDER DETAILS
Item                          Qty    Unit Price    Price
[Fish Name]                   [qty]  [price]       [total]
Freight Surcharge (£1.5/kg)   [kg]   1.50          [total]
Delivery Charge               1      [charge]      [charge]
                                                   TOTAL: £[total]

BANK DETAILS
Name:      Daniel Maria Lazar
Sort Code: 80-48-88
Account:   13616562


Generate PDF using WeasyPrint. Store PDF path in invoices table.

Button on order detail page: “Generate & Send Invoice” → generates PDF → sends via WhatsApp

MODULE 7: CUSTOMER BOOK

Page: Customers

Table with search/filter:

	•	Name, Customer ID, Phone, Area, Postcode
	•	Click → Customer Profile page

Customer Profile page:

	•	All their personal details (editable)
	•	Full order history (all weeks)
	•	Total spent (lifetime)
	•	Outstanding balance
	•	Most ordered items
	•	Add notes

Add/Edit Customer form:

	•	Auto-generate Customer ID based on area + year + sequence
	•	Area codes: ED (Edinburgh), GL (Glasgow), LI (Livingston), BA (Bathgate), EC (East Calder), BR (Broxburn), IN (Inverness), WI (Winchburgh), AY (Ayr)

Pre-load the 264 customers from the CSV data below into the database on first run.

MODULE 8: FISH & PRICE MASTER

Page: Fish Prices

Table of all fish/products:

	•	Fish name (English + Tamil + Malayalam)
	•	Size (1kg / 500g)
	•	Avra Impex price (vendor cost)
	•	Global Food price (vendor 2 cost)
	•	Selling price
	•	Is fish? (yes/no — affects freight calculation)
	•	Active/inactive toggle

Add/Edit Fish form

Pre-load all fish from the price sheet:

fish_data = [
    {"fish_name": "(1kg) Blue Swimmer Crab", "english_name": "Blue Swimmer Crab", "tamil_name": "நீலக்கண் நண்டு", "size": "1kg", "avra_price": 27, "global_price": 12, "selling_price": 37.80, "is_fish": True},
    {"fish_name": "(1/2kg) Blue Swimmer Crab", "english_name": "Blue Swimmer Crab", "tamil_name": "நீலக்கண் நண்ட", "size": "0.5kg", "avra_price": 15, "global_price": 12, "selling_price": 21.00, "is_fish": True},
    {"fish_name": "(1kg) Indian Mackerel (Ayila)", "english_name": "Indian Mackerel", "tamil_name": "அயிலை", "size": "1kg", "avra_price": 15, "global_price": None, "selling_price": 18.00, "is_fish": True},
    {"fish_name": "(1/2kg) Indian Mackerel (Ayila)", "size": "0.5kg", "avra_price": 9, "selling_price": 10.80, "is_fish": True},
    {"fish_name": "(1kg) Sardine (Mathi)", "tamil_name": "சாளை", "size": "1kg", "avra_price": 15, "selling_price": 15.00, "is_fish": True},
    {"fish_name": "(1/2kg) Sardine (Mathi)", "size": "0.5kg", "avra_price": 9, "selling_price": 9.00, "is_fish": True},
    {"fish_name": "(1kg) Anchovy (Netholi)", "tamil_name": "நெத்தில மீன்", "size": "1kg", "avra_price": 17, "global_price": 11, "selling_price": 22.10, "is_fish": True},
    {"fish_name": "(1/2kg) Anchovy (Netholi)", "size": "0.5kg", "avra_price": 10, "global_price": 11, "selling_price": 13.00, "is_fish": True},
    {"fish_name": "(1kg) Bonito", "tamil_name": "தூனை", "size": "1kg", "avra_price": 17, "global_price": 10.75, "selling_price": 22.10, "is_fish": True},
    {"fish_name": "(1kg) Threadfin Bream (Kilimeen)", "tamil_name": "சங்கரா மன்", "size": "1kg", "avra_price": 17, "selling_price": 22.10, "is_fish": True},
    {"fish_name": "(1kg) Ponny Fish", "tamil_name": "காரா", "size": "1kg", "avra_price": 17, "selling_price": 22.10, "is_fish": True},
    {"fish_name": "(1kg) Yellow Scads", "size": "1kg", "avra_price": 17, "selling_price": 23.80, "is_fish": True},
    {"fish_name": "(1kg) Yellow Travelly/Manjal Paarai", "size": "1kg", "avra_price": 18, "selling_price": 23.40, "is_fish": True},
    {"fish_name": "(1kg) Goat Fish (Red Mullet)", "tamil_name": "நகரை", "size": "1kg", "avra_price": 18, "selling_price": 23.40, "is_fish": True},
    {"fish_name": "(1kg) Ribbon Fish (Vaala Meen)", "size": "1kg", "avra_price": 18, "selling_price": 23.40, "is_fish": True},
    {"fish_name": "(1kg) Rabbit Fish", "tamil_name": "ஒரா மன்", "size": "1kg", "avra_price": 18, "selling_price": 23.40, "is_fish": True},
    {"fish_name": "(1kg) Emperor Fish (Vilameen)", "tamil_name": "விளவன", "size": "1kg", "avra_price": 19, "selling_price": 24.70, "is_fish": True},
    {"fish_name": "(1kg) Yellowfin Tuna (Choora)", "tamil_name": "சூர மீன்", "size": "1kg", "avra_price": 19, "selling_price": 24.70, "is_fish": True},
    {"fish_name": "(1kg) King Fish (Slice)", "tamil_name": "அருக்குவா மீன்", "size": "1kg", "avra_price": 21, "selling_price": 21.00, "is_fish": True},
    {"fish_name": "(1kg) Barramundi (Kalanchi)", "tamil_name": "கொளவான்", "size": "1kg", "avra_price": 20, "global_price": 12.60, "selling_price": 26.00, "is_fish": True},
    {"fish_name": "(1kg) Travelly / Vatta", "tamil_name": "பாரை", "size": "1kg", "avra_price": 20, "selling_price": 26.00, "is_fish": True},
    {"fish_name": "(1kg) Milkshark", "tamil_name": "பால் சுற", "size": "1kg", "avra_price": 20, "selling_price": 26.00, "is_fish": True},
    {"fish_name": "(1kg) Indian Salmon", "tamil_name": "காலான்", "size": "1kg", "avra_price": 20, "selling_price": 26.00, "is_fish": True},
    {"fish_name": "(1kg) Barracuda (Seelav)", "tamil_name": "சீலா", "size": "1kg", "avra_price": 20, "global_price": 12.45, "selling_price": 26.00, "is_fish": True},
    {"fish_name": "(1kg) Black Pomfret (B. Avoli)", "tamil_name": "வாவால்", "size": "1kg", "avra_price": 22, "global_price": 13.90, "selling_price": 28.60, "is_fish": True},
    {"fish_name": "(1kg) Ladyfish", "tamil_name": "கழங்கான்", "size": "1kg", "avra_price": 22, "selling_price": 28.60, "is_fish": True},
    {"fish_name": "(1kg) Sail Fish", "tamil_name": "மயில் மன்", "size": "1kg", "avra_price": 22, "selling_price": 30.80, "is_fish": True},
    {"fish_name": "(1kg) Silver Pomfret (S. Avoli)", "tamil_name": "வெள்ளை வவால்", "size": "1kg", "avra_price": 39, "selling_price": 50.70, "is_fish": True},
    {"fish_name": "(1kg) Cuttlefish (Kanava)", "tamil_name": "கன்னவய்", "size": "1kg", "avra_price": 20, "selling_price": 28.00, "is_fish": True},
    {"fish_name": "(1kg) Squid", "tamil_name": "ஊருள கன்னவாய்", "size": "1kg", "avra_price": 24, "selling_price": 28.80, "is_fish": True},
    {"fish_name": "(1kg) White Prawn", "tamil_name": "வெள்ளை இறால்", "size": "1kg", "avra_price": 33, "selling_price": 39.60, "is_fish": True},
    {"fish_name": "(1/2kg) White Prawn", "size": "0.5kg", "avra_price": 18, "selling_price": 21.60, "is_fish": True},
    {"fish_name": "(1kg) Black Tiger Prawn", "tamil_name": "டைகர இறால்", "size": "1kg", "avra_price": 36, "selling_price": 46.80, "is_fish": True},
    {"fish_name": "(1/2kg) Black Tiger Prawn", "size": "0.5kg", "avra_price": 19, "selling_price": 24.70, "is_fish": True},
    {"fish_name": "(1kg) Kid Goat Meat", "tamil_name": "இளம் ஆட்டு இறச்சி", "size": "1kg", "avra_price": 18, "selling_price": 23.40, "is_fish": False},
    {"fish_name": "(1kg) Goat Meat With Bone", "tamil_name": "ஆட்டு இறைச்சி", "size": "1kg", "avra_price": 15, "selling_price": 19.50, "is_fish": False},
    {"fish_name": "(1kg) Goat Meat without Bone", "size": "1kg", "avra_price": 21, "selling_price": 27.30, "is_fish": False},
    {"fish_name": "(1/2kg) Goat Meat without Bone", "size": "0.5kg", "avra_price": 12, "selling_price": 15.60, "is_fish": False},
    {"fish_name": "(1kg) Goat Liver+Heart", "size": "1kg", "avra_price": 6, "selling_price": 8.40, "is_fish": False},
    {"fish_name": "Lamb Diced on Bone", "size": "1kg", "avra_price": 16, "selling_price": None, "is_fish": False},
]


MODULE 9: WEEKLY AVAILABILITY BOARD (Order Form Sheet)

Page: This Week’s Orders

Show a table like the Excel Order Form:

	•	Rows = each fish type
	•	Columns = kg ordered, packs, available qty
	•	Team enters available qty per fish
	•	Color: green if available ≥ ordered, red if shortfall

Auto-populate from all confirmed orders for the week.

MODULE 10: VENDOR REPORT

Page: Vendor Report

Generated every Friday for current week’s orders.

Report shows:

TAREL VENDOR REPORT — Week of [date] to [date]
Delivery Date: [Wednesday date]

FISH ORDERS:
Fish Name              | Total Kg | Orders | Customers
(1kg) King Fish        | 15.00    | 8      | [names]
(1kg) Blue Swimmer Crab| 12.50    | 6      | [names]
...

MEAT ORDERS:
Kid Goat Meat          | 22.00    | 12     | [names]
...

GRAND TOTAL: [X]kg fish + [Y]kg meat


Button: “Download as PDF” — generates PDF
Button: “Mark as Sent to Vendor” — updates status

MODULE 11: DELIVERY ROUTES

Page: Delivery Routes

Two tabs: Martin’s Route | Danny’s Route

For each stop show:

	•	Stop number (draggable to reorder)
	•	Customer name + address + postcode
	•	Items ordered (summary)
	•	Invoice total
	•	Payment status badge

Print-friendly view for driver to take on delivery day.

Also show Inverness route separately if any Inverness orders that week.

MODULE 12: FINANCE & EXPENSES

Page: Finance

Two sections:

Expenses tab:

	•	Add expense: date, description, amount, paid/unpaid
	•	Categories: Petrol, Food, Fish Purchase, Meat Purchase, Car Rental, Other
	•	List all expenses for selected week

Income tab:

	•	Auto-populated from verified payments
	•	Show total income per week

P&L Summary:

Week: [date range]
Total Income:    £[X]
Total Expenses:  £[Y]
Fish Profit:     £[Z]
─────────────────────
Martin (50%):    £[A]
Danny (40%):     £[B]
Ministry (10%):  £[C]


Monthly summary view with all weeks.

MODULE 13: WHATSAPP INTEGRATION

Use Meta Cloud API (WhatsApp Business API).

Config stored in environment variables:

WHATSAPP_TOKEN=
WHATSAPP_PHONE_ID=
WHATSAPP_VERIFY_TOKEN=


Outgoing messages (send these automatically):

	1.	Order received acknowledgement (sent immediately on order creation)
	2.	Availability confirmed (sent after team marks available)
	3.	Availability not available (sent after team marks not available)
	4.	Invoice (PDF attachment via WhatsApp)
	5.	Payment confirmation (after team verifies payment)

Incoming webhook:

	•	Receive WhatsApp messages at /webhook/whatsapp
	•	Log incoming messages to a whatsapp_messages table
	•	Show unread incoming messages in dashboard

If Meta API not configured, fall back to showing a “Send manually” button that copies the message text to clipboard.

MODULE 14: SETTINGS

Page: Settings (Admin only)

	•	Team members management (add/edit/remove users)
	•	Bank details (editable — currently Daniel Maria Lazar / 80-48-88 / 13616562)
	•	Delivery charge settings (freight rate, small order threshold, Inverness rate)
	•	Profit split percentages (Martin/Danny/Ministry)
	•	WhatsApp API credentials
	•	Current delivery week management (open/close weeks)

FILE STRUCTURE

tarel/
├── app.py                  # Main Flask app, all routes
├── config.py               # Config, env vars
├── models.py               # SQLAlchemy models
├── db.py                   # DB connection
├── requirements.txt
├── .env
├── templates/
│   ├── base.html           # Base layout with nav
│   ├── login.html
│   ├── dashboard.html
│   ├── orders/
│   │   ├── list.html
│   │   ├── new.html
│   │   ├── detail.html
│   ├── customers/
│   │   ├── list.html
│   │   ├── profile.html
│   ├── availability.html
│   ├── invoice.html
│   ├── vendor_report.html
│   ├── delivery_routes.html
│   ├── finance.html
│   ├── fish_master.html
│   ├── settings.html
├── static/
│   ├── css/
│   │   └── style.css       # Mobile-first CSS
│   ├── js/
│   │   └── app.js
├── services/
│   ├── whatsapp.py         # Meta API integration
│   ├── ai_parser.py        # Claude API order parsing
│   ├── invoice_pdf.py      # WeasyPrint PDF generation
│   ├── vendor_report.py    # Report generation
└── seed_data.py            # Pre-load customers + fish prices


UI/UX REQUIREMENTS

	•	Mobile-first design (team uses phones)
	•	Color scheme: deep navy (#1a2744) + gold (#f0a500) — professional fish business feel
	•	Large touch targets (minimum 44px buttons)
	•	Status badges with clear colors (yellow=pending, blue=confirmed, green=paid, red=issue)
	•	Bottom navigation bar on mobile: Orders | Customers | Availability | Finance
	•	Toast notifications for all actions
	•	Confirm dialogs before destructive actions
	•	Loading states on all API calls
	•	Offline-friendly: show cached data if connection drops

ENVIRONMENT VARIABLES NEEDED

DATABASE_URL=postgresql://user:pass@localhost/tarel
SECRET_KEY=your-secret-key
ANTHROPIC_API_KEY=your-key
WHATSAPP_TOKEN=
WHATSAPP_PHONE_ID=
WHATSAPP_VERIFY_TOKEN=


SEED DATA

On first run (python seed_data.py), insert:

	1.	Default admin user: username=admin, password=tarel2026
	2.	All 40 fish/products from the price list above
	3.	All 264 customers from the customer database (provide as CSV import)
	4.	Current open delivery week

WHAT TO BUILD FIRST (Priority Order)

	1.	Database setup + models
	2.	Authentication (login/logout)
	3.	Customer Book (pre-load data)
	4.	Fish Master (pre-load prices)
	5.	New Order form with AI parsing
	6.	Order Pipeline view
	7.	Availability Check module
	8.	Invoice Generator + PDF
	9.	Vendor Report
	10.	Delivery Routes
	11.	Finance/Expenses
	12.	WhatsApp Integration
	13.	Settings page

Build this as a complete, production-ready Flask application. Every module should be fully functional. Use SQLAlchemy ORM. All forms should have validation. All tables should be searchable and filterable. The app should work perfectly on mobile browsers.

That’s your full prompt. Hand this to Claude and it will build the entire system module by module. If it hits context limits, tell it to continue from whichever module it stopped at — the prompt is structured so each module is Here’s your complete prompt to give to Claude:

TAREL FISH DELIVERY — COMPLETE INTERNAL MANAGEMENT SYSTEM

PROJECT OVERVIEW

Build a complete internal web application for a fish and meat delivery business operating in Scotland (Edinburgh, Glasgow, Livingston, Bathgate, Inverness routes). The team receives orders via WhatsApp, processes them manually, generates invoices, and delivers weekly. This app replaces their entire Excel workflow.

Tech Stack: Flask + PostgreSQL + HTML/CSS/JS (mobile-first, no React framework needed)

BUSINESS RULES (CRITICAL — embed these everywhere)

	•	Freight surcharge: £1.50 per kg (fish only, NOT meat/goat products)
	•	Small order charge: £2.00 extra if order total is under £30
	•	Inverness delivery charge: £13.00 flat
	•	Profit split: Martin 50% / Danny 40% / Ministry 10%
	•	Two vendors: Avra Impex (primary) and Global Food (secondary)
	•	Two drivers: Martin (Edinburgh/Livingston/Bathgate routes) and Danny (Glasgow route)
	•	Delivery cycle: Orders taken Monday–Friday, delivered following Wednesday
	•	Customer ID format: AreaCode + Year + Number (e.g. ED26105, GL26052, BA26113)
	•	Payment reference format: AreaCode + Year + Number (e.g. EH26210, IN26030)
	•	Bank details on every invoice: Daniel Maria Lazar / Sort: 80-48-88 / Account: 13616562
	•	Pricing: each fish has a 1kg price AND a half kg price (half kg costs more per kg as a markup strategy)
	•	Price calculation: 2kg = 1kg + 1kg price; 1.5kg = 1kg price + half kg price

DATABASE SCHEMA

-- Users (internal team)
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  username VARCHAR(50) UNIQUE,
  password_hash VARCHAR(255),
  role VARCHAR(20), -- 'admin', 'martin', 'danny', 'team'
  created_at TIMESTAMP DEFAULT NOW()
);

-- Customers
CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  customer_id VARCHAR(20) UNIQUE, -- e.g. ED26105
  name VARCHAR(150),
  phone VARCHAR(30),
  address TEXT,
  area VARCHAR(100),
  postcode VARCHAR(15),
  notes TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Fish/Product Master
CREATE TABLE fish_master (
  id SERIAL PRIMARY KEY,
  fish_name VARCHAR(200), -- full name e.g. "(1kg) King Fish (Slice)"
  english_name VARCHAR(150),
  tamil_name VARCHAR(150),
  malayalam_name VARCHAR(150),
  size VARCHAR(10), -- '1kg' or '0.5kg'
  avra_impex_price DECIMAL(10,2), -- vendor cost
  global_food_price DECIMAL(10,2), -- vendor 2 cost
  selling_price DECIMAL(10,2), -- customer price
  cut_type VARCHAR(100), -- e.g. "Steak", "Clean and Cut"
  is_fish BOOLEAN DEFAULT TRUE, -- FALSE for goat/meat products
  is_active BOOLEAN DEFAULT TRUE
);

-- Delivery Weeks
CREATE TABLE delivery_weeks (
  id SERIAL PRIMARY KEY,
  week_start DATE,
  week_end DATE,
  delivery_date DATE, -- the Wednesday
  status VARCHAR(20) DEFAULT 'open', -- 'open', 'vendor_report_sent', 'delivered', 'closed'
  created_at TIMESTAMP DEFAULT NOW()
);

-- Orders (one per customer per week)
CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  customer_id INTEGER REFERENCES customers(id),
  delivery_week_id INTEGER REFERENCES delivery_weeks(id),
  payment_reference VARCHAR(30),
  order_date DATE,
  delivery_date DATE,
  driver VARCHAR(50), -- 'Martin' or 'Danny'
  route VARCHAR(50), -- 'Edinburgh', 'Glasgow', 'Inverness', 'Livingston', 'Bathgate'
  delivery_stop_number INTEGER,
  status VARCHAR(30) DEFAULT 'received', 
  -- statuses: received, availability_confirmed, invoice_sent, payment_pending, payment_received, payment_verified, delivered
  delivery_instructions TEXT,
  order_platform VARCHAR(50) DEFAULT 'WhatsApp',
  raw_whatsapp_text TEXT, -- original message pasted by team
  created_by INTEGER REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW()
);

-- Order Items (one row per fish per order)
CREATE TABLE order_items (
  id SERIAL PRIMARY KEY,
  order_id INTEGER REFERENCES orders(id),
  fish_master_id INTEGER REFERENCES fish_master(id),
  fish_name VARCHAR(200), -- stored at time of order
  quantity_kg DECIMAL(10,3),
  unit_price DECIMAL(10,2),
  line_total DECIMAL(10,2),
  cut_instructions TEXT,
  availability_status VARCHAR(20) DEFAULT 'pending', -- 'pending', 'available', 'not_available'
  availability_checked_by INTEGER REFERENCES users(id),
  availability_checked_at TIMESTAMP
);

-- Invoices
CREATE TABLE invoices (
  id SERIAL PRIMARY KEY,
  order_id INTEGER REFERENCES orders(id),
  invoice_number VARCHAR(30),
  subtotal DECIMAL(10,2),
  freight_surcharge DECIMAL(10,2),
  delivery_charge DECIMAL(10,2),
  total DECIMAL(10,2),
  generated_at TIMESTAMP,
  sent_at TIMESTAMP,
  sent_by INTEGER REFERENCES users(id)
);

-- Payments
CREATE TABLE payments (
  id SERIAL PRIMARY KEY,
  order_id INTEGER REFERENCES orders(id),
  invoice_id INTEGER REFERENCES invoices(id),
  amount DECIMAL(10,2),
  payment_mode VARCHAR(50), -- 'Bank Transfer', 'Cash', 'UPI'
  payment_name VARCHAR(150), -- name used on bank transfer
  payment_received_date DATE,
  payment_verified_by INTEGER REFERENCES users(id),
  payment_verified_at TIMESTAMP,
  status VARCHAR(20) DEFAULT 'pending', -- 'pending', 'received', 'verified'
  screenshot_path TEXT
);

-- Expenses
CREATE TABLE expenses (
  id SERIAL PRIMARY KEY,
  expense_date DATE,
  description VARCHAR(200),
  amount DECIMAL(10,2),
  payment_status VARCHAR(20) DEFAULT 'paid',
  delivery_week_id INTEGER REFERENCES delivery_weeks(id),
  created_by INTEGER REFERENCES users(id)
);

-- Income
CREATE TABLE income (
  id SERIAL PRIMARY KEY,
  income_date DATE,
  description VARCHAR(200),
  amount DECIMAL(10,2),
  fish_profit DECIMAL(10,2),
  delivery_week_id INTEGER REFERENCES delivery_weeks(id)
);

-- Vendor Reports
CREATE TABLE vendor_reports (
  id SERIAL PRIMARY KEY,
  delivery_week_id INTEGER REFERENCES delivery_weeks(id),
  generated_at TIMESTAMP,
  generated_by INTEGER REFERENCES users(id),
  sent_at TIMESTAMP,
  report_data JSONB -- aggregated fish totals
);

-- Delivery Routes
CREATE TABLE delivery_stops (
  id SERIAL PRIMARY KEY,
  delivery_week_id INTEGER REFERENCES delivery_weeks(id),
  order_id INTEGER REFERENCES orders(id),
  stop_number INTEGER,
  route VARCHAR(50),
  driver VARCHAR(50)
);


COMPLETE MODULE SPECIFICATIONS

MODULE 1: AUTHENTICATION

	•	Session-based login with bcrypt password hashing
	•	Roles: admin, martin, danny, team
	•	Login page: clean, mobile-friendly, show company name “TAREL”
	•	Session timeout after 8 hours
	•	Login audit log

MODULE 2: DASHBOARD (Homepage after login)

Show these cards at the top:

	•	This week’s orders count
	•	Pending availability checks
	•	Unpaid invoices count
	•	Friday vendor report status (ready / not ready)

Below that show:

	•	Recent orders list (last 10)
	•	Quick action buttons: “New Order”, “Check Availability”, “Generate Vendor Report”
	•	Pending payments needing verification

MODULE 3: ORDER INTAKE (Most important module)

Page: New Order

Step 1 — Paste WhatsApp Chat:

	•	Large textarea where team pastes the raw WhatsApp message
	•	Button: “Parse Order with AI”
	•	Call Claude API (claude-sonnet-4-20250514) with this system prompt:

You are an order processing assistant for a fish and meat delivery business called TAREL.
Extract order details from this WhatsApp message and return ONLY valid JSON with no markdown.

Return this exact structure:
{
  "customer_name": "",
  "phone": "",
  "items": [
    {











































# TAREL — MINI ORDER PAGE + AI CUSTOMER ORDERING SYSTEM

## IMPORTANT — READ FIRST

I have provided the existing Tarel website project.

**DO NOT replace, redesign, or damage the existing Tarel website.**

Use the existing project as the visual and branding source of truth.

The existing project currently contains:

* `index.html`
* `styles.css`
* `script.js`
* `assets/logo.jpg`
* `assets/logo-transparent.png`
* `assets/logo-cream.png`
* `assets/favicon.png`
* Existing seafood/meat images
* Existing Tarel WhatsApp functionality
* Existing Tarel colours, typography, buttons, spacing and responsive design

The current website is a static HTML/CSS/JavaScript project.

The existing Tarel branding must remain exactly consistent.

---

# OBJECTIVE

Build a complete **Tarel Mini Order Page** that works as a customer-facing ordering experience accessed from WhatsApp.

The final concept is:

**Tarel Mini Order Page = Normal Shopping + AI Built Into The Experience**

The customer should be able to:

1. Open an order link from WhatsApp

2. Be identified by mobile number / customer ID

3. See their name and initial

4. Browse Tarel products

5. Search products normally

6. Use AI-powered natural-language search

7. Ask AI what fish/product is suitable for a dish

8. Ask AI to build an order

9. Set a budget

10. Calculate portions

11. Reorder previous purchases

12. Receive personalised recommendations

13. Add AI recommendations directly to cart

14. Adjust quantity

15. Select weight

16. Select cut/preparation

17. See live cart totals

18. Apply discounts

19. Apply freight surcharge rules

20. Choose delivery or collection\

21. Add order notes

22. Review the final order

23. Place the order

24. Receive an Order ID

25. See the order as `Pending Confirmation`

On the admin side, the same order must appear under:

**Received Order**

Admin can:

* Review
* Confirm
* Reject

When confirmed, the SAME order must move into the existing:

**Order Management**

Do NOT create duplicate orders.

---

# VERY IMPORTANT ARCHITECTURE RULE

Do NOT call AI for every customer action.

Normal ecommerce functionality must remain normal application logic.

## NO AI required for:

* Product listing
* Product images
* Product prices
* Product availability
* Stock
* Weight selection
* Cut selection
* Quantity
* Cart
* Discount calculation
* Freight surcharge
* Delivery charge
* Delivery date
* Checkout
* Order creation
* Order status
* Customer lookup
* Final price calculation

These must be handled by normal backend/application logic.

## AI is ONLY used for:

* Natural-language product search
* AI Fish Finder
* Meal/cooking recommendations
* Build My Order
* Budget-based ordering
* Portion recommendations
* Personalised recommendations
* Understanding customer intent
* Reorder recommendations
* Conversational shopping assistance

AI must NEVER invent:

* Products
* Prices
* Stock
* Discounts
* Delivery charges
* Freight charges
* Final order totals

The database/backend is always the source of truth.

---

# DO NOT USE META WHATSAPP API FOR THIS MVP

The current implementation should NOT require:

* Meta Business API
* WhatsApp Cloud API
* WABA
* Meta access tokens
* WhatsApp webhooks
* WhatsApp Flows

For this MVP, WhatsApp is simply the channel where we send the customer the Tarel Mini Order Page link.

Example:

`https://tarel.co.uk/order/fresh-catch`

For local development, use:

`http://localhost:<port>/order/fresh-catch`

The existing WhatsApp buttons should be updated so they can open the Mini Order Page instead of directly creating a WhatsApp order message where appropriate.

Keep the existing WhatsApp number/functionality available for customer support.

---

# DO NOT DEPLOY

This task is DEVELOPMENT ONLY.

Do NOT:

* push to GitHub
* commit changes
* deploy to Vercel
* deploy to Netlify
* deploy to Render
* deploy anywhere
* publish anything
* modify production
* require external production services

Everything must run locally.

The goal is to test the COMPLETE customer + order + admin flow locally.

---

# FIRST STEP — INSPECT THE EXISTING PROJECT

Before modifying anything:

1. Inspect every existing HTML/CSS/JS file.
2. Inspect the existing assets.
3. Identify the exact Tarel logo being used.
4. Identify existing colours.
5. Identify typography.
6. Identify button styles.
7. Identify cards.
8. Identify responsive breakpoints.
9. Identify existing WhatsApp functionality.
10. Identify existing product information.
11. Reuse as much existing code/assets/styles as practical.

Do NOT create a completely different visual system.

---

# BRANDING

Use the existing Tarel branding.

Existing palette:

Primary:
`#2E4237`

Secondary:
`#708E52`

Background:
`#EAE2D7`

Accent:
`#C9A24B`

Existing typography:

* Fraunces
* Manrope

Use the existing Tarel logo:

`assets/logo-transparent.png`

Use the existing favicon:

`assets/favicon.png`

Use existing product images wherever possible.

DO NOT create a new logo.

DO NOT replace the existing brand colours.

DO NOT introduce a generic ecommerce template.

The Mini Order Page must look like a natural extension of Tarel.

---

# CUSTOMER URL STRUCTURE

Create a route/page similar to:

`/order/fresh-catch`

For development:

`http://localhost:8080/order/fresh-catch`

The system should support future campaign URLs such as:

`/order/fresh-friday`

`/order/weekend-special`

`/order/seafood-box`

Create the structure so that campaign-specific product lists can be added later.

---

# CUSTOMER EXPERIENCE

## SCREEN 1 — CUSTOMER IDENTIFICATION

When opening:

`/order/fresh-catch`

Show:

Tarel logo

Welcome to Tarel

Ask for:

**Mobile Number**

OR

**Customer ID**

For existing customers, simulate lookup using local development data.

If customer is found:

Show:

**J**

**Welcome back, Jebastin**

`Customer ID: TAR1234`

The initial should be generated automatically from the customer name.

Do NOT make the customer enter their name every time if the customer already exists.

If the customer is new:

Allow:

* Name
* Mobile
* Address

Then create a local development customer record.

---

# CUSTOMER PROFILE

Create mock/local customer data for development.

Example customers:

### Customer 1

Name:
Jebastin P

Customer ID:
TAR1234

Phone:
+44 7553 132674

Favourite products:

* Salmon
* Tiger Prawns

Frequent categories:

* Fish
* Prawns

Preferred preparation:

* Fillet
* Curry Cut

Average order value:
£42

### Customer 2

Name:
Priya S

Customer ID:
TAR1240

Favourite products:

* King Fish
* Squid

### Customer 3

Name:
Arun Kumar

Customer ID:
TAR1255

Favourite products:

* Prawns
* Crab

Use this data to demonstrate that recommendations differ between customers.

---

# MAIN MINI ORDER PAGE

The main page should have:

## HEADER

Use the existing Tarel header style.

Show:

Tarel logo

Cart icon

Customer avatar/initial

Customer name

---

# PERSONALIZED CUSTOMER AREA

Example:

**J**

**Welcome back, Jebastin**

`Customer ID: TAR1234`

Then:

### Your usual

Show the customer's frequently ordered products.

Example:

* Salmon
* Tiger Prawns

Provide:

`+ Add`

or:

`Reorder`

---

# AI AREA

Do NOT make the AI dominate the screen.

Create one elegant Tarel-branded section:

## ✨ Ask Tarel

Subtitle:

**What are you looking for today?**

Input:

`Tell me what you want...`

Include search/submit button.

Under it show quick actions:

* 🐟 Find Fish
* 🍛 What should I cook?
* ✨ Build My Order
* 💰 Under £30
* 👨‍👩‍👧 For My Family
* 🔄 Order Again

This should look like part of the Tarel interface, not a separate chatbot.

---

# AI FEATURE 1 — AI FISH FINDER

Customer can type:

“I need boneless fish for frying.”

The AI should understand:

```text
Category = Fish
Preparation = Boneless
Cooking = Frying
```

Then query/filter REAL available Tarel products.

Display:

### Tarel recommends

Product image

Salmon Fillet

Boneless

£14/kg

Button:

`Add to Cart`

Also show alternative:

King Fish Steak

Button:

`Add to Cart`

The AI must use product IDs internally.

Do not add product names directly to the cart without validating them against the product database.

---

# AI FEATURE 2 — NATURAL LANGUAGE PRODUCT SEARCH

Customer can type:

“Show me fish under £15 suitable for curry.”

Convert the request into structured filters.

Example:

```json
{
  "category": "fish",
  "max_price": 15,
  "preparation": "curry"
}
```

Then query actual Tarel products.

Display matching products.

Do NOT use AI to invent the result.

---

# AI FEATURE 3 — WHAT SHOULD I COOK?

Customer:

“I am cooking fish curry for 5 people.”

AI should understand:

* Dish: Fish curry
* People: 5

Then query available products.

Recommendation:

King Fish

Curry Cut

Approximately 1.5kg

£24

Button:

`Add 1.5kg to Cart`

Also show optional complementary products if available.

---

# AI FEATURE 4 — BUILD MY ORDER

Customer selects:

**Build My Order**

AI asks:

1. How many people?
2. What do you want?
3. What's your budget?

Example:

4 people

Fish + Prawns

£40

Then produce a proposed basket.

Example:

King Fish — 1kg — £16

Tiger Prawns — 500g — £18

Squid — 250g — £6

Total:

£40

Button:

`Add All to Cart`

IMPORTANT:

The backend must validate every item and recalculate the actual total before adding/checkout.

---

# AI FEATURE 5 — BUDGET ORDERING

Customer:

“I have £30.”

AI searches available products and recommends a combination within the budget.

The final cart must be calculated by the backend.

AI cannot override product prices.

---

# AI FEATURE 6 — PORTION CALCULATOR

Customer:

“How much fish do I need for 8 people?”

AI can recommend:

Approximately 1.5–2.5kg depending on dish/type.

Then:

`Add Recommended Quantity`

Use deterministic rules where appropriate.

Do not unnecessarily call an LLM for simple arithmetic.

---

# AI FEATURE 7 — ORDER AGAIN

Show:

## 🔄 Order Your Usual

Use customer order history.

Example:

Last order:

Salmon — 1kg

Tiger Prawns — 500g

Blue Crab — 500g

Button:

`Reorder Everything`

The system should add the current equivalent products to the cart using CURRENT prices.

Do not reuse old prices.

---

# PERSONALISATION ENGINE

Each customer must have personalised recommendations.

Do NOT rely on AI for basic recommendation calculations.

Use customer history.

Track:

* purchase count
* last purchased
* favourite products
* favourite categories
* preferred cut
* preferred weight
* average order value
* recent orders
* frequently purchased products

Calculate a recommendation score.

Example:

```text
product_affinity_score =
purchase_frequency
+ recency
+ category_preference
+ repeat_purchase_signal
```

Then show:

### Picked for you

Different customers must see different recommendations.

---

# PRODUCT DATA

Create local development product data.

Include at least:

### Salmon Fillet

Category:
Fish

Price:
£14/kg

Weights:
500g, 1kg

Cuts:
Fillet

### King Fish

Category:
Fish

Price:
£16/kg

Weights:
500g, 1kg, 1.5kg, 2kg

Cuts:
Steak, Curry Cut

### Tiger Prawns

Category:
Prawns

Price:
£18/500g

Weights:
250g, 500g, 1kg

### Blue Crab

Category:
Crab

Price:
£12/500g

Weights:
500g, 1kg

### Squid

Category:
Squid

Price:
£6/500g

Weights:
250g, 500g, 1kg

Use existing Tarel images where available.

If existing images don't match these exact products, use the closest available assets and make the data clearly replaceable later.

---

# PRODUCT CARD

Use the existing Tarel visual language.

Each card should contain:

* Image
* Product name
* Price
* Weight selector
* Cut/preparation selector where applicable
* Quantity
* Add button

Example:

```text
Salmon Fillet

[ IMAGE ]

£14 / kg

Weight
[ 1kg ▼ ]

Preparation
[ Fillet ▼ ]

[-] 1 [+]

[ ADD ]
```

---

# CATEGORIES

Use:

All

Fish

Prawns

Crab

Squid

Meat

Special Offers

The category UI should match the existing Tarel style.

---

# NORMAL SEARCH

Provide normal search:

`Search fish, seafood or meat...`

This should work WITHOUT AI.

If the user types a simple product name:

`Salmon`

normal search should handle it.

AI is only needed for natural-language intent.

---

# CART

Create a real local development cart.

Cart must support:

* Add
* Remove
* Increase quantity
* Decrease quantity
* Change weight
* Change preparation
* Clear item

Sticky bottom cart on mobile:

`🛒 4 Items   £50.50   VIEW CART`

---

# PRICING ENGINE

Create a central pricing calculation function.

Do NOT calculate totals independently in multiple components.

Example:

```text
subtotal
- discount
+ freight surcharge
+ delivery charge
= total
```

Use current database/product values.

---

# DISCOUNT

Support local development discount:

Example:

`FRESH10`

10% discount.

Make the discount system replaceable with the real Tarel discount engine later.

---

# FREIGHT SURCHARGE

Use the Tarel business rule:

If the applicable order value requires the surcharge:

`£1.50`

Show:

Freight Surcharge: £1.50

If not applicable:

Freight Surcharge: £0.00

The backend/pricing engine is the source of truth.

---

# DELIVERY

Allow:

### Home Delivery

Show saved address.

### Collect From Us

No delivery charge.

Allow customer to change address.

---

# DELIVERY DATE

Create development delivery dates.

Example:

Friday

Saturday

Sunday

Only show available dates.

Make the data structure ready for future delivery-slot rules.

---

# ORDER NOTES

Allow:

`Any special preparation instructions?`

Example:

“Please cut into curry pieces.”

---

# FINAL CHECKOUT

Show:

Customer:

Jebastin P

Customer ID:

TAR1234

Phone:

+44 XXXXX XXXXX

Delivery:

Home Delivery

Address:

Saved address

Delivery Date:

Friday

Items:

All cart items

Pricing:

Subtotal

Discount

Freight Surcharge

Delivery Charge

TOTAL

Button:

## PLACE ORDER

---

# ORDER CREATION

When customer presses PLACE ORDER:

Create ONE order record.

Example:

```text
Order ID: TR-10482
Customer ID: TAR1234
Customer Name: Jebastin P
Source: WHATSAPP
Status: PENDING_CONFIRMATION
Payment Status: PENDING
```

Create associated order items.

Do NOT create separate customer and admin orders.

The customer view and admin view must reference the SAME order.

---

# CUSTOMER SUCCESS SCREEN

After placing:

## 🎉 Order Received!

Thank you, Jebastin.

Your order has been received.

Order ID:

**TR-10482**

Status:

🟡 Pending Confirmation

Message:

“Our team will review your order and confirm it shortly.”

Button:

`View My Order`

Button:

`Chat with Tarel on WhatsApp`

The WhatsApp button can use the existing Tarel WhatsApp number.

---

# CUSTOMER ORDER TRACKING

Create:

`/order/TR-10482`

Show:

### Order #TR-10482

✓ Order Received

🟡 Pending Confirmation

○ Confirmed

○ Preparing

○ Ready

○ Out for Delivery

○ Delivered

The status should come from the same order record.

---

# ADMIN SIDE

Create an admin development page.

Example:

`/admin/received-orders`

Use the SAME Tarel design language.

Do not create a generic dashboard.

---

# RECEIVED ORDERS

Add a menu item:

**📨 Received Orders**

Show:

* Order ID
* Customer
* Customer ID
* Phone
* Items
* Total
* Order date
* Source
* Status
* Action

Example:

```text
TR-10482
Jebastin P
TAR1234
4 Items
£50.50
WHATSAPP
Pending Confirmation
[Review]
```

---

# ORDER REVIEW

When admin clicks Review:

Show:

Customer details

Order items

Product images

Quantities

Weights

Cuts

Notes

Delivery method

Address

Delivery date

Subtotal

Discount

Freight

Delivery charge

Total

Buttons:

## Confirm Order

## Reject Order

---

# CONFIRMATION LOGIC

When admin clicks:

**Confirm Order**

Do NOT create another order.

Change:

```text
PENDING_CONFIRMATION
```

to:

```text
CONFIRMED
```

Then the order becomes visible in:

**Order Management**

---

# REJECTION LOGIC

If admin rejects:

Change status:

```text
REJECTED
```

Ask for optional rejection reason.

Example:

“Product unavailable.”

Store the rejection reason with the same order.

---

# ORDER MANAGEMENT

Create/extend:

`/admin/orders`

Show confirmed orders.

Statuses:

* Confirmed
* Preparing
* Ready
* Out for Delivery
* Delivered
* Cancelled

Allow admin to update status.

---

# ORDER STATUS FLOW

```text
Pending Confirmation
        ↓
Confirmed
        ↓
Preparing
        ↓
Ready
        ↓
Out for Delivery
        ↓
Delivered
```

---

# DATA MODEL

For local development, create a simple data layer.

Prefer a lightweight local backend if necessary.

Use a structure that can later be replaced with the real Tarel FastAPI/PostgreSQL backend.

Suggested entities:

```text
customers
products
product_variants
orders
order_items
delivery_addresses
customer_preferences
customer_product_affinity
order_history
quick_order_campaigns
quick_order_campaign_products
```

---

# QUICK ORDER CAMPAIGNS

Support campaign URLs.

Example:

`/order/fresh-catch`

Campaign:

Fresh Catch

Products:

Salmon

King Fish

Tiger Prawns

Blue Crab

Squid

Future campaigns:

`/order/fresh-friday`

`/order/weekend-special`

`/order/seafood-box`

The Mini Order Page should use the campaign to determine which products are displayed.

---

# AI ARCHITECTURE

Do NOT create one giant AI agent.

Use focused AI capabilities/agents.

## Agent 1 — Product Finder Agent

Input:

Natural-language request.

Output:

Structured product filters.

Example:

```json
{
  "category": "fish",
  "preparation": "boneless",
  "cooking_method": "frying",
  "max_price": 15
}
```

---

## Agent 2 — Meal Recommendation Agent

Input:

Dish + people + preferences.

Output:

Recommended product IDs and quantities.

---

## Agent 3 — Order Builder Agent

Input:

People + categories + budget.

Output:

Proposed product IDs and quantities.

---

## Agent 4 — Customer Recommendation Engine

Primarily rules/data driven.

Uses:

* order history
* frequency
* recency
* categories
* product affinity
* current availability

Use AI only when natural-language reasoning adds value.

---

# AI SAFETY / DATA RULE

AI must never directly write arbitrary products/prices into the order.

AI returns product IDs.

Backend validates:

```text
product exists
product is active
product is available
weight is valid
cut is valid
current price is fetched
stock is sufficient
```

Then backend adds to cart.

---

# AI UI

The AI should be integrated into the Mini Order Page.

Do NOT make it look like ChatGPT.

Use Tarel branding.

Keep it lightweight.

Example:

```text
✨ Ask Tarel

What are you looking for today?

[ Fish for 5 people under £30 ]

[🐟 Find Fish]
[🍛 What should I cook?]
[✨ Build My Order]
[💰 Under £30]
[🔄 Order Again]
```

AI responses should be concise and action-oriented.

Always provide product/action buttons where appropriate.

---

# RESPONSIVE DESIGN

The customer page is primarily mobile-first because the link will be opened from WhatsApp.

Must work properly on:

* iPhone
* Android
* tablet
* desktop

On mobile:

* Sticky cart
* Large touch targets
* Simple cards
* Minimal typing
* Fast loading
* Easy scrolling

Do not overcrowd the screen.

---

# VISUAL DIRECTION

Use the existing Tarel design.

Do NOT copy the generated mockup literally.

Use it only as UX inspiration.

The actual implementation must match the existing Tarel website.

Use:

* Existing logo
* Existing colours
* Existing fonts
* Existing border radius
* Existing buttons
* Existing shadows
* Existing spacing
* Existing imagery
* Existing responsive behaviour

The customer should feel:

“This is Tarel.”

Not:

“This is a separate ecommerce website.”

---

# LOCAL DEVELOPMENT

Everything must run locally.

Create a clear development command.

For example:

```bash
./run
```

or the appropriate command for the chosen implementation.

If adding a backend:

Run frontend and backend locally.

Example:

```text
Frontend:
http://localhost:3000

Backend:
http://localhost:8000
```

Do not require production credentials.

Use mock/local data.

---

# DEVELOPMENT MODE

Create clearly separated development/mock data.

The app should be usable immediately after starting locally.

No external database should be required for the initial demo.

If a database is introduced, provide an easy local setup.

---

# COMPLETE TEST FLOW

The final implementation MUST allow me to test this exact flow locally:

## CUSTOMER

1. Open `/order/fresh-catch`
2. Enter `TAR1234`
3. See:

“Welcome back, Jebastin”

4. See personalised recommendations
5. Search normally for Salmon
6. Add Salmon
7. Change weight
8. Change preparation
9. Add another product
10. Ask:

“I need fish for 5 people for curry”

11. Receive AI recommendation
12. Add recommendation to cart
13. Click Build My Order
14. Build a budget order
15. Test portion calculator
16. Test Order Again
17. Open cart
18. Apply discount
19. Check freight surcharge
20. Select delivery
21. Select date
22. Add notes
23. Review order
24. Place order
25. Receive Order ID
26. Open customer order tracking

## ADMIN

27. Open `/admin/received-orders`
28. See the SAME Order ID
29. Review customer
30. Review items
31. Review price
32. Review delivery
33. Review notes
34. Click Confirm Order
35. Verify status changes to Confirmed
36. Open Order Management
37. Verify SAME Order ID is there
38. Change status to Preparing
39. Change status to Ready
40. Change status to Out for Delivery
41. Change status to Delivered
42. Return to customer order page
43. Verify customer sees the updated status

---

# DEMO DATA

Create enough sample products and customers to make the UI feel realistic.

At minimum:

5–10 seafood products.

3 customers.

5–10 sample historical orders.

Different preferences for each customer.

Use realistic GBP prices.

---

# ERROR HANDLING

Handle:

* Product unavailable
* Invalid customer ID
* Empty cart
* Invalid quantity
* Invalid weight
* Invalid cut
* Delivery date unavailable
* Product removed while ordering
* AI recommendation unavailable
* Backend error

Never allow checkout with invalid products.

---

# PERFORMANCE

Do not make unnecessary AI calls.

Normal shopping must remain instant.

Cache or reuse:

* Product list
* Customer profile
* Recommendation data

AI calls should happen only when the user actively requests an AI feature.

---

# ACCESSIBILITY

Use:

* Semantic HTML
* Proper labels
* Keyboard navigation
* Accessible buttons
* Good contrast
* Clear focus states
* Alt text for product images

---

# SECURITY

For development:

* Do not expose API keys in frontend code.
* Keep AI keys server-side if an AI API is used.
* Do not trust frontend totals.
* Validate all order data server-side.
* Do not allow arbitrary product IDs/prices from the browser to become final order values.

---

# IMPORTANT: AI API

If no AI API key is available during development, DO NOT block the project.

Create a local/mock AI service that demonstrates the complete AI behaviour.

For example:

Input:

“I need boneless fish for frying.”

Mock AI returns:

Salmon Fillet

King Fish

The architecture must make the AI provider replaceable later.

Do not hard-code the AI provider into the UI.

Create a service abstraction such as:

```text
aiService
```

with methods:

```text
findProducts()
recommendMeal()
buildOrder()
calculatePortion()
recommendForCustomer()
```

---

# CODE QUALITY

Keep the code modular.

Do not put the entire Mini Order system into one giant JavaScript file.

Separate:

* Product data
* Customer data
* Cart
* Pricing
* Orders
* Recommendations
* AI services
* UI components
* Admin
* Mock API/data

Use clear naming.

Add comments where business logic is important.

---

# DO NOT MODIFY EXISTING WEBSITE UNNECESSARILY

The existing Tarel homepage must continue working.

Do not remove:

* Existing sections
* Existing WhatsApp buttons
* Existing vendor flow
* Existing contact flow
* Existing assets
* Existing responsive design

Only modify the existing WhatsApp order CTA where necessary to introduce the Mini Order Page.

Keep a support WhatsApp option.

---

# FINAL ACCEPTANCE CRITERIA

The project is complete only when:

1. Existing Tarel website still works.
2. Mini Order Page works locally.
3. Customer identification works.
4. Customer name + initial works.
5. Customer ID works.
6. Product browsing works.
7. Normal search works.
8. AI Fish Finder works.
9. Natural-language search works.
10. What Should I Cook works.
11. Build My Order works.
12. Budget ordering works.
13. Portion calculator works.
14. Order Again works.
15. Personalised recommendations differ by customer.
16. Products can be added from AI directly to cart.
17. Cart works.
18. Pricing works.
19. Discount works.
20. Freight surcharge works.
21. Delivery works.
22. Collection works.
23. Delivery date works.
24. Notes work.
25. Order can be submitted.
26. One order record is created.
27. Order appears in Received Orders.
28. Admin can review.
29. Admin can confirm.
30. Admin can reject.
31. Confirmed order appears in Order Management.
32. Same Order ID is maintained.
33. Order status can progress to Delivered.
34. Customer can see updated status.
35. No Meta API is required.
36. No deployment occurs.
37. No GitHub push occurs.
38. No production data is modified.
39. No API keys are exposed.
40. The entire flow can be demonstrated locally.

---

# FINAL INSTRUCTION

Before declaring the work complete:

1. Run the project locally.
2. Test the customer flow from beginning to end.
3. Test the admin flow from beginning to end.
4. Test AI/mock-AI features.
5. Test personalised recommendations using at least two different customers.
6. Test cart calculations.
7. Test discount.
8. Test freight surcharge.
9. Test delivery and collection.
10. Test order confirmation.
11. Test order rejection.
12. Test order status progression.
13. Test mobile responsive layout.
14. Check browser console for errors.
15. Fix all obvious errors.
16. Do NOT deploy.
17. Do NOT push.
18. Do NOT commit.
19. Leave everything in local development state.

At the end, provide:

* What was built
* Files changed/created
* How to run locally
* Local URLs
* Demo customer IDs
* Demo order flow
* AI features implemented
* Any remaining limitations

The priority is:

**Existing Tarel visual identity + excellent mobile ordering UX + reliable normal commerce logic + useful AI assistance + personalised recommendations + complete local end-to-end testing.**

