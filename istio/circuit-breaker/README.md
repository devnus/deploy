# 설정 공식 문서

https://istio.io/latest/docs/reference/config/networking/destination-rule/#DestinationRule

## [consecutive5xxErrors]

host가 connection pool에서 제외되는 5xx 오류 수 (\* 5)

## [consecutiveGatewayErrors]

host가 connection pool에서 제외되는 게이트웨이 오류 수. 502, 503, 504는 Gateway 오류로 판단된다. (\* 0 - disable)

consecutiveGatewayErrors 는 consecutive5xxErrors 에 포함되어져 동작합니다. 그래서 만약 consecutiveGatewayErrors 이 consecutive5xxErrors 의 값 이상으로 설정된다면 consecutiveGatewayErrors 는 효과가 없습니다.

## [interval]

interval에서 지정한 시간 내에
consecutiveError 횟수 만큼 에러가 발생하는 경우 circuit breaker 동작

## [baseEjectionTime]

차단한 호스트를 얼마 동안 로드밸런서 pool에서 제외할 것인가?
즉, 얼마나 오래 circuit breaker를 해당 호스트에게 적용할지 시간을 결정

## [maxEjectionPercent]

네트워크를 차단할 최대 host의 비율. 즉, 최대 몇 %까지 차단할 것인지 설정.
2개의 pod가 있을경우, 100%인 경우 2개 모두 차단이 가능하다
10%인 경우 차단이 불가능해 보이는데(1개가 50%이므로),
envoy에서는 circuit breaker가 발동되었으나,
10%에 해당하지 않아서 차단할 호스트가 없으면
강제적으로 해당 호스트를 차단하도록 설정한다.
