---
title: DROP SERVICE (Transact SQL) | Microsoft Docs
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
- DROP_SERVICE_TSQL
- DROP SERVICE
dev_langs:
- TSQL
helpviewer_keywords:
- deleting services
- services [Service Broker], removing
- dropping services
- DROP SERVICE statement
- removing services
ms.assetid: 2351bba7-0f2a-4cda-b3b2-6a88b8747c53
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4eb99ba6a7a5932bdf77df0a7931698ca503c4d7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-service-transact-sql"></a>DROP SERVICE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 서비스를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP SERVICE service_name  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *service_name*  
 삭제할 서비스의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다.  
  
## <a name="remarks"></a>주의  
 서비스를 참조하는 대화 우선 순위가 있으면 해당 서비스를 삭제할 수 없습니다.  
  
 서비스를 삭제하면 해당 서비스가 사용하는 큐에서 서비스에 대한 모든 메시지가 삭제됩니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 해당 서비스를 사용하는 진행 중인 대화의 원격 대화 상대에게 오류를 보냅니다.  
  
## <a name="permissions"></a>Permissions  
 서비스 삭제 권한은 기본적으로 서비스 소유자, db_ddladmin 또는 db_owner 고정 데이터베이스 역할의 멤버 및 sysadmin 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스를 삭제합니다.  
  
```  
DROP SERVICE [//Adventure-Works.com/Expenses] ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER BROKER PRIORITY &#40; Transact SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [서비스 &#40; 변경 Transact SQL &#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [CREATE SERVICE&#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP BROKER PRIORITY &#40; Transact SQL &#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

