---
title: mssqlctl 클러스터 디버그 참조
titleSuffix: SQL Server 2019 big data clusters
description: Mssqlctl 클러스터 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9312e972dfcb439f4ef19a4e72d8d66454622096
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527236"
---
# <a name="mssqlctl-cluster-debug"></a>mssqlctl 클러스터 디버그

다음 문서에 대 한 참조를 제공 합니다 **클러스터 디버그** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a id="commands"></a> 명령

|||
|---|---|
| [copy-logs](#copy-logs) | 로그를 복사 합니다. |
| [dump](#dump) | 트리거 로깅 덤프 합니다. |

## <a id="copy-logs"></a> 디버그 로그 복사 클러스터

로그를 복사 합니다.

```
mssqlctl cluster debug copy-logs
   --namespace
   [--container]
   [--pod]
   [--target-folder]
   [--timeout]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--namespace -n** | Kubernetes 네임 스페이스에 대해 사용 되는 클러스터 이름입니다. 필수 사항입니다. |
| **--container -c** | 로그 복사 비슷한 이름 가진 컨테이너에 대 한 선택 사항이 며 기본적으로 복사 모든 컨테이너에 대 한 로그입니다. 여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다. |
| **--pod -p** | 비슷한 이름의 pod에 대 한 로그를 복사 합니다. 선택 사항입니다. 모든 pod에 대 한 기본 복사 로그 합니다. 여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다. |
| **--target-folder -d** | 로그를 복사할 대상 폴더 경로입니다. 선택 사항이 며 기본적으로 만듭니다 결과 로컬 폴더에 있습니다.  여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다. |
| **--timeout -t** | 명령이 완료 될 때까지 기다리는 시간 (초) 수입니다. 기본값은 0으로 제한 되지 않습니다. |

## <a id="dump"></a> 클러스터 디버그 덤프

트리거 로깅 덤프 합니다.

```
mssqlctl cluster debug dump
   [--container]
   [--namespace]
   --target-folder
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--container -c** | 로그 복사 비슷한 이름 가진 컨테이너에 대 한 선택 사항이 며 기본적으로 복사 모든 컨테이너에 대 한 로그입니다. 여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다.  허용 되는 값: mssql 컨트롤러입니다. |
| **--namespace -n** | Kubernetes 네임 스페이스에 대해 사용 되는 클러스터 이름입니다. 필수 사항입니다. |
| **--target-folder -d** | 로그를 복사할 대상 폴더 경로입니다. 선택 사항이 며 기본적으로 만듭니다 결과 로컬 폴더에 있습니다.  여러 번을 지정할 수 없습니다. 여러 번 지정 하면 마지막으로 인증서가 사용 됩니다.  기본값: `./output/dump`합니다. 필수 사항입니다. |

## <a name="next-steps"></a>다음 단계

다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.