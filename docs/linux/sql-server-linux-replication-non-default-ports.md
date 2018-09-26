---
title: Linux에서 스냅숏 폴더 공유 SQL Server 복제 구성 | Microsoft Docs
description: 이 문서에서는 Linux에서 스냅숏 폴더 공유 SQL Server 복제를 구성 하는 방법을 설명 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 9/24/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6dd5887f4db97ae4d8f52103fd29403e7eb4c51e
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715472"
---
# <a name="configure-replication-with-non-default-ports"></a>기본이 아닌 포트를 사용 하 여 복제를 구성 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Network.tcpport mssql conf 설정을 사용 하 여 구성 된 모든 포트에서 수신 대기 하는 Linux 인스턴스에서 SQL Server를 사용 하 여 복제를 구성할 수 있습니다. 포트는 다음 조건이 true 인 경우 구성 하는 동안 서버 이름에 추가 해야 합니다.

1. 복제 설정에서는 Linux의 SQL Server의 인스턴스
2. 모든 인스턴스 (Windows 또는 Linux)가 기본이 아닌 포트에서 수신 합니다. 

인스턴스의 서버 이름을 @ 실행 하 여 있습니다@servername 인스턴스에서 합니다.

## <a name="examples"></a>예

'Server1' linux 1,500 포트에서 수신 대기합니다. 'Server1' 배포를 구성 하려면 `sp_adddistributor` 사용 하 여 `@distributor`입니다. 예를 들어: 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' linux 1,500 포트에서 수신 대기합니다. 배포자에 대 한 게시자를 구성 하려면 `sp_adddistpublisher` 사용 하 여 `@publisher`입니다. 예를 들어:

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' linux 6549 포트에서 수신합니다. 'Server2'를 구독자로 구성 하려면 `sp_addsubscription` 사용 하 여 `@subscriber`입니다. 예를 들어:

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' Server3의 서버 이름과 MSSQL2017의 인스턴스 이름을 사용 하 여 Windows에서 6549 포트에서 수신합니다. 'Server3'를 구독자로 구성 하려면 다음을 실행 합니다 `sp_addsubscription` 사용 하 여 `@subscriber`입니다. 예를 들어:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>다음 단계

[Linux에서 SQL Server 복제 개념:](sql-server-linux-replication.md)

[복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)합니다.

