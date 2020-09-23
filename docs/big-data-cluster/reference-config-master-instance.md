---
title: SQL Server 마스터 인스턴스 구성 속성
titleSuffix: SQL Server big data clusters
description: SQL Server 마스터 인스턴스의 구성 속성에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60888246623796d9b4d17c498da47ab4b6557cf2
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790478"
---
# <a name="sql-server-master-instance-configuration-properties"></a>SQL Server 마스터 인스턴스 구성 속성

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

## <a name="properties"></a>속성

배포 시 마스터 인스턴스에 대해 다음과 같은 SQL Server 옵션을 구성할 수 있습니다.

|속성|옵션|
| --- | --- |
|`[sqlagent]`|`enabled = { true | false }` |
|`[telemetry]`|`customerfeedback = { true | false }` |
|`[telemetry]`|`userRequestedLocalAuditDirectory = </path/file>`|
|`[licensing]`| `pid = { Enterprise | Developer }`|
|`[traceflag]`|` traceflag<#> = <####>`|

### <a name="examples"></a>예

다음 예제는 SQL 에이전트, 원격 분석을 사용하도록 설정하고, Enterprise Edition의 PID를 설정하고, 추적 플래그 1204를 사용하도록 설정합니다.

```
[sqlagent]
enabled=true

[telemetry]
customerfeedback=true
userRequestedLocalAuditDirectory = /tmp/audit

[licensing]
pid = Enterprise

[traceflag]
traceflag0 = 1204
```

자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 마스터 인스턴스 구성](configure-sql-server-master-instance.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 마스터 인스턴스 구성](configure-sql-server-master-instance.md)
