# Belloga Deploy

deploy 관련 디스크립터들을 관리하는 레포입니다

- AWS EKS 클러스터를 준비해주세요.
- ISTIO 1.14.1 버전을 준비해주세요.

(자세한 구성법은 매뉴얼 참고하기)

## 1. EKS 클러스터에 istio 구성하기

```
istioctl install -f ./istioOperator/istio-operator.yaml
```

### 설치 check

```
kubectl get deploy -n istio-system
```

### exteranl IP 확인

```
kubectl get svc -n istio-system
```

### istio 구성 삭제

```
istioctl x uninstall --purge
```

## 2. istio-injection 자동주입 활성화

```
kubectl label namespace default istio-injection=enabled
```

## 3. 마이크로서비스 배포

```
kubectl apply -f ./microservices
```

## 4. istio gateway

```
kubectl apply -f ./istio/ingress
```

## 5. service entry

```
kubectl apply -f ./istio/serviceEntry
```

## 6. zipkin

마이크로서비스 분산 로그 트레이싱을 위한 zipkin 활성화

```
kubectl apply -f ./istio/addons/zipkin.yaml
```
