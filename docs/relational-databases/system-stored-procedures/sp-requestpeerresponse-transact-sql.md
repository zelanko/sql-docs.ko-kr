---
description: sp_requestpeerresponse(Transact-SQL)
title: sp_requestpeerresponse (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b2114460ca878b45bb0b850c066e1fd9356504a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489207"
---
# <a name="sp_requestpeerresponse-transact-sql"></a>sp_requestpeerresponse(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 프로시저는 피어 투 피어 토폴로지의 노드에서 실행될 경우 토폴로지에서 노드를 하나씩 걸러서 응답을 요청합니다. 이 프로시저를 실행하고 해당 응답을 검토함으로써 이전의 모든 명령이 응답하는 노드에 전달되었음을 확인할 수 있습니다. 이 저장 프로시저는 모든 데이터베이스의 요청 노드에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 상태를 확인 하는 피어 투 피어 토폴로지의 게시 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @description = ] 'description'` 개별 상태 요청을 식별 하는 데 사용할 수 있는 사용자 정의 정보입니다. *설명은* **nvarchar (4000)** 이며 기본값은 NULL입니다.  
  
`[ @request_id = ] request_id` 새 요청의 ID를 반환 합니다. *request_id* 은 **int** 이며 OUTPUT 매개 변수입니다. 이 값은 [sp_helppeerresponses &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) 를 실행 하 여 상태 요청에 대 한 모든 응답을 볼 때 사용할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_requestpeerresponse** 은 피어 투 피어 트랜잭션 복제에 사용 됩니다.  
  
 **sp_requestpeerresponse** 은 피어 투 피어 토폴로지에 게시 된 데이터베이스를 복원 하기 전에 다른 모든 노드에서 모든 명령을 수신 했는지 확인 하는 데 사용 됩니다. 노드가 오프라인 상태일 때 변경된 DDL(데이터 정의 언어)이 다른 노드에 도착하는 시점을 예상하기 위해 해당 변경 사항을 복제하는 경우에도 사용됩니다.  
  
 사용자 정의 트랜잭션 내에서는 **sp_requestpeerresponse** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_requestpeerresponse**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;sp_deletepeerrequesthistory &#40;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [Transact-sql&#41;sp_helppeerrequests &#40;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
