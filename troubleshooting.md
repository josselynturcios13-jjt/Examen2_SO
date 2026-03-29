# Actividad 4: Troubleshooting - CI/CD Workflows

## Snippet 1 - Error de sintaxis en triggers

### ❌ Código con error:
```yaml
on:
  push
  branches: [main]
  pull_request
  branches [main, develop]
```

### ✅ Código corregido:
```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main, develop]
```
**Error:** Faltaban los dos puntos (:) después de `push` y `pull_request`,
y faltaba el `:` después de `branches` en pull_request.

---

## Snippet 2 - Referencia incorrecta a secrets

### ❌ Código con error:
```yaml
env:
  VERCEL_TOKEN: secrets.VERCEL_TOKEN
```

### ✅ Código corregido:
```yaml
env:
  VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
```
**Error:** Faltaba la sintaxis de expresión `${{ }}` para referenciar secrets.

---

## Snippet 3 - Matrix inválida

### ❌ Código con error:
```yaml
strategy:
  matrix:
    node-version: 18
```

### ✅ Código corregido:
```yaml
strategy:
  matrix:
    node-version: ["18.x", "20.x"]
```
**Error:** `node-version` era un valor escalar en vez de un array.
La matrix strategy requiere una lista con corchetes.