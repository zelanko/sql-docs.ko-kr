---
description: sp_delete_targetsvrgrp_member(Transact-SQL)
title: sp_delete_targetsvrgrp_member (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetsvrgrp_member_TSQL
- sp_delete_targetsvrgrp_member
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetsvrgrp_member
ms.assetid: 178a38d9-9b19-4648-95d7-e1397110d14c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6aae83cbedbacc9175da097ab001fb98780425c4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548128"
---
# <a name="sp_delete_targetsvrgrp_member-transact-sql"></a>sp_delete_targetsvrgrp_member(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  대상 서버 그룹에서 대상 서버를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_targetsvrgrp_member [ @group_name = ] 'group_name' , [ server_name = ] 'server_name'   
```  
  
## <a name="arguments"></a>인수  
`[ @group_name = ] 'group_name'` 그룹의 이름입니다. *group_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @server_name = ] 'server_name'` 지정 된 그룹에서 제거할 서버의 이름입니다. *server_name* 은 **nvarchar (30)** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자에 게 **sysadmin** 고정 서버 역할을 부여 해야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 Servers Maintaining Customer Information 그룹에서 `LONDON1` 서버를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_targetsvrgrp_member   
    @group_name = N'Servers Maintaining Customer Information',  
    @server_name = N'LONDON1';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_targetsvrgrp_member &#40;](../../relational-databases/system-stored-procedures/sp-add-targetsvrgrp-member-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
