---
title: mssqlctl 클러스터 구성 섹션 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 구성 섹션 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e0c4f543f349d166962e65ea91338595d25308ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800959"
---
# <a name="mssqlctl-cluster-config-section"></a>mssqlctl 클러스터 구성 섹션

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터 구성 섹션** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl 클러스터 구성 섹션 show](#mssqlctl-cluster-config-section-show) | 구성 파일의 섹션을 가져옵니다.
[mssqlctl 클러스터 구성 섹션 집합](#mssqlctl-cluster-config-section-set) | 구성 파일에 대 한 섹션을 설정합니다.
## <a name="mssqlctl-cluster-config-section-show"></a>mssqlctl 클러스터 구성 섹션 show
지정 된 json 경로 따라 선택한 구성 파일에서 지정된 된 섹션을 가져옵니다.
```bash
mssqlctl cluster config section show --json-path -j 
                                     --config-file -c  
                                     [--target -t]  
                                     [--force -f]
```
### <a name="examples"></a>예
간단한 json 키 경로 끝에 값을 가져옵니다.
```bash
mssqlctl cluster config section show --config-file custom-config.json --json-path 'metadata.name' --target section.json
```
조건부를 사용 하 여 json 키 경로 끝에 값을 가져옵니다.
```bash
mssqlctl cluster config section show --config-file custom-config.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--json-path -j`
즉, key1.key2.key3 config 파일에서 섹션을 원하는 값을 발생 시키는 json 키 경로입니다. Jsonpath 쿼리 언어를 사용 하 여 https://github.com/h2non/jsonpath-ng 예:-j ' $. spec.pools [? ( @.spec.type "마스터" = =)]... 끝점 '
#### `--config-file -c`
클러스터 구성 파일 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target -t`
저장할 섹션 파일의 파일 경로 배치 합니다. 기본값: stdout으로 전송 합니다.
#### `--force -f`
대상 파일의 덮어쓰기를 강제 합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-cluster-config-section-set"></a>mssqlctl 클러스터 구성 섹션 집합
지정 된 json 경로 따라 선택한 구성 파일에 지정된 된 섹션을 설정합니다.  모든 examplesbelow Bash에서 제공 됩니다.  다른 명령줄을 사용 하는 경우 주의 하십시오는 해야 할 수 있습니다 escapequotations 적절 하 게 합니다.  또는 패치 파일 기능을 사용할 수 있습니다.
```bash
mssqlctl cluster config section set --config-file -c 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="examples"></a>예
예 (인라인)-1 단일 끝점 (컨트롤러 끝점)의 포트를 설정 합니다.
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values '$.spec.controlPlane.spec.endpoints[?(@.name=="Controller")].port=30080'
```
예 1 (패치)-패치 파일을 사용 하 여 단일 끝점 (컨트롤러 끝점)의 포트를 설정 합니다.
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
2 (인라인)-집합 제어 평면 저장소 예입니다.
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values 'spec.controlPlane.spec.storage=spec.controlPlane.spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
패치 파일을 사용 하 여 제어 평면 저장소 집합 (patch)-2 예입니다.
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"spec.controlPlane.spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
3(inline)-ex (저장소 풀) 복제본을 포함 하는 풀 저장소를 설정 합니다.
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
예 3 (patch)-패치 파일을 사용 하 여 (저장소 풀) 복제본을 포함 하는 풀 저장소를 설정 합니다.
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -c`
설정 하려는 클러스터 구성의 구성 파일 경로
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--json-values -j`
Json 경로 값의 키 값 쌍 목록을: key1.subkey1=value1,key2.subkey2=value2 합니다. 제공할 수 있습니다 인라인 json 값과 같은: 키 ='{"kind": "클러스터", "name": "테스트 클러스터"}' 또는 key=./values.json 등의 파일 경로 제공 합니다. 조건부를 필요한 값을 설정 하려는 경우 경로 $로 시작 하 여 jsonpath 표기를 사용 하세요. 이렇게 하면 $ 조건부-j 등을 할 수 있습니다. key1.key2 [? ( @.key3'someValue' = =].key4 = value입니다. 아래 예제를 볼 수 있습니다. 추가적인 도움말이 필요한 경우 다음을 참조 하세요. https://jsonpath.com/
#### `--patch-file -p`
Jsonpatch 라이브러리를 기반으로 하는 패치 json 파일에 대 한 경로: http://jsonpatch.com/ 합니다. 값인 수행 하고자 하는 패치 작업의 배열 "패치" 이라고 하는 키를 사용 하 여 패치 json 파일을 시작 해야 합니다. 패치 작업의 경로 대해 대부분의 작업에 대 한 key1.key2 같은 점 표기법을 사용할 수 있습니다. 바꾸기 작업을 수행 하려는 경우 필요한 조건부 배열에서 값을 대체 하는 경로 $로 시작 하 여 jsonpath 표기를 사용 하세요. 이렇게 하면 $ 같은 조건부 작업을 수행 하 합니다. key1.key2 [? ( @.key3'someValue' = =].key4 합니다. 아래 예제를 참조 하세요. 추가 도움말을 참조 하세요. https://jsonpath.com/ 합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.

## <a name="next-steps"></a>다음 단계

다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.