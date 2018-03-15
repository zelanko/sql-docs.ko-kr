---
title: DROP WORKLOAD GROUP(Transact-SQL) | Microsoft Docs
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
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
ms.assetid: 1cd68450-5b58-4106-a2bc-54197ced8616
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5211e91f9bd1e6dc8dd49676c024b3356163538
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 사용자 정의 리소스 관리자 작업 그룹을 삭제합니다.  
  
 ![토픽 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "토픽 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP WORKLOAD GROUP group_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *group_name*  
 기존 사용자 정의 작업 그룹의 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 DROP WORKLOAD GROUP 문은 리소스 관리자 내부 그룹 또는 기본 그룹에서 사용할 수 없습니다.  
  
 DDL 문을 실행할 경우 리소스 관리자 상태에 대해 잘 알고 있는 것이 좋습니다. 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.  
  
 작업 그룹에 활성 세션이 있으면 변경 내용을 적용하기 위해 ALTER RESOURCE GOVERNOR RECONFIGURE 문이 호출될 경우 작업 그룹을 삭제하거나 다른 리소스 풀에 이동할 수 없습니다. 다음 동작 중 하나를 수행하여 이 문제를 방지할 수 있습니다.  
  
-   적용된 그룹에서 모든 세션의 연결이 끊어질 때까지 기다린 후 ALTER RESOURCE GOVERNOR RECONFIGURE 문을 다시 실행합니다.  
  
-   KILL 명령을 사용하여 적용된 그룹의 세션을 명시적으로 중지한 후 ALTER RESOURCE GOVERNOR RECONFIGURE 문을 다시 실행합니다.  
  
-   서버를 다시 시작합니다. 다시 시작 프로세스가 완료되면 삭제한 그룹은 생성되지 않고 이동한 그룹은 새 리소스 풀 할당을 사용합니다.  
  
-   DROP WORKLOAD GROUP 문을 발행했지만 변경 내용을 적용하기 위해 세션을 명시적으로 중지하지 않을 경우 DROP 문을 발행하기 이전의 이름을 사용하여 그룹을 다시 만든 다음 해당 그룹을 원래 리소스 풀로 이동할 수 있습니다. 변경 내용을 적용하려면 ALTER RESOURCE GOVERNOR RECONFIGURE 문을 실행합니다.  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `adhoc`라는 작업 그룹을 삭제합니다.  
  
```  
DROP WORKLOAD GROUP adhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [관리](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
