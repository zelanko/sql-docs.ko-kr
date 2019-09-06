---
title: azdata bdc config 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc config 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b24a552bcfaae45fa4c8644d590d2573909a03ce
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304834"
---
# <a name="azdata-bdc-config"></a>azdata bdc config

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

이 문서는 **azdata**에 대 한 참조 문서입니다. 

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc config init](#azdata-bdc-config-init) | 클러스터를 만드는 데 사용할 수 있는 빅 데이터 클러스터 구성 프로필을 초기화합니다.
[azdata bdc config list](#azdata-bdc-config-list) | 사용 가능한 구성 프로필 선택 항목을 나열합니다.
[azdata bdc config show](#azdata-bdc-config-show) | BDC의 현재 구성 또는 지정 하는 로컬 파일의 구성 (예: custom/BDC. json)을 표시 합니다.
[azdata bdc config add](#azdata-bdc-config-add) | 구성 파일에서 json 경로의 값을 추가합니다.
[azdata bdc config remove](#azdata-bdc-config-remove) | 구성 파일에서 json 경로의 값을 제거합니다.
[azdata bdc config replace](#azdata-bdc-config-replace) | 구성 파일에서 json 경로의 값을 바꿉니다.
[azdata bdc config patch](#azdata-bdc-config-patch) | json 패치 파일을 기준으로 구성 파일을 패치합니다.
## <a name="azdata-bdc-config-init"></a>azdata bdc config init
클러스터를 만드는 데 사용할 수 있는 빅 데이터 클러스터 구성 프로필을 초기화합니다. 구성 프로필의 특정 원본을 세 가지 선택 항목 중 하나로 인수에 지정할 수 있습니다.
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>예
안내에 따른 BDC 구성 초기화 환경 - 필요한 값에 대한 프롬프트가 표시됩니다.
```bash
azdata bdc config init
```
인수를 사용하는 BDC 구성 초기화 - ./custom에서 aks-dev-test의 구성 프로필을 만듭니다.
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target -t`
구성 프로필을 배치할 위치의 파일 경로입니다. custom-config.json에서 기본적으로 cwd로 설정되어 있습니다.
#### `--source -s`
구성 프로필 원본: [' aks ', ' kubeadm-prod ', ' minikube ', ' kubeadm ']
#### `--force -f`
대상 파일을 강제로 덮어씁니다.
#### `--accept-eula -a`
사용 조건에 동의하시겠습니까? [예/아니요]. 이 인수를 사용하지 않으려면 ACCEPT_EULA 환경 변수를 ‘yes’로 설정하면 됩니다. 
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-config-list"></a>azdata bdc config list
`bdc config init`에서 사용할 수 있는 구성 프로필 선택 항목을 나열합니다.
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>예
사용 가능한 구성 프로필 이름을 모두 표시합니다.
```bash
azdata bdc config list
```
특정 구성 프로필의 json을 표시합니다.
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--config-profile -c`
기본 구성 프로필: [' aks ', ' kubeadm-prod ', ' minikube ', ' kubeadm ']
#### `--type -t`
확인하려는 구성 유형입니다.
`cluster`
#### `--accept-eula -a`
사용 조건에 동의하시겠습니까? [예/아니요]. 이 인수를 사용하지 않으려면 ACCEPT_EULA 환경 변수를 ‘yes’로 설정하면 됩니다. 
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-config-show"></a>azdata bdc config show
BDC의 현재 구성 또는 지정 하는 로컬 파일의 구성 (예: custom/BDC. json)을 표시 합니다. 한 섹션만 가져오려는 경우에도 이 명령에 json 경로를 사용할 수 있습니다.  출력할 대상 파일을 지정할 수도 있습니다.  대상 파일을 지정하지 않으면 터미널에 출력됩니다.
```bash
azdata bdc config show [--config-file -c] 
                       [--target -t]  
                       [--json-path -j]  
                       [--force -f]
```
### <a name="examples"></a>예
콘솔에 BDC 구성을 표시합니다.
```bash
azdata bdc config show
```
로컬 구성 파일에서 간단한 json 키 경로의 끝에 있는 값을 가져옵니다.
```bash
azdata bdc config show --config-file custom-config/bdc.json --json-path 'metadata.name' --target section.json
```
로컬 구성 파일에서 서비스 내의 리소스를 가져옵니다.
```bash
azdata bdc config show --config-file custom-config/bdc.json  --json-path '$.spec.services.sql.resources' --target section.json
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--config-file -c`
빅 데이터 클러스터 구성 파일 경로 (예: 사용자 지정/a p i. json)
#### `--target -t`
결과를 저장할 출력 파일입니다. 기본값: stdout으로 전달됩니다.
#### `--json-path -j`
구성에서 원하는 섹션 또는 값으로 이어지는 json 키 경로입니다(즉, key1.key2.key3). jsonpath 쿼리 언어(https://jsonpath.com/ )를 사용합니다. 예: -j ‘$.spec.pools[?(@.spec.type == “Master”)]..endpoints’
#### `--force -f`
대상 파일을 강제로 덮어씁니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-config-add"></a>azdata bdc config add
구성 파일에서 json 경로의 값을 추가합니다.  아래의 모든 예제는 Bash로 제공됩니다.  다른 명령줄을 사용하는 경우 따옴표를 적절하게 이스케이프해야 할 수도 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>예
예 1 - 제어 평면 스토리지를 추가합니다.
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 구성의 빅 데이터 클러스터 구성 파일 경로입니다 (예: custom/bdc. json).
#### `--json-values -j`
값에 해당하는 json 경로의 키-값 쌍 목록입니다. 예: key1.subkey1=value1,key2.subkey2=value2. key=‘{“kind”:“cluster”,“name”:“test-cluster”}’와 같은 인라인 json 값을 제공하거나 key=./values.json과 같은 파일 경로를 제공할 수 있습니다. add는 조건부를 지원하지 않습니다.  제공 하는 인라인 값이 ' = ' 및 ', '를 사용 하는 키 값 쌍 이면 해당 문자를 이스케이프 하십시오.  예를 들면 key1 = "key2\=val2\,key3\=val3"입니다. 경로를 표시하는 방법의 예제는 http://jsonpatch.com/ 을 참조하세요.  배열에 액세스하려는 경우 key.0=value와 같이 인덱스를 지정해야 합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-config-remove"></a>azdata bdc config remove
구성 파일에서 json 경로의 값을 제거합니다.  아래의 모든 예제는 Bash로 제공됩니다.  다른 명령줄을 사용하는 경우 따옴표를 적절하게 이스케이프해야 할 수도 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>예
예 1 - 제어 평면 스토리지를 제거합니다.
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 구성의 빅 데이터 클러스터 구성 파일 경로입니다 (예: custom/bdc. json).
#### `--json-path -j`
jsonpatch 라이브러리를 기준으로, 제거하려는 값을 나타내는 json 경로 목록입니다(예: key1.subkey1,key2.subkey2). remove는 조건부를 지원하지 않습니다. 경로를 표시하는 방법의 예제는 http://jsonpatch.com/ 을 참조하세요.  배열에 액세스하려는 경우 key.0=value와 같이 인덱스를 지정해야 합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-config-replace"></a>azdata bdc config replace
구성 파일에서 json 경로의 값을 바꿉니다.  아래의 모든 예제는 Bash로 제공됩니다.  다른 명령줄을 사용하는 경우 따옴표를 적절하게 이스케이프해야 할 수도 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>예
예 1 - 단일 엔드포인트(컨트롤러 엔드포인트)의 포트를 바꿉니다.
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
예 2 - 제어 평면 스토리지를 바꿉니다.
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ex 3-저장소-0 리소스 사양 (복제본 포함)을 대체 합니다.
```bash
azdata bdc config replace --config-file custom/bdc.json --json-values '$.spec.resources.storage-0.spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 구성의 빅 데이터 클러스터 구성 파일 경로입니다 (예: custom/bdc. json).
#### `--json-values -j`
값에 해당하는 json 경로의 키-값 쌍 목록입니다. 예: key1.subkey1=value1,key2.subkey2=value2. key=‘{“kind”:“cluster”,“name”:“test-cluster”}’와 같은 인라인 json 값을 제공하거나 key=./values.json과 같은 파일 경로를 제공할 수 있습니다. replace는 jsonpath 라이브러리를 통한 조건부를 지원합니다.  이 기능을 사용하려면 경로를 $로 시작합니다. 그러면 -j $.key1.key2[?(@.key3==‘someValue’].key4=value와 같은 조건부를 수행할 수 있습니다. 제공 하는 인라인 값이 ' = ' 및 ', '를 사용 하는 키 값 쌍 이면 해당 문자를 이스케이프 하십시오.  예를 들면 key1 = "key2\=val2\,key3\=val3"입니다. 아래 예제를 참조할 수 있습니다. 추가 도움말을 보려면 https://jsonpath.com/ 을 참조하세요.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-config-patch"></a>azdata bdc config patch
지정된 패치 파일에 따라 구성 파일을 패치합니다. 경로를 작성하는 방법에 대한 자세한 내용은 http://jsonpatch.com/ 을 참조하세요. replace 작업은 jsonpath 라이브러리(https://jsonpath.com/ )를 통해 해당 경로에 조건부를 사용할 수 있습니다. 모든 패치 json 파일은 패치 배열과 해당 작업(추가, 바꾸기, 제거), 경로 및 값을 포함하는 “patch” 키로 시작해야 합니다. “제거” 작업에는 값이 필요하지 않으며 경로만 있으면 됩니다. 다음 예제를 참조하세요.
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>예
예 1 - 패치 파일을 사용하여 단일 엔드포인트(컨트롤러 엔드포인트)의 포트를 바꿉니다.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
예 2 - 패치 파일을 사용하여 제어 평면 스토리지를 바꿉니다.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
예 3 - 패치 파일을 사용하여 복제본(스토리지 풀)을 포함하여 풀 스토리지를 바꿉니다.
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.resources.storage-0.spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 구성의 빅 데이터 클러스터 구성 파일 경로입니다 (예: custom/bdc. json).
#### `--patch-file -p`
jsonpatch 라이브러리(http://jsonpatch.com/ )를 기반으로 하는 패치 json 파일의 경로입니다. 수행하려는 패치 작업의 배열이 값으로 포함된 “patch” 키로 패치 json 파일을 시작해야 합니다. 패치 작업 경로의 경우 대부분의 작업은 key1.key2와 같은 점 표기법을 사용할 수 있습니다. 바꾸기 작업을 수행하고 조건부가 필요한 배열의 값을 바꾸려는 경우 경로를 $로 시작하여 jsonpath 표기법을 사용합니다. 그러면 $.key1.key2[?(@.key3==‘someValue’].key4와 같은 조건부를 수행할 수 있습니다. 다음 예제를 참조하세요. 조건부에 대한 추가 도움말을 보려면 https://jsonpath.com/ 을 참조하세요.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

- 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. 

- **azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.
