---
title: azdata bdc 디버그 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc 디버그 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38c327287273ae6596326d88d9e0d67c8e014d47
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426233"
---
# <a name="azdata-bdc-debug"></a>azdata bdc 디버그

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc 디버그** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc 디버그 복사-로그](#azdata-bdc-debug-copy-logs) | 로그를 복사 합니다.
[azdata bdc 디버그 덤프](#azdata-bdc-debug-dump) | 로깅 덤프를 트리거합니다.
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc 디버그 복사-로그
빅 데이터 클러스터에서 디버그 로그를 복사 합니다.-kube config는 시스템에 필요 합니다.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -n`
Kubernetes 네임 스페이스에 사용 되는 빅 데이터 클러스터 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--container -c`
이름이 비슷한 컨테이너의 로그를 복사 하 고, 기본적으로 모든 컨테이너에 대 한 로그를 복사 합니다. 를 여러 번 지정할 수 없습니다. 여러 번 지정 된 경우 마지막 항목을 사용 합니다.
#### `--target-folder -d`
로그를 복사할 대상 폴더 경로입니다. 선택 사항입니다. 기본적으로 로컬 폴더에 결과를 만듭니다.  를 여러 번 지정할 수 없습니다. 여러 번 지정 된 경우 마지막 항목을 사용 합니다.
#### `--pod -p`
유사한 이름으로 pod에 대 한 로그를 복사 합니다. 선택 사항으로, 기본적으로 모든 pod에 대 한 로그를 복사 합니다. 를 여러 번 지정할 수 없습니다. 여러 번 지정 된 경우 마지막 항목을 사용 합니다.
#### `--timeout -t`
명령이 완료 될 때까지 대기 하는 시간 (초)입니다. 기본값은 무제한입니다.
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
## <a name="azdata-bdc-debug-dump"></a>azdata bdc 디버그 덤프
시스템에서 로깅 덤프를 트리거하고 컨테이너 kube 구성에서 복사 해야 합니다.
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -n`
Kubernetes 네임 스페이스에 사용 되는 빅 데이터 클러스터 이름입니다.
#### `--container -c`
이름이 비슷한 컨테이너의 로그를 복사 하 고, 기본적으로 모든 컨테이너에 대 한 로그를 복사 합니다. 를 여러 번 지정할 수 없습니다. 여러 번 지정 된 경우 마지막 항목을 사용 합니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target-folder -d`
로그를 복사할 대상 폴더 경로입니다. 선택 사항입니다. 기본적으로 로컬 폴더에 결과를 만듭니다.  를 여러 번 지정할 수 없습니다. 여러 번 지정 된 경우 마지막 항목을 사용 합니다.`./output/dump`
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
