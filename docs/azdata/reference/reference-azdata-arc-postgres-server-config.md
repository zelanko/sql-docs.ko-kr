---
title: azdata arc postgres server config 참조
titleSuffix: SQL Server big data clusters
description: azdata arc postgres server config 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e63a0374ee93b34d3824a4d6e5c9341ba1176ee6
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942893"
---
# <a name="azdata-arc-postgres-server-config"></a>azdata arc postgres server config

`azdata`에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata arc postgres server config init](#azdata-arc-postgres-server-config-init) | PostgreSQL 서버 그룹의 CRD 및 사양 파일을 초기화합니다.
[azdata arc postgres server config add](#azdata-arc-postgres-server-config-add) | 구성 파일에서 json 경로의 값을 추가합니다.
[azdata arc postgres server config remove](#azdata-arc-postgres-server-config-remove) | 구성 파일에서 json 경로의 값을 제거합니다.
[azdata arc postgres server config replace](#azdata-arc-postgres-server-config-replace) | 구성 파일에서 json 경로의 값을 바꿉니다.
[azdata arc postgres server config patch](#azdata-arc-postgres-server-config-patch) | json 패치 파일을 기준으로 구성 파일을 패치합니다.
## <a name="azdata-arc-postgres-server-config-init"></a>azdata arc postgres server config init
PostgreSQL 서버 그룹의 CRD 및 사양 파일을 초기화합니다.
```bash
azdata arc postgres server config init --path -p 
                                       [--engine-version -ev]
```
### <a name="examples"></a>예
PostgreSQL 서버 그룹의 CRD 및 사양 파일을 초기화합니다.
```bash
azdata arc postgres server config init --path ./template
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
PostgreSQL 서버 그룹의 CRD 및 사양을 기록할 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--engine-version -ev`
11 또는 12여야 합니다. 기본 값은 12입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-arc-postgres-server-config-add"></a>azdata arc postgres server config add
구성 파일에서 json 경로의 값을 추가합니다.  아래의 모든 예제는 Bash로 제공됩니다.  다른 명령줄을 사용하는 경우 따옴표를 적절하게 이스케이프해야 할 수도 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata arc postgres server config add --path -p 
                                      --json-values -j
```
### <a name="examples"></a>예제
예제 1 - 스토리지를 추가합니다.
```bash
azdata arc postgres server config add --path custom/spec.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
사용자 지정 리소스 사양의 경로(즉, custom/spec.json)입니다.
#### `--json-values -j`
값에 해당하는 json 경로의 키-값 쌍 목록입니다. 예: key1.subkey1=value1,key2.subkey2=value2. key=‘{“kind”:“cluster”,“name”:“test-cluster”}’와 같은 인라인 json 값을 제공하거나 key=./values.json과 같은 파일 경로를 제공할 수 있습니다. add는 조건부를 지원하지 않습니다.  지정한 인라인 값이 “=”와 “,”를 포함하는 키-값 쌍인 경우 해당 문자를 이스케이프합니다.  (예: key1="key2\=val2\,key3\=val3") 경로를 표시하는 방법의 예제는 http://jsonpatch.com/ 을 참조하세요.  배열에 액세스하려는 경우 key.0=value와 같이 인덱스를 지정해야 합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-arc-postgres-server-config-remove"></a>azdata arc postgres server config remove
구성 파일에서 json 경로의 값을 제거합니다.  아래의 모든 예제는 Bash로 제공됩니다.  다른 명령줄을 사용하는 경우 따옴표를 적절하게 이스케이프해야 할 수도 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata arc postgres server config remove --path -p 
                                         --json-path -j
```
### <a name="examples"></a>예제
예제 1 - 스토리지를 제거합니다.
```bash
azdata arc postgres server config remove --path custom/spec.json --json-path ".spec.storage"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
사용자 지정 리소스 사양의 경로(즉, custom/spec.json)입니다.
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
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-arc-postgres-server-config-replace"></a>azdata arc postgres server config replace
구성 파일에서 json 경로의 값을 바꿉니다.  아래의 모든 예제는 Bash로 제공됩니다.  다른 명령줄을 사용하는 경우 따옴표를 적절하게 이스케이프해야 할 수도 있습니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
azdata arc postgres server config replace --path -p 
                                          --json-values -j
```
### <a name="examples"></a>예제
예제 1 - 단일 엔드포인트의 포트를 바꿉니다.
```bash
azdata arc postgres server config replace --path custom/spec.json --json-values "$.spec.endpoints[?(@.name=="Controller")].port=30080"
```
예제 2 - 스토리지를 바꿉니다.
```bash
azdata arc postgres server config replace --path custom/spec.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
사용자 지정 리소스 사양의 경로(즉, custom/spec.json)입니다.
#### `--json-values -j`
값에 해당하는 json 경로의 키-값 쌍 목록입니다. 예: key1.subkey1=value1,key2.subkey2=value2. key=‘{“kind”:“cluster”,“name”:“test-cluster”}’와 같은 인라인 json 값을 제공하거나 key=./values.json과 같은 파일 경로를 제공할 수 있습니다. replace는 jsonpath 라이브러리를 통한 조건부를 지원합니다.  이 기능을 사용하려면 경로를 $로 시작합니다. 그러면 -j $.key1.key2[?(@.key3==“someValue”].key4=value와 같은 조건부를 수행할 수 있습니다. 지정한 인라인 값이 “=”와 “,”를 포함하는 키-값 쌍인 경우 해당 문자를 이스케이프합니다.  (예: key1="key2\=val2\,key3\=val3") 아래 예제를 참조할 수 있습니다. 추가 도움말을 보려면 https://jsonpath.com/ 을 참조하세요.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-arc-postgres-server-config-patch"></a>azdata arc postgres server config patch
지정된 패치 파일에 따라 구성 파일을 패치합니다. 경로를 작성하는 방법에 대한 자세한 내용은 http://jsonpatch.com/ 을 참조하세요. replace 작업은 jsonpath 라이브러리(https://jsonpath.com/ )를 통해 해당 경로에 조건부를 사용할 수 있습니다. 모든 패치 json 파일은 패치 배열과 해당 작업(추가, 바꾸기, 제거), 경로 및 값을 포함하는 “patch” 키로 시작해야 합니다. “제거” 작업에는 값이 필요하지 않으며 경로만 있으면 됩니다. 다음 예제를 참조하세요.
```bash
azdata arc postgres server config patch --path -p 
                                        --patch-file
```
### <a name="examples"></a>예제
예제 1 - 패치 파일을 사용하여 단일 엔드포인트의 포트를 바꿉니다.
```bash
azdata arc postgres server config patch --path custom/spec.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=="Controller")].port","value":30080}]}
```
예제 2 - 패치 파일을 사용하여 스토리지를 바꿉니다.
```bash
azdata arc postgres server config patch --path custom/spec.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
사용자 지정 리소스 사양의 경로(즉, custom/spec.json)입니다.
#### `--patch-file`
jsonpatch 라이브러리(http://jsonpatch.com/ )를 기반으로 하는 패치 json 파일의 경로입니다. 수행하려는 패치 작업의 배열이 값으로 포함된 “patch” 키로 패치 json 파일을 시작해야 합니다. 패치 작업 경로의 경우 대부분의 작업은 key1.key2와 같은 점 표기법을 사용할 수 있습니다. 바꾸기 작업을 수행하고 조건부가 필요한 배열의 값을 바꾸려는 경우 경로를 $로 시작하여 jsonpath 표기법을 사용합니다. 그러면 $.key1.key2[?(@.key3==“someValue”].key4와 같은 조건부를 수행할 수 있습니다. 다음 예제를 참조하세요. 조건부에 대한 추가 도움말을 보려면 https://jsonpath.com/ 을 참조하세요.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. 

**azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata 설치](..\install\deploy-install-azdata.md)를 참조하세요.

