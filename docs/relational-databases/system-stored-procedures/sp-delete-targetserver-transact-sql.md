---
title: sp_delete_targetserver (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 63b8fdb66b868d7fc0c1c7a83d574bafb92224b6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692251"
---
# <a name="spdeletetargetserver-transact-sql"></a>sp_delete_targetserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용할 수 있는 대상 서버의 목록에서 지정된 서버를 제거합니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@server_name=** ] **'***server***'**  
 사용할 수 있는 대상 서버에서 제거할 서버의 이름입니다. *서버* 됩니다 **nvarchar(30)**, 기본값은 없습니다.  
  
 [  **@clear_downloadlist=** ] *clear_downloadlist*  
 대상 서버의 다운로드 목록을 지울 것인지 여부를 지정합니다. *clear_downloadlist* 형식인 **bit**, 기본값은 **1**합니다. 때 *clear_downloadlist* 됩니다 **1**, 프로시저는 서버를 삭제 하기 전에 서버의 다운로드 목록을 지웁니다. 때 *clear_downloadlist* 됩니다 **0**, 다운로드 목록이 지워지지 않습니다.  
  
 [  **@post_defection=** ] *post_defection*  
 제거 명령을 대상 서버에 게시할 것인지 여부를 지정합니다. *post_defection* 형식인 **비트**, 기본값은 1입니다. 때 *post_defection* 됩니다 **1**, 프로시저는 서버를 삭제 하기 전에 제거 명령을 대상 서버에 게시 합니다. 때 *post_defection* 됩니다 **0**, 절차 제거 명령을 대상 서버에 게시 하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 대상 서버를 삭제 하는 일반적인 방법은 호출 하는 것 **sp_msx_defect** 대상 서버에서. 사용 하 여 **sp_delete_targetserver** 은 수동으로 제거 해야 하는 데 필요한 경우에 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장된 프로시저를 실행 하려면 사용자에 부여 해야 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용할 수 있는 작업 서버에서 `LONDON1`이라는 서버를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>참고자료  
 [sp_help_targetserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
