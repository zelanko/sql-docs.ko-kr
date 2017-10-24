---
title: DROP ENDPOINT (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_ENDPOINT_TSQL
- DROP ENDPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- removing endpoints
- endpoints [SQL Server], removing
- deleting endpoints
- DROP ENDPOINT statement
- dropping endpoints
ms.assetid: 6aca7412-66a5-4fa4-86b2-061512ff2080
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c823724dbd2f273a161b103b44eb50a77d5f4462
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-endpoint-transact-sql"></a>DROP ENDPOINT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 끝점을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP ENDPOINT endPointName  
```  
  
## <a name="arguments"></a>인수  
 *endPointName*  
 제거할 끝점의 이름입니다.  
  
## <a name="remarks"></a>주의  
 사용자 트랜잭션 내에서 ENDPOINT DDL 문을 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 사용자의 구성원 이어야 합니다.는 **sysadmin** 고정 서버 역할, 끝점, 소유자 또는 해당 끝점에 대 한 CONTROL 권한이 부여 된 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이전에 만든 `sql_endpoint`라는 끝점을 제거합니다.  
  
```  
DROP ENDPOINT sql_endpoint;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

