---
title: mssqlctl 클러스터 구성 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 57b77e83994f8471e677ba2ba367acc48a66cddd
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860024"
---
# <a name="mssqlctl-cluster-config"></a>mssqlctl 클러스터 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터 구성** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a id="commands"></a> 명령

|||
|---|---|
| [get](#get) | 클러스터를 가져옵니다. |

## <a id="get"></a> mssqlctl cluster config get

클러스터를 가져옵니다.

```
mssqlctl cluster config get
   --name
   --output-file
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--name -n** | Kubernetes 네임 스페이스에 대해 사용 되는 클러스터 이름입니다. 필수 사항입니다. |
| **--output-file -f** | 출력 파일에 결과 저장할입니다. 필수 사항입니다. |

## <a name="next-steps"></a>다음 단계

다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.