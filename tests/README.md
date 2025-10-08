# Terratest

## Prerequites

* Go (1.25.1)

Installing on Mac
```bash
brew install go
```
Installing on Linux (Debian/Ubuntu)
```bash
sudo apt install golang-go 
```

Verify Version
```bash
go version
```

## Initializing Tests

If go.mod is not in the tests folder, then perform the following:

```bash
cd tests
go mod init github.com/mlaguren/infrastructure-pipeline/tests
go get github.com/gruntwork-io/terratest/modules/terraform
go get github.com/stretchr/testify/assert
go mod tidy
```

For junit output, install gotestsum.
```bash
go install gotest.tools/gotestsum@latest
```
