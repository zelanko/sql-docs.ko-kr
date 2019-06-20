---
title: mssqlctl 클러스터 디버그 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 디버그 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4eafc3838d153a2616e34e98aed041374c04292d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779395"
---
# <a name="mssqlctl-cluster-debug"></a>mssqlctl 클러스터 디버그

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터 디버그** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl cluster debug copy-logs](#mssqlctl-cluster-debug-copy-logs) | 로그를 복사 합니다.
[mssqlctl 클러스터 디버그 덤프](#mssqlctl-cluster-debug-dump) | 트리거 로깅 덤프 합니다.
## <a name="mssqlctl-cluster-debug-copy-logs"></a>mssqlctl cluster debug copy-logs
클러스터에서 디버그 로그를 복사-kube 구성 시스템에 필요 합니다.
```bash
mssqlctl cluster debug copy-logs --namespace -n 
                                 [--container -c]  
                                 [--target-folder -d]  
                                 [--pod -p]  
                                 [--timeout -t]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -n`
Kubernetes 네임 스페이스에 대해 사용 되는 클러스터 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--container -c`
로그 복사 비슷한 이름 가진 컨테이너에 대 한 선택 사항이 며 기본적으로 복사 모든 컨테이너에 대 한 로그입니다. 여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다.
#### `--target-folder -d`
로그를 복사할 대상 폴더 경로입니다. 선택 사항이 며 기본적으로 만듭니다 결과 로컬 폴더에 있습니다.  여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다.
#### `--pod -p`
비슷한 이름의 pod에 대 한 로그를 복사 합니다. 선택 사항입니다. 모든 pod에 대 한 기본 복사 로그 합니다. 여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다.
#### `--timeout -t`
명령이 완료 될 때까지 기다리는 시간 (초) 수입니다. 기본값은 0으로 제한 되지 않습니다.
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
## <a name="mssqlctl-cluster-debug-dump"></a>mssqlctl 클러스터 디버그 덤프
컨테이너에서 복사 및 로깅 덤프 트리거-kube 구성 시스템에 필요 합니다.
```bash
mssqlctl cluster debug dump --namespace -n 
                            --container -c  
                            [--target-folder -d]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -n`
Kubernetes 네임 스페이스에 대해 사용 되는 클러스터 이름입니다.
#### `--container -c`
로그 복사 비슷한 이름 가진 컨테이너에 대 한 선택 사항이 며 기본적으로 복사 모든 컨테이너에 대 한 로그입니다. 여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target-folder -d`
로그를 복사할 대상 폴더 경로입니다. 선택 사항이 며 기본적으로 만듭니다 결과 로컬 폴더에 있습니다.  여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다. `./output/dump`
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