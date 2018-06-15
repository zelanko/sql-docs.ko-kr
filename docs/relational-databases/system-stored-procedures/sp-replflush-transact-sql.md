---
title: sp_replflush (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replflush
- sp_replflush_TSQL
helpviewer_keywords:
- sp_replflush
ms.assetid: 20809f5f-941d-427f-8f0c-de7a6c487584
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bfab78fd3cbb9fb6750c7259ab2c0efd20b23006
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32997590"
---
# <a name="spreplflush-transact-sql"></a>sp_replflush(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  아티클 캐시를 플러시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  이 프로시저를 수동으로 실행할 필요는 없습니다. **sp_replflush** 숙련 된 복제 지원 전문가 지시에 따라 복제 문제를 해결 하는 것에 대 한만 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replflush  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_replflush** 트랜잭션 복제에 사용 됩니다.  
  
 아티클 정의는 효율성을 높이기 위해 캐시에 저장됩니다. **sp_replflush** 아티클 정의가 수정 되거나 삭제 될 때마다 다른 복제 저장 프로시저에 사용 됩니다.  
  
 하나의 클라이언트 연결만 지정된 데이터베이스로의 로그 판독기 액세스를 가질 수 있습니다. 실행 하는 클라이언트에 데이터베이스에 대 한 로그 판독기 액세스를 경우 **sp_replflush** 발생 하면 클라이언트의 액세스가 해제 합니다. 다른 클라이언트가 사용 하 여 트랜잭션 로그를 검색할 수 있습니다 **sp_replcmds** 또는 **sp_replshowcmds**합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_replflush**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_repltrans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
