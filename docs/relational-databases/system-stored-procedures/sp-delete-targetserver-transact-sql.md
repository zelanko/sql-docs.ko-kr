---
title: sp_delete_targetserver (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4dc25d35d1037b3fae934ab6112ea2afdf40ca7a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790385"
---
# <a name="sp_delete_targetserver-transact-sql"></a>sp_delete_targetserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  사용할 수 있는 대상 서버의 목록에서 지정된 서버를 제거합니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>인수  
`[ @server_name = ] 'server'`사용 가능한 대상 서버로 제거할 서버의 이름입니다. *서버* 는 **nvarchar (30)** 이며 기본값은 없습니다.  
  
`[ @clear_downloadlist = ] clear_downloadlist`대상 서버에 대 한 다운로드 목록을 지울지 여부를 지정 합니다. *clear_downloadlist* 형식은 **bit**이며 기본값은 **1**입니다. *Clear_downloadlist* **1**인 경우이 프로시저는 서버를 삭제 하기 전에 서버에 대 한 다운로드 목록을 지웁니다. *Clear_downloadlist* **0**이면 다운로드 목록이 지워지지 않습니다.  
  
`[ @post_defection = ] post_defection`대상 서버에 결함 명령을 게시할 것인지 여부를 지정 합니다. *post_defection* 형식은 **bit**이며 기본값은 1입니다. *Post_defection* **1**인 경우 프로시저는 서버를 삭제 하기 전에 대상 서버에 오류 명령을 게시 합니다. *Post_defection* 가 **0**이면 프로시저에서 대상 서버에 오류 명령을 게시 하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 대상 서버를 삭제 하는 일반적인 방법은 대상 서버에서 **sp_msx_defect** 를 호출 하는 것입니다. 수동 제거를 필요한 경우에만 **sp_delete_targetserver** 을 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자에 게 **sysadmin** 고정 서버 역할을 부여 해야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 사용할 수 있는 작업 서버에서 `LONDON1`이라는 서버를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_help_targetserver &#40;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [Transact-sql&#41;sp_msx_defect &#40;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
