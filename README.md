# Helm Quick Reference

## Template Syntax

### Built-in Objects
```yaml
"{{ .Release.Name }}-nginx"      # Name of the release
"{{ .Chart.AppVersion }}"        # App version from Chart.yaml
"{{ .Chart.Name }}"              # Chart name
```

### Values Reference
```yaml
# Access values from values.yaml
replicas: {{ .Values.deploy.replicas }}
image: "nginx:{{ .Chart.AppVersion }}"
```

## Common Commands

### Install
```bash
# Dry run (test without installing)
helm install --generate-name .\build4kube\ --dry-run

# Install with auto-generated name
helm install --generate-name .\build4kube\

# Install with specific name
helm install my-release .\build4kube\
```

### Upgrade & Rollback
```bash
# Upgrade existing release
helm upgrade "release-name" ./build4kube

# Rollback to previous version
helm rollback "release-name"
```

### List & Delete
```bash
# List all releases
helm list

# Delete a release
helm uninstall "release-name"
```

### Debugging
```bash
# Render templates locally
helm template .\build4kube\

# Show chart values
helm show values .\build4kube\
```

## Configuration Files

### Chart.yaml
```yaml
appVersion: "1.29.0"  # Used as {{ .Chart.AppVersion }} in templates
```

### values.yaml
```yaml
deploy:
  replicas: 2
```

### templates/deployment.yaml
```yaml
replicas: {{ .Values.deploy.replicas }}
image: "nginx:{{ .Chart.AppVersion }}"
```

## Key Points
- Values in `Chart.yaml` → accessed via `.Chart.*`
- Values in `values.yaml` → accessed via `.Values.*`
- Image version controlled by `appVersion` in Chart.yaml
- To update app version: change `appVersion` in Chart.yaml, then run `helm upgrade`