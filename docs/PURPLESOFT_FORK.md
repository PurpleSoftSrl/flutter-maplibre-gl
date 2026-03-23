# Fork PurpleSoft — `flutter-maplibre-gl`

- **Fork GitHub:** [PurpleSoftSrl/flutter-maplibre-gl](https://github.com/PurpleSoftSrl/flutter-maplibre-gl)  
- **Upstream:** [maplibre/flutter-maplibre-gl](https://github.com/maplibre/flutter-maplibre-gl)  
- Documentazione plugin: [README upstream](https://github.com/maplibre/flutter-maplibre-gl/blob/main/README.md), [pub.dev `maplibre_gl`](https://pub.dev/packages/maplibre_gl).

## Sincronizzare con upstream

```bash
git fetch upstream
git checkout main
git merge upstream/main
# risolvi conflitti se presenti, poi:
git push origin main
```

Con [GitHub CLI](https://cli.github.com/) (`gh`): assicurati che `gh` sia nel `PATH` (es. `C:\Program Files\GitHub CLI`).

## Usare il fork in un’app Flutter

Nel `pubspec.yaml` dell’app (es. dependency_overrides):

```yaml
dependency_overrides:
  maplibre_gl:
    git:
      url: https://github.com/PurpleSoftSrl/flutter-maplibre-gl.git
      path: maplibre_gl
  maplibre_gl_platform_interface:
    git:
      url: https://github.com/PurpleSoftSrl/flutter-maplibre-gl.git
      path: maplibre_gl_platform_interface
  maplibre_gl_web:
    git:
      url: https://github.com/PurpleSoftSrl/flutter-maplibre-gl.git
      path: maplibre_gl_web
```

Poi `flutter pub get` e rebuild iOS/Android.

## Nota iOS — `std::domain_error` / SIGABRT

Errore tipico lato **maplibre-native** (C++): spesso legato a valori geometrici non validi (es. coordinate **NaN**, zoom/bounds fuori range, stile o sorgenti tile inconsistenti). Utile:

1. Catturare lo **stack nativo** in Xcode (breakpoint su C++ exception) o log completi all’avvio mappa.  
2. Verificare **camera iniziale** (`LatLng`, zoom) e **style URL** / JSON caricato.  
3. Confrontare versione plugin con [CHANGELOG](https://github.com/maplibre/flutter-maplibre-gl/blob/main/CHANGELOG.md) e issue upstream.

Le modifiche al fork andanno committate su `main` (o branch dedicato) e referenziate dall’app via `ref:` se serve un commit fisso.
