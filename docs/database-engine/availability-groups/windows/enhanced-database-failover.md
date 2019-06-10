---
title: 가용성 그룹에 대해 향상된 데이터베이스 장애 조치 사용
description: Always On 가용성 그룹의 데이터베이스가 더 이상 트랜잭션을 쓸 수 있는 경우 장애 조치(failover)를 트리거하는 향상된 데이터베이스 장애 조치(failover)를 활성화하는 단계입니다.
ms.custom: seodec18
ms.date: 09/25/2017
ms.prod: sql
ms.reviewer: mikeray
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], enhanced database failover
- Availability Groups [SQL Server], failover
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 2d18dde037e9c6dc21ae7c33a84e403451edc1c7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765783"
---
# <a name="enable-enhanced-database-failover-to-a-database-in-an-always-on-availability-group"></a>Always On 가용성 그룹의 데이터베이스에 대해 향상된 데이터베이스 장애 조치(failover) 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2012 및 2014에서 주 복제본의 가용성 그룹에 참여하는 데이터베이스에서 트랜잭션을 쓸 수 있는 기능이 손실되면, 복제본이 동기화되고 자동 장애 조치를 수행하도록 구성되어 있어도 장애 조치가 트리거되지 않습니다.

SQL Server 2016에서는 마법사 또는 Transact-SQL을 사용하여 설정할 수 있는 *확장된 데이터베이스 장애 조치*라는 새로운 선택적 동작을 도입했습니다. 이 옵션을 사용하도록 설정하고 자동 장애 조치를 구성하면 가용성 그룹에 참여하는 하나의 데이터베이스에서 더 이상 트랜잭션을 쓸 수 없게 되면 동기화된 보조 복제본으로 장애 조치가 트리거됩니다.

**시나리오 1**

가용성 그룹은 DB1이라는 단일 데이터베이스를 포함하여 인스턴스 A와 인스턴스 B 간에 구성됩니다. DB1의 데이터 파일은 드라이브 E에 있고, 트랜잭션 로그 파일은 드라이브 F에 있습니다. 가용성 모드는 자동 장애 조치가 포함된 동기 커밋으로 설정됩니다. 새 확장된 데이터베이스 장애 조치 옵션은 가용성 그룹에 구성됩니다. 두 복제본은 현재 동기화된 상태입니다. 드라이브 E에 문제가 있어 실패합니다. 이 시나리오에서는 드라이브 E에 트랜잭션 로그가 없으므로 확장된 데이터베이스 장애 조치가 발생하지 않습니다.  

**시나리오 2**

이 시나리오의 가용성 그룹은 시나리오 1과 동일하게 구성됩니다. Drive E가 실패하는 대신 이번에는 트랜잭션 로그 드라이브인 Drive F가 실패합니다. 이 경우 장애 조치가 트리거됩니다. 확장된 데이터베이스 장애 조치의 조건을 충족하므로 트랜잭션 로그에 연결할 수 없습니다. 즉 데이터베이스에서 트랜잭션을 쓸 수 없습니다.

**시나리오 3**

가용성 그룹은 다음 두 개의 데이터베이스가 포함된 인스턴스 A와 인스턴스 B 간에 구성됩니다. DB1 및 DB2. 가용성 모드는 자동 장애 조치 모드가 포함된 동기 커밋으로 설정되며, 확장된 데이터베이스 장애 조치를 사용하도록 설정됩니다. DB2의 데이터와 트랜잭션 로그 파일을 포함한 디스크에 대한 액세스가 손실됩니다. 문제가 검색되면 가용성 그룹에서 자동으로 인스턴스 B로 장애 조치합니다.

## <a name="configure-and-view-the-enhanced-database-failover-option"></a>확장된 데이터베이스 장애 조치 옵션 구성 및 보기

확장된 데이터베이스 장애 조치는 SQL Server Management Studio 또는 Transact-SQL을 사용하여 구성할 수 있습니다. PowerShell cmdlet에는 현재 이 기능이 없습니다. 확장된 데이터베이스 장애 조치는 기본적으로 사용하지 않도록 설정됩니다.

### <a name="sql-server-management-studio"></a>SQL Server Management Studio

SQL Server Management Studio를 사용하여 내게 필요한 옵션 그룹을 만드는 중에 확장된 데이터베이스 장애 조치를 사용하도록 설정할 수 있습니다. 가용성 그룹을 만든 후에 사용하거나 사용하지 않도록 설정하는 유일한 방법은 Transact-SQL을 사용하는 것입니다.

*수동 가용성 그룹 만들기*

[새 가용성 그룹 대화 상자 사용(SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md) 문서에 나오는 지침을 사용하여 가용성 그룹을 만듭니다. 확장된 데이터베이스 장애 조치를 사용하려면 *데이터베이스 수준 상태 검색* 옆의 확인란을 선택합니다.

*가용성 그룹 마법사 사용*

[가용성 그룹 마법사 사용(SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md) 문서에 나오는 지침을 사용합니다. 확장된 데이터베이스 장애 조치를 사용하도록 설정하는 옵션은 [가용성 그룹 이름 지정] 대화 상자에 있습니다. 사용하려면 *데이터베이스 수준 상태 검색* 옆의 상자를 선택합니다.

### <a name="transact-sql"></a>Transact-SQL

가용성 그룹을 만드는 중에 확장된 데이터베이스 장애 조치 동작을 구성하려면 다음과 같이 DB_FAILOVER를 ON으로 설정해야 합니다.

```SQL
CREATE AVAILABILITY GROUP [AGNAME]
WITH ( DB_FAILOVER = ON)
...
```
가용성 그룹을 구성한 후 이 동작을 추가하려면 다음 ALTER AVAILABILITY GROUP 명령을 사용합니다.
```SQL
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = ON)
```
이 동작을 사용하지 않으려면 다음 ALTER AVAILABILITY GROUP 명령을 실행합니다.
```SQL
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = OFF)
```
### <a name="dynamic-management-view"></a>동적 관리 뷰
가용성 그룹에서 확장된 데이터베이스 장애 조치의 사용 여부를 확인하려면 `sys.availability_groups` 동적 관리 뷰를 쿼리합니다. `db_failover` 열은 확장된 데이터베이스 장애 조치를 사용하지 않는 경우 0, 사용하는 경우 1을 갖습니다. 

## <a name="next-steps"></a>다음 단계 

- [데이터베이스 상태 검색 구성](sql-server-always-on-database-health-detection-failover-option.md)

- [가용성 그룹 마법사 사용(SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

- [새 가용성 그룹 대화 상자 사용(SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
- [Transact-SQL을 사용하여 가용성 그룹 만들기](create-an-availability-group-transact-sql.md)

