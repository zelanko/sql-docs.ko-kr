---
title: sp_dbmmonitoraddmonitoring (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitoraddmonitoring
- sp_dbmmonitoraddmonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], monitoring
- sp_dbmmonitoraddmonitoring
ms.assetid: 9489dc30-af29-4363-a172-4645947fc95e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4ed53c6a72b201129cf9f75214261bbdd47d6fb9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68108148"
---
# <a name="sp_dbmmonitoraddmonitoring-transact-sql"></a>sp_dbmmonitoraddmonitoring(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 인스턴스의 모든 미러된 데이터베이스에 대한 미러링 상태를 정기적으로 업데이트하는 데이터베이스 미러링 모니터 작업을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dbmmonitoraddmonitoring [ update_period ]  
```  
  
## <a name="arguments"></a>인수  
 *update_period*  
 업데이트 간격(분)을 지정합니다. 1분에서 120분 사이의 값을 지정할 수 있습니다. 기본값은 1분입니다.  
  
> [!NOTE]  
>  업데이트 기간을 너무 짧게 설정하면 클라이언트에 대한 응답 시간이 느려질 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 이 프로시저를 사용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 서버 인스턴스에서 실행될 수 있어야 하며 데이터베이스 미러링 모니터 작업을 실행하려면 에이전트가 실행되고 있어야 합니다.  
  
 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]데이터베이스 미러링을 시작 하면 **sp_dbmmonitoraddmonitoring** 프로시저가 자동으로 실행 됩니다. ALTER DATABASE 문을 사용 하 여 수동으로 미러링을 시작 하는 경우 서버 인스턴스에서 미러된 데이터베이스를 모니터링 하려면 **sp_dbmmonitoraddmonitoring** 를 수동으로 실행 해야 합니다.  
  
> [!NOTE]  
>  데이터베이스 미러링을 설정 하기 전에 **sp_dbmmonitoraddmonitoring** 를 실행 하면 모니터링 작업이 실행 되지만 데이터베이스 미러링 모니터 기록이 저장 되는 상태 테이블은 업데이트 되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 업데이트 기간을 `3`분으로 지정하여 모니터링을 시작합니다.  
  
```  
EXEC sp_dbmmonitoraddmonitoring 3;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 &#40;SQL Server&#41;모니터링](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Transact-sql&#41;sp_dbmmonitorchangemonitoring &#40;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [Transact-sql&#41;sp_dbmmonitordropmonitoring &#40;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [Transact-sql&#41;sp_dbmmonitorhelpmonitoring &#40;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
