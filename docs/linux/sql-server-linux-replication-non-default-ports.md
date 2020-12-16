---
title: 복제 스냅샷 폴더 구성(기본이 아닌 포트)
titleSuffix: SQL Server on Linux
description: Linux에서 기본이 아닌 포트를 SQL Server 복제에 사용하여 스냅샷 폴더 공유를 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: ce4e17be837794382435c8a5369ef92a44a5b91a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471504"
---
# <a name="configure-replication-with-non-default-ports-sql-server-linux"></a>기본이 아닌 포트를 사용하여 복제 구성(SQL Server Linux)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

network.tcpport mssql-conf 설정을 통해 구성된 임의 포트에서 수신 대기하는 SQL Server on Linux 인스턴스를 사용하여 복제를 구성할 수 있습니다. 다음 조건에 해당하는 경우 구성 중에 포트를 서버 이름에 추가해야 합니다.

1. 복제 설정에 SQL Server on Linux 인스턴스가 포함됩니다.
2. 기본 포트가 아닌 포트에서 수신 대기하는 인스턴스(Windows 또는 Linux)가 있습니다. 

인스턴스의 서버 이름은 인스턴스에서 @@servername을 실행하여 확인할 수 있습니다. 서버 이름 대신 IP 주소를 사용하지 마세요. 게시자, 배포자 또는 구독자의 IP 주소를 사용하면 오류가 발생할 수 있습니다.

> [!NOTE]
> Linux에서 기본 포트가 아닌 포트를 사용하여 SQL Server 복제본을 만드는 것은 SQL Server 2019 이상에서만 가능합니다.

## <a name="examples"></a>예제

‘Server1’은 Linux의 포트 1500에서 수신 대기합니다. 배포에 대해 ‘Server1’을 구성하려면 `@distributor`와 함께 `sp_adddistributor`를 실행합니다. 예를 들면 다음과 같습니다. 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

‘Server1’은 Linux의 포트 1500에서 수신 대기합니다. 배포자에 대해 게시자를 구성하려면 `@publisher`와 함께 `sp_adddistpublisher`를 실행합니다. 예를 들면 다음과 같습니다.

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

‘Server2’는 Linux의 포트 6549에서 수신 대기합니다. ‘Server2’를 구독자로 구성하려면 `@subscriber`와 함께 `sp_addsubscription`을 실행합니다. 예를 들면 다음과 같습니다.

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

‘Server3’은 Windows의 포트 6549에서 수신 대기하며, 서버 이름은 Server3이고 인스턴스 이름은 MSSQL2017입니다. ‘Server3’을 구독자로 구성하려면 `@subscriber`와 함께 `sp_addsubscription`을 실행합니다. 예를 들면 다음과 같습니다.

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>다음 단계

[개념: Linux의 SQL Server 복제](sql-server-linux-replication.md)

[복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)

