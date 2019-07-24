---
title: azdata bdc 구성 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed777391af3695da69e04c0e2693cff912c76771
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426293"
---
# <a name="azdata-bdc-config"></a>azdata bdc 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc 구성** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc 구성 초기화](#azdata-bdc-config-init) | 클러스터 만들기에 사용할 수 있는 빅 데이터 클러스터 구성 프로필을 초기화 합니다.
[azdata bdc 구성 목록](#azdata-bdc-config-list) | 사용 가능한 구성 프로필 선택을 나열 합니다.
[azdata bdc 구성 표시](#azdata-bdc-config-show) | BDC의 현재 구성 또는 지정 하는 로컬 파일의 구성 (예: custom/cluster)을 표시 합니다.
[azdata bdc 구성 추가](#azdata-bdc-config-add) | 구성 파일에서 json 경로에 대 한 값을 추가 합니다.
[azdata bdc 구성 제거](#azdata-bdc-config-remove) | 구성 파일에서 json 경로에 대 한 값을 제거 합니다.
[azdata bdc 구성 바꾸기](#azdata-bdc-config-replace) | 구성 파일의 json 경로에 대 한 값을 바꿉니다.
[azdata bdc 구성 패치](#azdata-bdc-config-patch) | Json 패치 파일을 기반으로 구성 파일을 패치 합니다.
## <a name="azdata-bdc-config-init"></a>azdata bdc 구성 초기화
클러스터 만들기에 사용할 수 있는 빅 데이터 클러스터 구성 프로필을 초기화 합니다. 구성 프로필의 특정 소스는 세 가지 선택 항목의 인수에 지정할 수 있습니다.
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>예
단계별 BDC 구성 초기화 환경-필요한 값에 대 한 프롬프트를 받게 됩니다.
```bash
azdata bdc config init
```
BDC 구성 init with 인수를 사용 하 여 aks에서 테스트의 구성 프로필을 만듭니다.
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target -t`
구성 프로필을 배치할 파일의 경로입니다. 기본적으로 cwd를 사용 하 여 사용자 지정-app.config를 사용 합니다.
#### `--source -s`
구성 프로필 원본: [' aks ', ' kubeadm ', ' minikube '].
#### `--force -f`
대상 파일을 강제로 덮어씁니다.
#### `--accept-eula -a`
사용 조건에 동의 하나요? [예/아니요]. 이 인수를 사용 하지 않으려면 환경 변수 ACCEPT_EULA을 ' y e s '로 설정할 수 있습니다. 이 제품에 대 한 사용 조건은에서 https://aka.ms/azdata-eula 볼 수 있습니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.
## <a name="azdata-bdc-config-list"></a>azdata bdc 구성 목록
에서 사용할 수 있는 구성 프로필 선택 항목 나열`bdc config init`
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>예
사용 가능한 모든 구성 프로필 이름을 표시 합니다.
```bash
azdata bdc config list
```
특정 구성 프로필의 json을 표시 합니다.
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--config-profile -c`
기본 구성 프로필: [' aks ', ' kubeadm ', ' minikube '].
#### `--type -t`
표시 하려는 구성 유형입니다.
`cluster`
#### `--accept-eula -a`
사용 조건에 동의 하나요? [예/아니요]. 이 인수를 사용 하지 않으려면 환경 변수 ACCEPT_EULA을 ' y e s '로 설정할 수 있습니다. 이 제품에 대 한 사용 조건은에서 https://aka.ms/azdata-eula 볼 수 있습니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.
## <a name="azdata-bdc-config-show"></a>azdata bdc 구성 표시
BDC의 현재 구성 또는 지정 하는 로컬 파일의 구성 (예: custom/cluster)을 표시 합니다. 섹션을 가져오려는 경우에도이 명령은 json 경로를 사용할 수 있습니다.  출력할 대상 파일을 지정할 수도 있습니다.  대상 파일을 지정 하지 않으면 터미널에만 출력 됩니다.
```bash
azdata bdc config show [--config-file -c] 
                       [--target -t]  
                       [--json-path -j]  
                       [--force -f]
```
### <a name="examples"></a>예
콘솔에 BDC 구성 표시
```bash
azdata bdc config show
```
로컬 구성 파일에서 간단한 json 키 경로의 끝에 있는 값을 가져옵니다.
```bash
azdata bdc config show --config-file custom-config/cluster.json --json-path 'metadata.name' --target section.json
```
로컬 구성 파일에서 조건부를 사용 하 여 json 키 경로 끝에 있는 값을 가져옵니다.
```bash
azdata bdc config show --config-file custom-config/cluster.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--config-file -c`
빅 데이터 클러스터 구성 파일 경로 (예: 사용자 지정/s c r i c e s.
#### `--target -t`
결과를 저장할 출력 파일입니다. 기본값: stdout으로 전달 됩니다.
#### `--json-path -j`
구성에서 원하는 섹션 또는 값 (예: key1. key2. key3)으로 이어지는 json 키 경로입니다. Jsonpath 쿼리 언어 https://jsonpath.com/ 를 사용 합니다 (예:-j ' $. spec [? ( @.spec.type = = "Master")].. 종점
#### `--force -f`
대상 파일을 강제로 덮어씁니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.
## <a name="azdata-bdc-config-add"></a>azdata bdc 구성 추가
구성 파일의 json 경로에 값을 추가 합니다.  아래의 모든 예제는 Bash에서 제공 됩니다.  다른 명령줄을 사용 하는 경우 적절 하 게 escapequotations 할 수 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>예
예 1-제어 평면 저장소를 추가 합니다.
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 구성의 빅 데이터 클러스터 구성 파일 경로입니다 (예: custom/cluster. json).
#### `--json-values -j`
값에 대 한 json 경로의 키 값 쌍 목록: key1. subkey1 = value1, key2. subkey2 = value2 Key = ' {"kind": "cluster", "name": "test-cluster"} '와 같은 인라인 json 값을 제공 하거나 키 =./values.json.와 같은 파일 경로를 제공할 수 있습니다. Add는 조건을 지원 하지 않습니다.  경로를 http://jsonpatch.com/ 표시 하는 방법에 대 한 예제는를 참조 하세요.  배열에 액세스 하려는 경우에는 key. 0 = value와 같은 인덱스를 표시 하 여이 작업을 수행 해야 합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.
## <a name="azdata-bdc-config-remove"></a>azdata bdc 구성 제거
구성 파일의 json 경로에서 값을 제거 합니다.  아래의 모든 예제는 Bash에서 제공 됩니다.  다른 명령줄을 사용 하는 경우 적절 하 게 escapequotations 할 수 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>예
예 1-제어 평면 저장소를 제거 합니다.
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 구성의 빅 데이터 클러스터 구성 파일 경로입니다 (예: custom/cluster. json).
#### `--json-path -j`
Jsonpatch 라이브러리를 기반으로 하 여 제거 하려는 값 (예: key1. subkey1, key2. subkey2)을 나타내는 json 경로의 목록입니다. Remove는 조건을 지원 하지 않습니다. 경로를 http://jsonpatch.com/ 표시 하는 방법에 대 한 예제는를 참조 하세요.  배열에 액세스 하려는 경우에는 key. 0 = value와 같은 인덱스를 표시 하 여이 작업을 수행 해야 합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.
## <a name="azdata-bdc-config-replace"></a>azdata bdc 구성 바꾸기
구성 파일의 json 경로에 있는 값을 바꿉니다.  모든 examplesbelow은 Bash에서 제공 됩니다.  다른 명령줄을 사용 하는 경우 적절 하 게 escapequotations 할 수 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>예
예 1-단일 끝점 (컨트롤러 끝점)의 포트를 바꿉니다.
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
예 2-제어 평면 저장소 바꾸기
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ex 3-복제본 (저장소 풀)을 포함 하 여 풀 저장소를 바꿉니다.
```bash
azdata bdc config replace --config-file custom/cluster.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 구성의 빅 데이터 클러스터 구성 파일 경로입니다 (예: custom/cluster. json).
#### `--json-values -j`
값에 대 한 json 경로의 키 값 쌍 목록: key1. subkey1 = value1, key2. subkey2 = value2 Key = ' {"kind": "cluster", "name": "test-cluster"} '와 같은 인라인 json 값을 제공 하거나 키 =./values.json.와 같은 파일 경로를 제공할 수 있습니다. Replace는 jsonpath 라이브러리를 통한 조건을 지원 합니다.  이를 사용 하려면 $를 사용 하 여 경로를 시작 합니다. 이를 통해-j $. key2 [? ( @.key3= = ' someValue ']. key4 = value. 아래 예제를 볼 수 있습니다. 추가 도움말은 다음을 참조 하세요. https://jsonpath.com/
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.
## <a name="azdata-bdc-config-patch"></a>azdata bdc 구성 패치
지정 된 패치 파일에 따라 구성 파일을 패치 합니다. 경로를 http://jsonpatch.com/ 구성 하는 방법에 대 한 자세한 내용은를 참조 하십시오. Replace 작업은 jsonpath 라이브러리로 https://jsonpath.com/ 인해 해당 경로에 조건을 사용할 수 있습니다. 모든 패치 json 파일은 해당 하는 op (추가, 바꾸기, 제거), 경로 및 값을 포함 하는 패치 배열을 포함 하는 "patch"의 키로 시작 해야 합니다. "제거" op에는 값, 경로만 필요 하지 않습니다. 아래 예제를 참조 하세요.
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>예
예 1-단일 끝점 (컨트롤러 끝점)의 포트를 패치 파일로 바꿉니다.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
예 2-제어 평면 저장소를 패치 파일로 바꿉니다.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3-복제본 (저장소 풀)을 포함 하는 풀 저장소를 패치 파일로 바꿉니다.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 구성의 빅 데이터 클러스터 구성 파일 경로입니다 (예: custom/cluster. json).
#### `--patch-file -p`
Jsonpatch 라이브러리 http://jsonpatch.com/ 를 기반으로 하는 패치 json 파일의 경로입니다. "Patch" 라는 키를 사용 하 여 패치 json 파일을 시작 해야 합니다. 해당 값은 원하는 패치 작업의 배열입니다. 패치 작업의 경로에 대해 대부분의 작업에 대해 key1과 같은 점 표기법을 사용할 수 있습니다. 바꾸기 작업을 수행 하 고 조건부가 필요한 배열의 값을 바꾸려는 경우 $를 사용 하 여 경로를 시작 하 여 jsonpath 표기법을 사용 하세요. 그러면 $. key1 [? ()와 같은 조건부를 사용할 수 있습니다. @.key3= = ' someValue ']. key4. 아래 예제를 참조 하세요. 조건에 대 한 추가 도움말은를 참조 https://jsonpath.com/ 하세요.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.

## <a name="next-steps"></a>다음 단계

다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요. **Azdata** 도구를 설치 하는 방법에 대 한 자세한 내용은 [install azdata to manage SQL Server 2019 빅 data 클러스터](deploy-install-azdata.md)를 참조 하세요.