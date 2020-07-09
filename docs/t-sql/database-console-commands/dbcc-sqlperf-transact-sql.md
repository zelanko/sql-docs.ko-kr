---
title: DBCC SQLPERF(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
author: pmasl
ms.author: umajay
ms.openlocfilehash: 4132d5ec459f5fb180ebea94665449cefa7e961a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882007"
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

모든 데이터베이스의 트랜잭션 로그 공간 사용량 통계를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 대기 및 래치 통계를 다시 설정하는데 사용할 수도 있습니다.
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]([일부 지역에서는 미리 보기로 제공](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     | [ "sys.dm_os_latch_stats" , CLEAR ]  
     | [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
LOGSPACE  
트랜잭션 로그의 현재 크기와 각 데이터베이스의 로그 공간 사용 비율을 반환합니다. 이 정보를 사용하여 트랜잭션 로그에 사용된 공간을 모니터링합니다.

> [!IMPORTANT]
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]로 시작하는 트랜잭션 로그의 공간 사용 정보에 대한 자세한 내용은 이 항목의 [설명](#Remarks) 섹션을 참조하세요.
  
**"sys.dm_os_latch_stats"** , CLEAR  
래치 통계를 다시 설정합니다. 자세한 내용은 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)을 참조하세요. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서는 이 옵션을 사용할 수 없습니다.  
  
**"sys.dm_os_wait_stats"** , CLEAR  
대기 통계를 다시 설정합니다. 자세한 내용은 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조하세요. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서는 이 옵션을 사용할 수 없습니다.  
  
WITH NO_INFOMSGS  
심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="result-sets"></a>결과 집합  
 다음 표에서는 결과 집합의 열을 설명합니다.  
  
|열 이름|정의|  
|---|---|
|**데이터베이스 이름**|로그 통계가 표시될 데이터베이스의 이름입니다.|  
|**Log Size (MB)**|로그에 할당된 현재 크기입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 내부 헤더 정보용으로 적은 양의 디스크 공간을 예약하므로 이 값은 원래 로그 공간을 위해 할당된 크기보다 작습니다.|  
|**Log Space Used (%)**|현재 트랜잭션 로그 정보를 저장하는 데 사용 중인 로그 파일의 비율입니다.|  
|**상태**|로그 파일의 상태이며 항상 0입니다.|  
  
## <a name="remarks"></a><a name="Remarks"></a> 주의  
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작하여 `DBCC SQLPERF(LOGSPACE)` 대신에 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) DMV를 사용하여 데이터베이스 당 트랜잭션 로그의 공간 사용 정보를 반환합니다.    
 
트랜잭션 로그는 데이터베이스에서 수행된 각 트랜잭션을 기록합니다. 자세한 내용은 [트랜잭션 로그 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) 및 [SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)을 참조하세요.
  
## <a name="permissions"></a>사용 권한  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 `DBCC SQLPERF(LOGSPACE)`를 실행하려면 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다. 대기 및 래치 통계를 다시 설정하려면 서버에 대한 `ALTER SERVER STATE` 권한이 필요합니다.
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 프리미엄 및 중요 비즈니스용 계층에서 데이터베이스에 대한 `VIEW DATABASE STATE` 권한이 필요합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 표준, 기본 및 범용 계층에서 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 관리자 계정이 필요합니다. 대기 및 래치 통계 재설정은 지원되지 않습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. 모든 데이터베이스에 대한 로그 공간 정보 표시  
다음 예에서는 `LOGSPACE` 인스턴스에 포함된 모든 데이터베이스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 정보를 표시합니다.
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. 대기 통계 다시 설정  
다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 대기 통계를 다시 설정합니다.
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

