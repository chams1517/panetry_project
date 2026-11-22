<<<<<<< HEAD
# Dar El-Mouna

Tunisian and regional recipes, with pantry, meal planning and shopping features in progress. Django project.

## Run it

```
python -m venv .venv
.venv\Scripts\activate          # Windows  (macOS/Linux: source .venv/bin/activate)
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Add recipes (with photos) in the admin at `/admin/`. Uploaded photos are stored in `media/`.

## Pages

| Page | URL | What it does |
|---|---|---|
| Dashboard | `/dashboard/` | Stats, today's meals, items to use soon, open lists, recipes matching your pantry |
| Discover recipes | `/recipes/` | Your recipes + the TheMealDB online library; search, category and region filters |
| Online recipe | `/recipes/online/<id>/` | Preview of an online recipe, "Add to my recipes" imports it |
| Recipe | `/recipes/<id>/` | Ingredients compared with your pantry, favorite, add to plan, make shopping list |
| My pantry | `/pantry/` | Add, merge and remove ingredients, with expiry dates |
| Meal planner | `/planner/` | Week view, add/remove meals, one shopping list for the week |
| Shopping list | `/shopping/` | Lists and items, tick off, created by hand, from a recipe or from the week |
| Favorites | `/recipes/favorites/` | Saved recipes |
| Chef Ramsay | `/chef-ramsay/` | AI chef (Grok) that knows your pantry, expiry dates, plan, favorites and recipes |
| Settings | `/accounts/settings/` | Profile and password |

## Chef Ramsay (Grok)

Chef Ramsay uses the xAI Grok API. Get a key at https://console.x.ai, then set it before starting the server:

```
set XAI_API_KEY=your-key            # Windows  (macOS/Linux: export XAI_API_KEY=your-key)
set XAI_MODEL=grok-4                # optional, any chat model your key can use
python manage.py runserver
```

Each question sends Grok your pantry, expiring items, planned meals, favorites and a catalog of your recipes (no email or personal data), plus the last 10 messages. It can only recommend recipes that exist in your catalog; invented ids are dropped. The key stays on the server. Without a key, or if Grok is unreachable, a simple rule-based fallback answers instead. Limit: 40 messages per user per hour (`CHEF_MAX_MESSAGES_PER_HOUR`). Code: `chatbot/brain.py`, `llm.py`, `context.py`.

## Recipe API (TheMealDB)

`recipes/services/themealdb.py` is a small client for https://www.themealdb.com (free, no key needed with the public test key). Responses are cached for an hour and any network failure is shown as a friendly message while your own recipes keep working. Importing (`recipes/services/importer.py`) copies a recipe, its ingredients and its photo URL into the local database so it can be favorited, planned and shopped for. TheMealDB gives no preparation time, so imported recipes get an estimate based on the ingredient count.

To use another key or a mirror: `set THEMEALDB_BASE_URL=https://www.themealdb.com/api/json/v1/<key>` (environment variable).

Tests: `python manage.py test` (the API is mocked, no network needed).

## Frontend

- Look: warm white page, soft cards, dark pill buttons, orange accent. `static/css/` holds the design system: `tokens.css` (colors and type, light and dark in one place), `base.css`, `layout.css`, `components.css`, and `pages/`.
- `templates/partials/` holds reusable pieces: header, footer, recipe card, form field, empty state, pagination, icons.
- Dark mode follows the system setting; the toggle saves a manual choice in the browser.
- The font (DM Sans) is self-hosted in `static/fonts/` under the SIL Open Font License; icons are from Lucide (ISC).
- To add a photo to the login and signup pages, put an image in `static/img/` and add this to `static/css/layout.css`:
  `.auth-art { --auth-photo: url("../img/auth-hero.jpg"); }`
=======
# panetry_project
>>>>>>> aa8ef26662895a31a051486e599eae6867b11213
