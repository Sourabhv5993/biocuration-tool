# Biocuration Frontend (Angular)

## Development

```powershell
npm install
npm start
```

Uses `proxy.conf.json` so API calls to `/api` forward to Django at `http://127.0.0.1:8000`.

## Production build

```powershell
npm run build
```

Set `apiUrl` in `src/environments/environment.ts` to your deployed API origin.

## Toast notifications (snackbar)

Inject `SnackbarService` (`providedIn: 'root'`) from `src/app/core/services/snackbar.service.ts`:

- `snackbar.info(message, durationMs?)` — soft teal bar (default ~4.5s)
- `snackbar.success(message, durationMs?)`
- `snackbar.error(message, durationMs?)`
- `snackbar.warning(message, durationMs?)`
- `snackbar.show(message, { variant, durationMs })`
- `snackbar.clear()` — dismiss early (the bar also has a close control)

The host UI lives in `app-snackbar` next to `router-outlet` in `app.component.ts` (compact bar, **top center**, respects `safe-area-inset-top`).

## Auth structure

| Path | Purpose |
|------|---------|
| `src/app/core/services/auth.service.ts` | Login, refresh, profile, logout |
| `src/app/core/interceptors/auth.interceptor.ts` | Bearer token + refresh on 401 |
| `src/app/core/guards/auth.guard.ts` | Requires login |
| `src/app/core/guards/role.guard.ts` | Admin / curator / QA routes |

## Next UI work

- Admin: projects list, assign members, user management
- Curator: RNA / Peptide forms bound to `payload` JSON
- QA: review queue with approve/reject
