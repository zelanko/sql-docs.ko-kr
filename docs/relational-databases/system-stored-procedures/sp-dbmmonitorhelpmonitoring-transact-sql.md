---
description: sp_dbmmonitorhelpmonitoring(Transact-SQL)
title: sp_dbmmonitorhelpmonitoring (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorhelpmonitoring
- sp_dbmmonitorhelpmonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorhelpmonitoring
- database mirroring [SQL Server], monitoring
ms.assetid: a085cf87-269f-454a-a146-21f80a113b72
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dd82681731ab29068c2a951850da9f2ad225742b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548168"
---
# <a name="sp_dbmmonitorhelpmonitoring-transact-sql"></a>sp_dbmmonitorhelpmonitoring(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 업데이트 기간을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dbmmonitorhelpmonitoring   
```  
  
## <a name="arguments"></a>인수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
 현재 업데이트 기간, 즉 데이터베이스 미러링 상태 테이블에 대한 업데이트 간격(분)을 반환합니다. 1분에서 120분 사이의 값입니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 업데이트 기간을 반환합니다.  
  
```  
EXEC sp_dbmmonitorhelpmonitoring;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorresults&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
