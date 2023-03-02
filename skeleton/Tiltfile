# -*- mode: Python -*-
load('ext://namespace', 'namespace_create')
load('ext://helm_remote', 'helm_remote')
load('ext://helm_resource', 'helm_resource')
load('ext://restart_process', 'docker_build_with_restart')

namespace_create('testapp')

goswagger_cmd = 'swagger generate server -A infrastructure-api -f ./swagger.yml'
copy_api_cmd = 'cp ./configure_infrastructure_api.go restapi/configure_infrastructure_api.go'
compile_cmd = 'GOOS=linux GOARCH=amd64 go build -o infrastructure-api-server ./cmd/infrastructure-api-server'
go_mod_tidy_cmd = 'go mod tidy'

local_resource(
  'go-swagger',
  goswagger_cmd,
)

local_resource(
  'copy-api',
  copy_api_cmd,
  deps=['go-swagger'],
)

local_resource(
  'go-mod-tidy',
  go_mod_tidy_cmd,
  deps=['copy-api'],
)

local_resource(
  'go-compile',
  compile_cmd,
  deps=['go-mod-tidy'],
)

docker_build(
  'example-go-image',
  '.',
  dockerfile='./Dockerfile',
)

k8s_yaml(helm('infrastructure/infra-api', name='infra-api', values='infrastructure/infra-api/values.yaml'))
k8s_resource('infra-api-test-go-api', port_forwards='8081:3000')
