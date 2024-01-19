## 클러스터 생성
```bash
$ cd cluster/nextjs-argocd-cluster

$ source setup.sh
```
<br>


## ArgoCD 접속
[http://localhost:30009](http://localhost:30009) 에 접속<br>
<br>


## nextjs 애플리케이션 구동
```bash
$ cd deploy/kustomize/overlay

$ kubectl kustomize ./ | kubectl apply -f -

```

## nextjs 애플리케이션 접속
[http://localhost:3000](http://localhost:3000) 에 접속<br>
<br>

## 이번 문서에서 문서화 하려고 하는 것
아래 Before, After 에 해당하는 버전들에 대해 Blue/Green 배포시에는 어떻게 하는지, Canary 배포시에는 어떻게 하는지를 기록하려 함.
<br>

도커 이미지 저장소 : [hub.docker.com/repository/docker/chagchagchag/nextjs-argocd-example](https://hub.docker.com/repository/docker/chagchagchag/nextjs-argocd-example/general)
<br>

### Before (태그 : `v0.0.1`)
<img src="./docs/img/BEFORE.png"/>
<br>

### After (태그 : `v0.0.2`)
<img src="./docs/img/AFTER.png"/>
<br>

> 참고)
> Next.js 는 초기 node 의존성을 다운로드 받기 까지 굉장한 시간이 소요됩니다. 굉장히 느.......립니다. `kubectl -n nextjs-example get all` 을 통해 리소스 상태를 확인 후 `Running` 상태일때 `http://localhost:3000` 으로 접속하시기 바랍니다.<br>
> <br>
