---
title: sp_scriptpublicationcustomprocs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8436616ced84892dc7e484a5d83f3f0c3779f244
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771578"
---
# <a name="sp_scriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  사용자 지정 프로시저 스키마 자동 생성 옵션을 사용하는 게시의 모든 테이블 아티클에 대한 사용자 지정 INSERT, UPDATE 및 DELETE 프로시저를 스크립팅합니다. **sp_scriptpublicationcustomprocs** 는 스냅숏이 수동으로 적용 되는 구독을 설정 하는 데 특히 유용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication_name'`게시의 이름입니다. *publication_name* 는 **sysname** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 단일 **nvarchar (4000)** 열로 구성 된 결과 집합을 반환 합니다. 결과 집합은 사용자 지정 저장 프로시저를 만드는 데 필요한 완전한 CREATE PROCEDURE 문을 이룹니다.  
  
## <a name="remarks"></a>설명  
 사용자 지정 프로시저(0x2) 스키마 자동 생성 옵션을 사용하지 않으면 아티클에 대해 사용자 지정 프로시저가 스크립팅되지 않습니다.  
  
 다음 절차는 **sp_scriptpublicationcustomprocs** 에서 구독자를 만드는 프로시저를 만드는 데 사용 되며 직접 실행 해서는 안 됩니다.  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>사용 권한  
 Execute 권한은 **public**에 부여 됩니다. 이 저장 프로시저 내에서 프로시저 보안 검사를 수행 하 여 **sysadmin** 고정 서버 역할의 멤버에 대 한 액세스를 제한 하 고 현재 데이터베이스의 고정 데이터베이스 역할을 **db_owner** 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
