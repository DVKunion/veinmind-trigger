# Veinmind Trigger

基于 `veinmind-action` 实现 `http` 自动调用触发 `action` 扫描, 并将扫描结果上传至 OSS

## 使用

1. Fork 本仓库到自己的账户下
2. 创建属于自己的GitHub Token
3. 调用接口:

```shell
curl -v\
  -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-GITHUB_TOKEN>"\
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/<USER>/veinmind-trigger/actions/workflows/scanner.yml/dispatches \
  -d '{"ref":"main","inputs":{"image":"ubuntu:latest"}'
```

将会自动触发扫描。并将结果存储到 `action` 的 `Artifact`

如果需要上传结果至oss, 需要:

```shell
curl -v\
  -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-GITHUB_TOKEN>"\
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/<USER>/veinmind-trigger/actions/workflows/scanner.yml/dispatches \
  -d '{"ref":"main","inputs":{"image":"ubuntu:latest", "imageId": "<image sha256Id>", "ep": "", "ak":"", "sk":""}'
```