## start

```bash
$ source setup.sh
```

<br>



## 접속

- [http://localhost:30009](http://localhost:30009)

<br>



## 로그인

- id : admin
- pw : 위의 `start` 과정에서 콘솔에 출력된 비밀번호

비밀번호는 ArgoCD 접속 후 Account Settings 에서 변경 가능

<br>



## ArgoCD 클러스터 종료

```bash
source destroy.sh

또는

kind delete cluster --name nextjs-argocd-cluster
```

또는 Docker Desktop 에서 `nextjs-argocd-cluster-control-plane`, `nextjs-argocd-cluster-worker` 를 Delete 합니다.

<br>



## 접속포트를 바꾸려면?

- 가급적 사용하지 않는 포트를 클러스터 포트 매핑으로 해두었습니다.
- 만약 다른 포트를 사용하시려면 `argocd-cluster.yml` 파일에서 아래 주석 표시된 부분을 수정한 후 클러스터 삭제 후 재기동하세요.

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  kubeadmConfigPatches:
  - |
    kind: InitConfiguration
    nodeRegistration:
      kubeletExtraArgs:
        node-labels: "ingress-ready=true"
  extraPortMappings:
  ## ...
  - containerPort: 30009 # 컨테이너 내부 포트 
    hostPort: 30009 # 여기를 변경하시면 새로운 포트로 접속 가능합니다.
    protocol: TCP
  - containerPort: 80
    hostPort: 3000
    protocol: TCP
- role: worker
# - role: worker
# - role: worker
```