# 일반적인 Node.js 도커 베스트 프랙티스

다음의 일반 도커 가이드라인 섹션은 모든 프로그래밍 언어들 사이에서 표준화된 best practice를 포함하며 Node.js에 국한되지 않는다.

## ![✔] ADD 대신 COPY 커맨드를 사용하여라

**핵심 요약:** ADD가 원격 사이트로부터 바이너리들을 다운로드하는 등 향상된 가져오기를 지원하는 반면 COPY는 로컬파일들만 복제하기 때문에 더 안전하다.

## ![✔] 베이스 OS 업데이트를 피하라

**핵심 요약:** 빌드 중에 로컬 바이너리들을 업데이트하는 것(예. apt-get update)은 돌 때마다 관련없는 이미지들을 생성하고 향상된 우선권을 요구로 한다. 이러는 대신에 자주 업데이트되는 베이스 이미지를 사용하여라

## ![✔] labels를 이용해 이미지를 분류하여라

**핵심 요약:** 각 이미지에 메타데이터를 제공하는 것은 Ops professional 이미지를 적절히 다루는데 도움을 줄 것이다. 예를 들어, 메인테이너 이름을 포함하고, 데이트와 누군가 이미지에 대한 수학적 증명을(reason about) 할 때 유용할 수 있는 정보를 빌드하여라.

## ![✔] 특권이 없는 컨테이너들을 사용하라

**핵심 요약:** 특권이 있는 컨테이너들은 루트 유저가 호스트 머신에 대해 갖는 것과 동일한 권한과 능력을 가지고 있다. 이것은 필요치 않고 경험상 공식 노드 이미지 내에 생성된 'node' 유저를 사용하여야 한다.

## ![✔] 최종 결과를 검사하고 증명하라.

**핵심 요약:** 종종 빌드 프로세스 과정의 비밀 혹은 중요하지 않은 파일들의 유출과 같은 부작용을 간과하는 경우가 있다. [Dive](https://github.com/wagoodman/dive)같은 툴을 이용해 생성된 이미지를 검사함은 이와 같은 문제를 알아내는 데 도움을 줄 수 있다.

## ![✔] 완전성 체크를 수행하여라

**핵심 요약:** 베이스 혹은 최종 이미지들을 풀 하는 과정에서, 네트워크는 해로운 이미지를 다운로드 하도록 선동되거나 리다이렉트 되기도 한다. content를 서명하거나 증명하지 않는 한 도커 포로토콜의 표준 중 이러한 현상을 방지하는 것은 없다. [Docker Notary](https://docs.docker.com/notary/getting_started/)는 이 현상을 방지할 수 있는 툴 중 하나이다.