---
title: DROP CONTRACT (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- DROP_CONTRACT_TSQL
- DROP CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- dropping contracts
- removing contracts
- deleting contracts
- contracts [Service Broker], dropping
- DROP CONTRACT statement
ms.assetid: fdd0f81e-3c22-4cdf-9416-b4977a6ac3b6
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 58c76223cf592bc90b4c9cb831f93af943e59154
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-contract-transact-sql"></a>DROP CONTRACT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스에서 기존 계약을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP CONTRACT contract_name   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *contract_name*  
 삭제할 계약의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다.  
  
## <a name="remarks"></a>주의  
 서비스 또는 대화 우선 순위에서 참조하는 계약은 삭제할 수 없습니다.  
  
 계약을 삭제하면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 오류로 인해 이 계약을 사용하는 기존 대화가 종료됩니다.  
  
## <a name="permissions"></a>Permissions  
 계약 삭제 권한은 기본적으로 계약 소유자, db_ddladmin 또는 db_owner 고정 데이터베이스 역할의 멤버 및 sysadmin 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스에서 `//Adventure-Works.com/Expenses/ExpenseSubmission` 계약을 제거합니다.  
  
```  
DROP CONTRACT   
    [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER BROKER PRIORITY &#40; Transact SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [서비스 &#40; 변경 Transact SQL &#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [계약 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [DROP BROKER PRIORITY &#40; Transact SQL &#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [DROP 서비스 &#40; Transact SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

