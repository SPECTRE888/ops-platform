# BAR OPS — Tech Reference

Professional event management platform for bar/catering operations.

## Live Site
- **URL**: https://bar-opsv2public.netlify.app/app.html
- **Demo**: `?demo=1` for offline mode
- **Repo**: https://github.com/SPECTRE888/bar-ops
- **Deploy**: git push main → auto-deploy Netlify (~30s)

## Stack
- **Frontend**: Vanilla HTML/JS/CSS (single-file app.html, ~7500 lines)
- **Backend**: Netlify Functions (Node.js)
- **Auth**: Supabase OAuth (Google)
- **Database**: Supabase PostgreSQL
- **Payments**: Stripe (subscriptions)
- **Hosting**: Netlify

## Sidebar Structure (Real)

### Menu Organization
```
├── Dashboard
├── Bar
│   ├── Catalogue (Spirits, Juices, Mixers, Syrups, Garnishes, etc.)
│   └── Cocktails
├── Équipe (Team)
│   ├── Mon équipe (Staff roster)
│   ├── Clients
│   └── Fournisseurs (Suppliers)
├── Prestation (Services)
│   ├── Événements (Event creation)
│   ├── Suivi (Financial tracking)
│   └── Historique (Past events)
├── Planning (Calendar)
└── Compte (Account)
    ├── Profil (Settings)
    └── Déconnexion (Logout)
```

## Catalogue Categories
- Spiritueux (Spirits)
- Jus & Purées (Juices)
- Mixers & Sodas
- Sirops (Syrups)
- Garnitures (Garnishes)
- Consommables (Consumables)
- Épices & Condiments (Spices)
- Verrerie (Glassware)
- Glace (Ice)
- Bar & Matériel (Equipment)

## Key Features (Live)

### Inventory Management
- Catalogue with multi-category filtering
- Glassware tracking (types, volumes, pricing, stock)
- Ice management (quantities, pricing)

### Team Management
- Staff roster with roles (Bartender, Serveur, Bar Manager, Manutentionnaire)
- Hourly rates + billing
- Contact management

### Event Planning
- Event creation with full details
- Cocktail selection + quantity
- Staff assignment
- Delivery cost/billing
- Financial tracking (CA, margins, deposits)

### Quotations & Invoicing
- Automatic quote generation
- Invoice management
- Payment tracking (deposits, full payment)

### Calendar & History
- Monthly event planning calendar
- Past events archive with search
- Event status tracking

## Core Rules

1. **Vanilla architecture** — no frameworks, no modules, no build step
2. **Single-file HTML** — app.html contains all app logic
3. **PATCH ONLY** — minimal, targeted modifications only
4. **Mobile-first** — responsive design
5. **Offline capable** — `?demo=1` mode for demo/testing
6. **Deterministic pricing** — loss% formula for cocktails, hourly rates for staff

## Authentication
- **Method**: Supabase + Google OAuth
- **Flow**: Email/password or Google login
- **Subscription**: Stripe paywall on login

## Storage & State
- **Local**: in-memory `state` object
- **Persistent**: localStorage via `save()`/`load()` (user-scoped via `SK`)
- **Cloud**: Supabase sync via `cloudPush()`/`cloudPull()`
- **Demo**: `?demo=1` uses `freshState()`, no cloud access

## Constants & Conventions

### Staff Types (IMMUTABLE)
```javascript
['Bartender', 'Serveur', 'Bar Manager', 'Manutentionnaire']
```

### Event Timing
- `arrBrt`/`depBrt` = Bartender arrival/departure (decimal hours)
- `arrWtr`/`depWtr` = Server arrival/departure
- `arrMgr`/`depMgr` = Manager arrival/departure
- `arrMan`/`depMan` = Manutentionnaire arrival/departure

### Pricing Formula (Cocktail)
```
prixVente = costHT / (1 - loss/100)
```

## Backend Functions

Located in `netlify/functions/`:
- `subscription.js` — Stripe checkout handler
- `delete-account.js` — Account deletion
- `send-quote.js` — Email quote via SendGrid
- `webhook.js` — Stripe webhook processor

## Development Workflow

```bash
cd ops-platform/apps/bar-ops
git add .
git commit -m "feature: description"
git push origin main
# → Netlify auto-deploys to live site (~30s)
```

Test locally by opening `app.html` in browser. Use `?demo=1` for offline testing.

