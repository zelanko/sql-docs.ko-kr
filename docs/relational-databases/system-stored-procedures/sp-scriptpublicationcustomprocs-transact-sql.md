---
title: sp_scriptpublicationcustomprocs (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32d983a52ab15444024e7762eba73572671da4c6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spscriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자 지정 프로시저 스키마 자동 생성 옵션을 사용하는 게시의 모든 테이블 아티클에 대한 사용자 지정 INSERT, UPDATE 및 DELETE 프로시저를 스크립팅합니다. **sp_scriptpublicationcustomprocs** 구독 스냅숏이 수동으로 적용을 설정 하는 데 특히 유용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication**=] **'***publication_name***'**  
 게시의 이름입니다. *publication_name* 은 **sysname** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 단일으로 구성 된 결과 집합을 반환 **nvarchar (4000)** 열입니다. 결과 집합은 사용자 지정 저장 프로시저를 만드는 데 필요한 완전한 CREATE PROCEDURE 문을 이룹니다.  
  
## <a name="remarks"></a>주의  
 사용자 지정 프로시저(0x2) 스키마 자동 생성 옵션을 사용하지 않으면 아티클에 대해 사용자 지정 프로시저가 스크립팅되지 않습니다.  
  
 다음 절차에서 사용 **sp_scriptpublicationcustomprocs** 구독자 프로시저를 만들 수 및 직접 실행할 수는 없습니다.  
  
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
  
## <a name="permissions"></a>Permissions  
 실행 권한이 부여 되었습니다 **공용**;의 멤버에 대 한 액세스를 제한 하려면이 저장된 프로시저 내에서 프로시저 보안 검사가 수행 되는 **sysadmin** 고정된 서버 역할 및 **db_ 소유자** 현재 데이터베이스의 고정된 데이터베이스 역할입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
