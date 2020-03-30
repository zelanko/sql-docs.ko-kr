---
title: 데이터베이스 상태 | Microsoft 문서
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.DATABASESTATES.F1
helpviewer_keywords:
- emergency database state [SQL Server]
- verifying database states
- viewing database states
- displaying database states
- database states [SQL Server]
- current database state
- offline database state [SQL Server]
- suspect database state
- recovery pending database state [SQL Server]
- states [SQL Server], databases
- online database state
- states [SQL Server]
- restoring database state [SQL Server]
ms.assetid: b7f1f111-ca73-4a89-b567-a98d64d6ecb3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1aa8519092b90f34089cd2c31441b51b2b0da014
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68109688"
---
# <a name="database-states"></a>데이터베이스 상태
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  데이터베이스는 항상 하나의 특정한 상태에 있습니다. 예를 들어 ONLINE, OFFLINE 또는 SUSPECT 상태일 수 있습니다. 데이터베이스의 현재 상태를 확인하려면 **sys.databases** 카탈로그 뷰의 [state_desc](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 열이나 **DATABASEPROPERTYEX** 함수의 [Status](../../t-sql/functions/databasepropertyex-transact-sql.md) 속성을 선택합니다.  
  
## <a name="database-state-definitions"></a>데이터베이스 상태 정의  
 다음 표에서는 데이터베이스 상태를 정의합니다.  
  
|시스템 상태|정의|  
|-----------|----------------|  
|ONLINE|데이터베이스에 액세스할 수 있습니다. 복구의 실행 취소 단계가 완료되지 않은 경우에도 주 파일 그룹은 온라인 상태입니다.|  
|OFFLINE|데이터베이스를 사용할 수 없습니다. 명시적 사용자 동작으로 인해 데이터베이스가 오프라인 상태가 되어 추가 사용자 동작이 수행될 때까지 오프라인 상태로 있습니다. 예를 들어 파일을 새 디스크로 이동하기 위해 데이터베이스를 오프라인으로 설정할 수 있습니다. 이러한 경우 이동이 완료되면 데이터베이스가 온라인 상태로 돌아옵니다.|  
|RESTORING|주 파일 그룹에서 하나 이상의 파일을 복원하고 있거나 하나 이상의 보조 파일이 오프라인 상태에서 복원되고 있습니다. 데이터베이스를 사용할 수 없습니다.|  
|RECOVERING|데이터베이스가 복구되고 있습니다. 복구 중 과정은 일시적 상태입니다. 복구가 성공하면 데이터베이스는 자동으로 온라인 상태가 됩니다. 복구가 실패하면 데이터베이스는 주의 대상 상태가 됩니다. 데이터베이스를 사용할 수 없습니다.|  
|RECOVERY PENDING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 복구 중 리소스 관련 오류가 발생했습니다. 데이터베이스가 손상되지는 않았지만 파일이 누락되었거나 시스템 리소스 제한으로 인해 데이터베이스를 시작할 수 없습니다. 데이터베이스를 사용할 수 없습니다. 오류를 해결하고 복구 프로세스를 완료하기 위한 사용자의 추가적인 동작이 필요합니다.|  
|SUSPECT|주 파일 그룹이 주의 대상이거나 손상되었을 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작하는 동안에는 데이터베이스를 복구할 수 없습니다. 데이터베이스를 사용할 수 없습니다. 문제를 해결하기 위한 사용자의 추가적인 동작이 필요합니다.|  
|EMERGENCY|사용자가 데이터베이스를 변경하고 응급 상태로 설정했습니다. 데이터베이스가 단일 사용자 모드에 있고 복구 또는 복원되었을 수 있습니다. 데이터베이스가 READ_ONLY로 표시되고 로깅이 비활성화되며 **sysadmin** 고정 서버 역할의 멤버로 액세스가 제한됩니다. EMERGENCY는 주로 문제 해결을 위해 사용됩니다. 예를 들어 주의 대상으로 표시된 데이터베이스를 응급 상태로 설정할 수 있습니다. 이렇게 하면 시스템 관리자가 데이터베이스에 읽기 전용으로 액세스할 수 있습니다. **sysadmin** 고정 서버 역할의 멤버만 데이터베이스를 응급 상태로 설정할 수 있습니다.|  
  
## <a name="related-content"></a>관련 내용  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [미러링 상태&#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [파일 상태](../../relational-databases/databases/file-states.md)  
  
  
