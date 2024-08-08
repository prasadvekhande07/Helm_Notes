# Helm_Notes
"Here's a structured version of your notes on Helm:

### Helm Chart Overview

#### Purpose:
- Helm introduces reusable Kubernetes (K8s) configurations to avoid code repetition.
- Options for Helm chart structure:
  1. One Helm chart per microservice (for very different configurations).
  2. A shared Helm chart for all microservices (for similar configurations).
  3. Combination of both:
     - Shared chart for similar applications.
     - Separate charts for completely different applications.

### Basic Structure of a Helm Chart

#### Folder Structure:
```
microservice/
  ├── charts/         # Chart dependencies
  ├── templates/      # K8s YAML templates with placeholders
  ├── .helmignore     # Files to exclude from the Helm chart
  ├── Chart.yaml      # Chart metadata
  ├── values.yaml     # Default values for the templates
```
- Templates use placeholders defined in `{{ }}`, which Helm replaces with actual values.

### Values Object

- Built-in object that is initially empty.
- Sources for values:
  1. `values.yaml` file in the chart.
  2. User-supplied file passed with `-f` flag.
  3. Parameter passed with `--set` flag.

### Built-in Objects

- Templates receive several objects from the template engine:
  - Examples: "Release", "Files", "Values", etc.
  - Documentation: [Helm Built-in Objects](https://helm.sh/docs/chart_template_guide/builtin_objects)

### Variable Naming Conventions

- Names should begin with a lowercase letter.
- Use camelCase for separation.

### "Range" in Templates

- Provides a "for each"-style loop to iterate through lists.

### Commands

#### Creating a Helm Chart:
```bash
$ helm create microservice
```

#### Installing a Helm Chart with Specific Values:
```bash
$ helm install -f email-service-values.yaml emailservice microservice
$ helm install -f values/recommendation-service-values.yaml recommendationservice microservice
```

#### Template Command:
```bash
$ helm template -f values/redis-values.yaml charts/redis
```
- To check if it is taking the correct values.

#### Dry Run and Install:
```bash
$ helm install --dry-run -f values/redis-values.yaml rediscart charts/redis
```

#### Uninstalling a Release:
```bash
$ helm uninstall emailservice
```

### Helmfile

- Declarative way to manage Helm charts: `helmfile.yaml`
- Functions:
  - Declare the definition of an entire K8s cluster.
  - Change specifications depending on the application or environment.

#### Commands:
```bash
$ brew install helmfile
$ helmfile sync
$ helmfile list
$ helmfile destroy
```

### Where to Host Helm Charts

- With your application code.
- In a separate Git repository for Helm charts."
