# Kubernetes ConfigMap Manifest Guide

## Table of Contents

- [Kubernetes ConfigMap Manifest Guide](#kubernetes-configmap-manifest-guide)
  - [Basic ConfigMap Structure](#basic-configmap-structure)
  - [Key Components Explained](#key-components-explained)
    - [1. Metadata Section](#1-metadata-section)
    - [2. Data Section](#2-data-section)
  - [Creating ConfigMaps](#creating-configmaps)
    - [1. From Literal Values](#1-from-literal-values)
    - [2. From Files](#2-from-files)
    - [3. From Directory](#3-from-directory)
  - [Using ConfigMaps in Pods](#using-configmaps-in-pods)
    - [1. As Environment Variables](#1-as-environment-variables)
    - [2. As Single Environment Variable](#2-as-single-environment-variable)
    - [3. As Volume Mount](#3-as-volume-mount)
  - [Best Practices](#best-practices)
  - [Common Commands](#common-commands)
- [Create ConfigMap from literal values](#create-configmap-from-literal-values)
- [Create ConfigMap from file](#create-configmap-from-file)
- [Create ConfigMap from directory](#create-configmap-from-directory)
- [View ConfigMap](#view-configmap)
- [Edit ConfigMap](#edit-configmap)
- [Delete ConfigMap](#delete-configmap)
  - [Troubleshooting](#troubleshooting)
  - [Important Notes](#important-notes)


This guide explains the structure and components of a Kubernetes ConfigMap manifest.

## Basic ConfigMap Structure

A ConfigMap is a Kubernetes resource that stores non-confidential data in key-value pairs. Here's a breakdown of the key components:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: default
data:
  # Simple key-value pair
  APP_COLOR: "blue"
  APP_MODE: "production"
  
  # File-like key
  game.properties: |
    enemy.types=aliens,monsters
    player.maximum-lives=5
    
  # Multi-line configuration
  ui.properties: |
    color.good=purple
    color.bad=yellow
    allow.textmode=true
```

## Key Components Explained

### 1. Metadata Section
- `apiVersion`: v1 (for ConfigMaps)
- `kind`: ConfigMap
- `metadata`: ConfigMap identification
  - `name`: Unique name for the ConfigMap
  - `namespace`: (Optional) Namespace where ConfigMap resides

### 2. Data Section
- `data`: Key-value pairs of configuration data
  - Simple key-value pairs
  - File-like keys with multi-line content
  - Binary data (using `binaryData` field)

## Creating ConfigMaps

### 1. From Literal Values
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: literal-config
data:
  DB_HOST: "mysql"
  DB_PORT: "3306"
```

### 2. From Files
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: file-config
data:
  # Content of config-file.txt
  config-file.txt: |
    line1
    line2
    line3
```

### 3. From Directory
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: dir-config
data:
  file1.properties: |
    key1=value1
    key2=value2
  file2.properties: |
    key3=value3
    key4=value4
```

## Using ConfigMaps in Pods

### 1. As Environment Variables
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: env-pod
spec:
  containers:
  - name: test-container
    image: nginx
    envFrom:
    - configMapRef:
        name: app-config
```

### 2. As Single Environment Variable
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: single-env-pod
spec:
  containers:
  - name: test-container
    image: nginx
    env:
    - name: APP_COLOR
      valueFrom:
        configMapKeyRef:
          name: app-config
          key: APP_COLOR
```

### 3. As Volume Mount
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-pod
spec:
  containers:
  - name: test-container
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: app-config
```

## Best Practices

1. Use meaningful ConfigMap names
2. Group related configuration together
3. Use namespaces to organize ConfigMaps
4. Keep ConfigMaps small and focused
5. Use descriptive keys
6. Consider using ConfigMap generators in CI/CD
7. Implement proper RBAC for ConfigMap access
8. Use ConfigMap updates carefully in production

## Common Commands

```bash
# Create ConfigMap from literal values
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2

# Create ConfigMap from file
kubectl create configmap my-config --from-file=path/to/file

# Create ConfigMap from directory
kubectl create configmap my-config --from-file=path/to/dir

# View ConfigMap
kubectl get configmap <configmap-name> -o yaml

# Edit ConfigMap
kubectl edit configmap <configmap-name>

# Delete ConfigMap
kubectl delete configmap <configmap-name>
```

## Troubleshooting

1. Check ConfigMap exists:
```bash
kubectl get configmap <configmap-name>
```

2. View ConfigMap contents:
```bash
kubectl describe configmap <configmap-name>
```

3. Verify ConfigMap mounted in pod:
```bash
kubectl exec <pod-name> -- ls /etc/config
```

4. Check environment variables:
```bash
kubectl exec <pod-name> -- env | grep <config-key>
```

## Important Notes

1. ConfigMaps are not encrypted
2. Maximum size is 1MiB
3. Changes to ConfigMap don't automatically update pods
4. Consider using Secrets for sensitive data
5. ConfigMaps are namespace-scoped
6. Updates to ConfigMap may require pod restart
7. Use ConfigMap volume for file-based configurations 

