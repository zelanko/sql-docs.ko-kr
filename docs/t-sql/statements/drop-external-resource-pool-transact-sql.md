---
title: "외부 리소스 풀 (Transact SQL) DROP | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0aae6de75280fb0e32879ece5acea6d0fd94f3c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-resource-pool-transact-sql"></a>DROP 외부 리소스 풀 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  외부 프로세스에 대 한 리소스를 정의 하는 데 사용 하는 리소스 관리자 외부 리소스 풀을 삭제 합니다. R 서비스에 대 한 외부 풀 제어 `rterm.exe`, `BxlServer.exe`, 및 생성 된 다른 프로세스입니다. 사용 하 여 외부 리소스 풀이 만들어집니다 [외부 리소스 풀 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-resource-pool-transact-sql.md) 를 사용 하 여 수정할 [ALTER EXTERNAL RESOURCE pool&#40; Transact SQL &#41; ](../../t-sql/statements/alter-external-resource-pool-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
## <a name="arguments"></a>인수  
 *pool_name 이라*  
 삭제할 외부 리소스 풀의 이름입니다.  
  
## <a name="remarks"></a>주의  
 작업 그룹을 포함 하는 경우에 외부 리소스 풀을 삭제할 수 없습니다.  
  
 리소스 관리자 기본 풀 또는 내부 풀을 삭제할 수 없습니다.  
  
 재구성이 않습니다 n  
  
 DDL 문을 실행할 경우 리소스 관리자 상태에 대해 잘 알고 있는 것이 좋습니다. 자세한 내용은 참조 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 `CONTROL SERVER` 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이라는 외부 리소스 풀을 삭제 `ex_pool`합니다.  
  
```  
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [external scripts enabled 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [SQL Server R Services에 대 한 알려진된 문제](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [외부 RESOURCE pool&#40; 변경 Transact SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [DROP RESOURCE pool&#40; Transact SQL &#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)  
  
  

