---
title: sp_dbmmonitorhelpalert (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorhelpalert_TSQL
- sp_dbmmonitorhelpalert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorhelpalert
- database mirroring [SQL Server], monitoring
ms.assetid: 43911660-b4e4-4934-8c02-35221160aaec
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 40fe5e8e82d1a4e7b4f2f32d55f27b191d9aee8b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760157"
---
# <a name="sp_dbmmonitorhelpalert-transact-sql"></a>sp_dbmmonitorhelpalert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  여러 가지 주요 데이터베이스 미러링 모니터 성능 메트릭 중 하나 또는 모두에 대한 경고 임계값 정보를 반환합니다.  
 
  ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dbmmonitorhelpalert database_name   
    [ , alert_id ]   
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 데이터베이스를 지정합니다.  
  
 [ *alert_id* ]  
 반환될 경고를 식별하는 정수 값입니다. 이 인수를 생략하면 모든 경고가 반환되지만 보존 기간은 반환되지 않습니다.  
  
 특정 경고를 반환하려면 다음 값 중 하나를 지정합니다.  
  
|값|성능 메트릭|경고 임계값|  
|-----------|------------------------|-----------------------|  
|1|보내지 않은 가장 오래된 트랜잭션|주 서버 인스턴스에서 경고가 생성되기까지 Send Queue에 누적될 수 있는 트랜잭션에 해당하는 시간(분)을 지정합니다. 이 경고는 시간을 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 되며 특히 성능 우선 모드와 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 경고는 보호 우선 모드와도 관련이 있습니다.|  
|2|보내지 않은 로그|주 서버 인스턴스에서 경고를 생성하는 보내지 않은 로그 크기(KB)를 지정합니다. 이 경고는 KB를 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 되며 특히 성능 우선 모드와 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 경고는 보호 우선 모드와도 관련이 있습니다.|  
|3|복원되지 않은 로그|미러 서버 인스턴스에서 경고를 생성하는 복원되지 않은 로그 크기(KB)를 지정합니다. 이 경고는 장애 조치(Failover) 시간을 측정하는 데 도움이 됩니다. *장애 조치 시간* 은 주로 이전 미러 서버에서 Redo Queue에 남아 있는 로그를 롤포워드해야 하는 시간과 짧은 추가 시간으로 구성됩니다.|  
|4|미러 커밋 오버헤드|주 서버에서 경고가 생성되기까지 허용되는 트랜잭션당 평균 지연 시간(밀리초)을 지정합니다. 이 지연 시간은 주 서버 인스턴스에서 미리 서버 인스턴스가 트랜잭션 로그 레코드를 Redo Queue에 쓸 때까지 대기하는 동안 발생한 오버헤드 양입니다. 이 값은 보호 우선 모드에만 해당됩니다.|  
|5|보존 기간|데이터베이스 미러링 상태 테이블의 행이 유지되는 기간을 제어하는 메타데이터입니다.|  
  
 경고에 해당 하는 이벤트 Id에 대 한 자세한 내용은 [SQL Server&#41;&#40;미러링 성능 메트릭에 대해 경고 임계값 및 경고 사용 ](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)을 참조 하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
 반환되는 각 경고에 대해 다음 열이 포함된 행을 반환합니다.  
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|**alert_id**|**int**|아래 표에서는 각 성능 메트릭에 대 한 **alert_id** 값과 **sp_dbmmonitorresults** 결과 집합에 표시 되는 메트릭의 측정 단위를 나열 합니다.|  
|**threshold**|**int**|경고에 대한 임계값입니다. 미러링 상태를 업데이트할 때 이 임계값 위의 값이 반환되면 Windows 이벤트 로그에 항목이 입력됩니다. 이 값은 경고에 따라 KB, 분 또는 밀리초를 나타냅니다. 임계값이 현재 설정되어 있지 않으면 이 값은 NULL입니다.<br /><br /> **참고:** 현재 값을 보려면 [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md) 저장 프로시저를 실행 합니다.|  
|**사용**|**bit**|0 = 이벤트를 사용할 수 없습니다.<br /><br /> 1 = 이벤트를 사용할 수 있습니다.<br /><br /> **참고:** 보존 기간을 항상 사용 하도록 설정 합니다.|  
  
|값|성능 메트릭|단위|  
|-----------|------------------------|----------|  
|1|보내지 않은 가장 오래된 트랜잭션|분|  
|2|보내지 않은 로그|KB|  
|3|복원되지 않은 로그|KB|  
|4|미러 커밋 오버헤드|밀리초|  
|5|보존 기간|시간|  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 보내지 않은 가장 오래된 트랜잭션 성능 메트릭에 대한 경고의 사용 여부를 나타내는 행을 반환합니다.  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012, 1 ;  
```  
  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서의 사용 여부를 나타내는 행을 각 성능 메트릭에 대해 반환합니다.  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 &#40;SQL Server&#41;모니터링](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Transact-sql&#41;sp_dbmmonitorchangealert &#40;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [Transact-sql&#41;sp_dbmmonitorchangemonitoring &#40;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [Transact-sql&#41;sp_dbmmonitordropalert &#40;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [Transact-sql&#41;sp_dbmmonitorupdate &#40;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)   
 [Transact-sql&#41;sp_dbmmonitorhelpmonitoring &#40;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
