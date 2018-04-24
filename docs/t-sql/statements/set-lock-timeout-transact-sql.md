---
title: SET LOCK_TIMEOUT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LOCK_TIMEOUT_TSQL
- SET_LOCK_TIMEOUT_TSQL
- SET LOCK_TIMEOUT
- LOCK_TIMEOUT
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- releasing locks
- LOCK_TIMEOUT option
- SET LOCK_TIMEOUT statement
- locking [SQL Server], time-outs
- wait time for lock releases [SQL Server]
ms.assetid: dd0c389e-956d-435e-bf71-e16624a0a215
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7707e2f47f2da6f789d151c24c6117e1ec1774cd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="set-locktimeout-transact-sql"></a>SET LOCK_TIMEOUT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  잠금이 해제될 때가지 문이 기다려야 할 시간(밀리초)을 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SET LOCK_TIMEOUT timeout_period  
```  
  
## <a name="arguments"></a>인수  
 *timeout_period*  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 잠금 오류를 반환할 때까지 기다리는 시간을 밀리초 단위로 지정한 숫자입니다. -1(기본값)은 제한 시간이 없음(무기한 대기)을 나타냅니다.  
  
 기다리는 시간이 제한 시간 값을 초과하면 오류가 반환됩니다. 0은 기다리지 않음을 나타내고 잠금이 있으면 바로 오류 메시지가 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 연결을 시작할 때는 이 설정이 -1로 되어 있습니다. 이 값을 변경하면 연결의 나머지 부분에서는 새 설정 값이 적용됩니다.  
  
 SET LOCK_TIMEOUT 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
 이 SET 옵션 대신 READPAST 잠금 참고를 사용할 수도 있습니다.  
  
 CREATE DATABASE, ALTER DATABASE 및 DROP DATABASE 문은 SET LOCK_TIMEOUT 설정을 인식하지 못합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>1. 잠금 시간 제한을 1800 밀리초로 설정  
 다음 예에서는 잠금 제한 시간을 `1800`밀리초로 설정합니다.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>2. 잠금이 해제될 때까지 계속 대기하도록 잠금 제한 시간을 설정합니다.  
 다음 예제에서는 잠금 대기 시간을 무기한 대기하고 만료되지 않도록 설정합니다. 이는 각 연결이 시작될 때 이미 설정된 기본 동작입니다.  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 다음 예에서는 잠금 제한 시간을 `1800`밀리초로 설정합니다. 이 릴리스에서는 [!INCLUDE[ssDW](../../includes/ssdw-md.md)]이 문을 성공적으로 구문 분석하지만 값 1800을 무시하고 기본 동작을 계속 사용합니다.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>참고 항목  
 [@@LOCK_TIMEOUT&#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

