---
title: DROP EXTERNAL RESOURCE POOL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL RESOURCE POOL
- DROP_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL RESOURCE POOL statement
ms.assetid: e2fa01bd-96ff-4ea9-bb08-6cb6b6adf68c
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 203413f37f0357749433fef3d7bcc25043b0a4ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="drop-external-resource-pool-transact-sql"></a>DROP EXTERNAL RESOURCE POOL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  외부 프로세스에 대한 리소스를 정의하는 데 사용된 Resource Governor 외부 리소스 풀을 삭제합니다. R 서비스에 대해 외부 풀은 `rterm.exe`, `BxlServer.exe` 및 이들에 의해 생성된 기타 프로세스를 제어합니다. 외부 리소스 풀은 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)를 사용하여 만들어지고 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)를 사용하여 수정됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
## <a name="arguments"></a>인수  
 *pool_name*  
 삭제될 외부 리소스 풀 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 작업 그룹이 들어 있으면 해당 외부 리소스 풀을 삭제할 수 없습니다.  
  
 리소스 관리자 기본 풀 또는 내부 풀을 삭제할 수 없습니다.  
  
 재구성이 n을 합니다  
  
 DDL 문을 실행할 경우 리소스 관리자 상태에 대해 잘 알고 있는 것이 좋습니다. 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 `CONTROL SERVER` 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `ex_pool`이라는 외부 리소스 풀을 삭제합니다.  
  
```  
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [External Scripts Enabled 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [SQL Server R Services의 알려진 문제](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)  
  
  
