---
title: mssqlctl 클러스터 구성 섹션 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 구성 섹션 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5a793e7d0fcaf782a09a4981491ef0a8d90ab5a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759140"
---
# <a name="mssqlctl-cluster-config-section"></a>mssqlctl 클러스터 구성 섹션

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터 구성 섹션** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl 클러스터 구성 섹션에서 가져오기](#mssqlctl-cluster-config-section-get) | 구성 파일의 섹션을 가져옵니다.
[mssqlctl 클러스터 구성 섹션 집합](#mssqlctl-cluster-config-section-set) | 구성 파일에 대 한 섹션을 설정합니다.
## <a name="mssqlctl-cluster-config-section-get"></a>mssqlctl 클러스터 구성 섹션에서 가져오기
지정 된 json 경로 따라 선택한 구성 파일에서 지정된 된 섹션을 가져옵니다.
```bash
mssqlctl cluster config section get --json-path -j 
                                    --config-file -f  
                                    [--target -t]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--json-path -j`
즉, key1.key2.key3 config 파일에서 섹션을 원하는 값을 발생 시키는 json 키 경로입니다. Jsonpath 쿼리 언어를 사용 하 여 https://github.com/h2non/jsonpath-ng예:-j ' $. spec.pools [? ( @.spec.type "마스터" = =)]... 끝점 '
#### `--config-file -f`
클러스터 구성 파일 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target -t`
저장할 섹션 파일의 파일 경로 배치 합니다.
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
지정 된 json 경로 따라 선택한 구성 파일에 지정된 된 섹션을 설정합니다.
```bash
mssqlctl cluster config section set --config-file -f 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--config-file -f`
설정 하려는 클러스터 구성의 구성 파일 경로
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--json-values -j`
Json 경로 값의 키 값 쌍 목록을: key1.subkey1=value1,key2.subkey2=value2 합니다. 제공할 수 있습니다 인라인 json 값 예: 키 ='{"kind": "클러스터", "name": "테스트 클러스터"}' key=./values.json 등의 파일 경로 제공 하거나
#### `--patch-file -p`
Jsonpath 고 jsonpatch 라이브러리를 기반으로 하는 패치 json 파일에 대 한 경로: https://github.com/stefankoegl/python-json-patch , https://github.com/h2non/jsonpath-ng -간단한 예제: {"패치": [{"op": "add", "path": "metadata.name", "value": "테스트"}, {"op": "add", "path": "metadata.array", "value": [1, 2, 3]}]} "패치" 키를 포함 하 고 패치를 확인 하려는 배열 값을 가질 하세요.  따라서 실행 됩니다. A more complex example: {"patch": [{"op": "replace", "path": "$.spec.pools[?(@.spec.type == 'Master')]..endpoints","value": {"name": "새 끝점"}}]}
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