---
title: sp_resync_targetserver (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_resync_targetserver
- sp_resync_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resync_targetserver
ms.assetid: 40e44df7-d3e3-44ee-b149-08aba629a21f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6aa435a7c0a65634323f6c3f90874cd3694fa876
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816850"
---
# <a name="sp_resync_targetserver-transact-sql"></a>sp_resync_targetserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 대상 서버에서 모든 다중 서버 작업을 다시 동기화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_resync_targetserver  
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>인수  
`[ @server_name = ] 'server'`다시 동기화 할 서버의 이름입니다. *server* 은 **sysname**이며 기본값은 없습니다. **All** 을 지정 하면 모든 대상 서버가 다시 동기화 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 **Sp_post_msx_operation** 작업의 결과를 보고 합니다.  
  
## <a name="remarks"></a>설명  
 **sp_resync_targetserver** 대상 서버에 대 한 현재 명령 집합을 삭제 하 고 대상 서버에서 다운로드할 새 집합을 게시 합니다. 새로운 집합은 모든 다중 서버를 삭제하는 명령과 서버에서 현재 대상이 되는 각 작업에 대한 삽입으로 구성됩니다.  
  
## <a name="permissions"></a>권한  
 이 프로시저를 실행할 수 있는 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `SEATTLE1` 대상 서버를 다시 동기화합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_resync_targetserver  
    N'SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_help_downloadlist &#40;](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)   
 [Transact-sql&#41;sp_post_msx_operation &#40;](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
