---
title: DROP CREDENTIAL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP CREDENTIAL
- DROP_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing credentials
- DROP CREDENTIAL statement
- credentials [SQL Server], DROP CREDENTIAL statement
- authentication [SQL Server], credentials
- deleting credentials
- dropping credentials
ms.assetid: df22c826-317d-45a6-b078-186acb65f71e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ba22628773ece8251c61858b1f2a24d19b4531fb
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361373"
---
# <a name="drop-credential-transact-sql"></a>DROP CREDENTIAL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버에서 자격 증명을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>인수  
 *credential_name*  
 서버에서 제거할 자격 증명의 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 자격 증명 자체를 삭제하지 않고 자격 증명과 연결된 암호를 삭제하려면 [ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md)을 사용합니다.  
  
 자격 증명에 대한 정보는 **sys.credentials** 카탈로그 뷰에 표시됩니다.  
  
> [!WARNING]  
>  프록시는 자격 증명과 연관됩니다. 프록시에 사용되는 자격 증명을 삭제하면 연관된 프록시가 사용할 수 없는 상태가 됩니다. 프록시에 사용되는 자격 증명을 삭제할 때는 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)를 사용하여 프록시를 삭제하고 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)를 사용하여 연관된 프록시를 다시 만드세요.  
  
## <a name="permissions"></a>Permissions  
 ALTER ANY CREDENTIAL 권한이 필요합니다. 시스템 자격 증명을 삭제하는 경우 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Saddles`라는 자격 증명을 제거합니다.  
  
```  
DROP CREDENTIAL Saddles;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
