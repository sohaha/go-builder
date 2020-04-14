# docker-golang-builder

容器化的构建环境，方便跨平台交叉编译 Go 程序

## 使用方法

```bash
docker run --rm -it -v $(pwd):/go/app -w /go/src/dev --name go-builder seekwe/go-builder:latest sh -c 'CGO_ENABLED=1 GOOS=linux GOARCH=amd64 go build'

```

## 使用示例

```bash
# 提取依赖到项目目录免得还需要去容器内去下载一遍依赖
go mod vendor

# CGO 编译 linux x64**
docker run --rm -it -v $(pwd):/go/app -w /go/src/dev --name go-builder seekwe/go-builder:latest sh -c 'CGO_ENABLED=1 GOOS=linux GOARCH=amd64 go build -mod=vendor -ldflags "-s -w"'

# CGO 编译 windows x64**
docker run --rm -it -v $(pwd):/go/app -w /go/src/dev --name go-builder seekwe/go-builder:latest sh -c 'CGO_ENABLED=1 CC=x86_64-w64-mingw32-gcc CXX=x86_64-w64-mingw32-g++ GOOS=windows GOARCH=amd64 go build -mod=vendor -ldflags "-s -w"'

# CGO 编译 windows x86
docker run --rm -it -v $(pwd):/go/app -w /go/src/dev --name go-builder seekwe/go-builder:latest sh -c 'GO111MODULE=on CGO_ENABLED=1 CC=i686-w64-mingw32-gcc CXX=i686-w64-mingw32-g++ GOOS=windows GOARCH=386 go build -mod=vendor -ldflags "-s -w"'

# CGO 编译 darwin x64**
docker run --rm -it -v $(pwd):/go/app -w /go/src/dev --name go-builder seekwe/go-builder:latest sh -c 'CGO_ENABLED=1 CC=o64-clang CXX=o64-clang++ GOOS=darwin GOARCH=amd64 go build -mod=vendor -ldflags "-s -w"'

```

## 可用版本