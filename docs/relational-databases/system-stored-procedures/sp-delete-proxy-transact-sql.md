---
title: sp_delete_proxy (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_proxy
- sp_delete_proxy_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_delete_proxy
- DROP PROXY statement
ms.assetid: 44a1db13-b7f2-4dab-a1b5-b8dafb41737c
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 433d4030b22cfa211348f9a42b3be0f868ad62ba
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spdeleteproxy-transact-sql"></a>sp_delete_proxy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 프록시를 제거합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_proxy [ @proxy_id = ] id , [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>인수  
 [  **@proxy_id** =] *id*  
 제거할 프록시의 프록시 ID입니다. *proxy_id* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@proxy_name** =] **'***proxy_name***'**  
 제거할 프록시의 이름입니다. *proxy_name* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 어느  **@proxy_name**  또는  **@proxy_id**  지정 해야 합니다. 두 인수가 모두 지정될 경우 두 인수는 같은 프록시를 참조해야 합니다. 그렇지 않으면 저장 프로시저가 실패합니다.  
  
 작업 단계가 지정된 프록시를 참조할 경우 해당 프록시는 삭제할 수 없으며 저장 프로시저가 실패합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만 기본적으로는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_delete_proxy**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Catalog application proxy`라는 프록시를 삭제합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_proxy &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
  
  
