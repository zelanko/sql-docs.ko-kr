---
title: sp_dbmmonitorchangealert (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorchangealert_TSQL
- sp_dbmmonitorchangealert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorchangealert
- database mirroring [SQL Server], monitoring
ms.assetid: 1b29f82b-9cf8-4539-8d5c-9a1024db8a50
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41132fa5fd69036e9bc504628cd353d809d6a0bf
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spdbmmonitorchangealert-transact-sql"></a>sp_dbmmonitorchangealert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 미러링 성능 메트릭에 대해 경고 임계값을 추가하거나 변경합니다.  

  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dbmmonitorchangealert database_name   
    , alert_id   
    , alert_threshold   
    , enabled   
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 지정한 경고 임계값을 추가하거나 변경할 데이터베이스를 지정합니다.  
  
 *alert_id*  
 추가되거나 변경될 경고를 식별하는 정수 값입니다. 다음 값 중 하나를 지정합니다.  
  
|Value|성능 메트릭|경고 임계값|  
|-----------|------------------------|-----------------------|  
|1.|보내지 않은 가장 오래된 트랜잭션|주 서버 인스턴스에서 경고가 생성되기까지 Send Queue에 누적될 수 있는 트랜잭션에 해당하는 시간(분)을 지정합니다. 이 경고는 시간을 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 되며 특히 성능 우선 모드와 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 경고는 보호 우선 모드와도 관련이 있습니다.|  
|2|보내지 않은 로그|주 서버 인스턴스에서 경고를 생성하는 보내지 않은 로그 크기(KB)를 지정합니다. 이 경고는 KB를 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 되며 특히 성능 우선 모드와 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 경고는 보호 우선 모드와도 관련이 있습니다.|  
|3|복원되지 않은 로그|미러 서버 인스턴스에서 경고를 생성하는 복원되지 않은 로그 크기(KB)를 지정합니다. 이 경고는 장애 조치(Failover) 시간을 측정하는 데 도움이 됩니다. *장애 조치 시간* 은 주로 이전 미러 서버에서 Redo Queue에 남아 있는 로그를 롤포워드해야 하는 시간과 짧은 추가 시간으로 구성됩니다.|  
|4|미러 커밋 오버헤드|주 서버에서 경고가 생성되기까지 허용되는 트랜잭션당 평균 지연 시간(밀리초)을 지정합니다. 이 지연 시간은 주 서버 인스턴스에서 미리 서버 인스턴스가 트랜잭션 로그 레코드를 Redo Queue에 쓸 때까지 대기하는 동안 발생한 오버헤드 양입니다. 이 값은 보호 우선 모드에만 해당됩니다.|  
|5|보존 기간|데이터베이스 미러링 상태 테이블의 행이 유지되는 기간을 제어하는 메타데이터입니다.|  
  
 경고에 해당 하는 이벤트 Id에 대 한 정보를 참조 하십시오. [미러링 성능 메트릭에 &#40;에 대해 사용 하 여 경고 임계값 및 경고 SQL Server &#41; ](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
 *alert_threshold*  
 경고에 대한 임계값입니다. 미러링 상태를 업데이트할 때 이 임계값 위의 값이 반환되면 Windows 이벤트 로그에 항목이 입력됩니다. 이 값은 성능 메트릭에 따라 KB, 분 또는 밀리초를 나타냅니다.  
  
> [!NOTE]  
>  현재 값을 보려면 실행는 [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md) 저장 프로시저입니다.  
  
 *enabled*  
 경고 사용 여부  
  
 0 = 경고를 사용하지 않습니다.  
  
 1 = 경고를 사용합니다.  
  
> [!NOTE]  
>  보존 기간은 항상 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 각 성능 메트릭에 대한 임계값과 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]데이터베이스의 보존 기간을 설정합니다. 다음 표에서는 이 예에 사용된 값을 보여 줍니다.  
  
|*alert_id*|성능 메트릭|경고 임계값|경고 사용 여부|  
|-----------------|------------------------|-----------------------|-----------------------------|  
|1.|보내지 않은 가장 오래된 트랜잭션|30분|예|  
|2|보내지 않은 로그|10, 000 KB|예|  
|3|복원되지 않은 로그|10, 000 KB|예|  
|4|미러 커밋 오버헤드|1,000밀리초|아니요|  
|5|보존 기간|8시간|예|  
  
```  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 1, 30, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 2, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 3, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 4, 1000, 0 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 5, 8, 1 ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorhelpalert&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitordropalert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
  
