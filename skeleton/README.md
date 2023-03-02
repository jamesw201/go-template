# ${{ values.component_id }}

## Description

${{ values.description }}

## Develop

Validate spec
```
swagger validate ./swagger.yml
```

Generate code
```
swagger generate server -A infrastructure-api -f ./swagger.yml
```
