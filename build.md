# MaxKB Docker构建指南

## 构建步骤

按照以下顺序执行构建命令：

### 1. 构建向量模型镜像

```bash
docker build -t maxkb-vector-model:latest -f installer/Dockerfile .
```

### 2. 构建Python-PostgreSQL环境镜像

```bash
docker build -t maxkb-python-pg -f installer/Dockerfile-python-pg .
```

### 3. 构建主应用镜像

```bash
docker build -t daqian/maxkb -f installer/Dockerfile .
```

## 高级构建选项

### 使用版本标签
如果需要指定版本标签，可以使用以下命令：
```bash
docker build -t maxkb-vector-model:v1.0 -f installer/Dockerfile-vector-model .
docker build -t maxkb-python-pg:v1.0 -f installer/Dockerfile-python-pg .
docker build -t maxkb:v1.0 -f installer/Dockerfile .
```

### 缓存控制
不使用缓存构建：
```bash
docker build --no-cache -t daqian/maxkb -f installer/Dockerfile .
```

强制使用缓存构建：
```bash
docker build --cache-from daqian/maxkb:latest -t daqian/maxkb -f installer/Dockerfile .
```

## 注意事项
1. 请确保在项目根目录下执行构建命令
2. 构建顺序很重要，因为可能存在镜像依赖关系
3. 首次构建时建议使用 `--no-cache` 选项以确保所有组件都是最新的

