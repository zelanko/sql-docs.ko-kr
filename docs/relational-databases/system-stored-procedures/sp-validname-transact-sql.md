---
title: sp_validname (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_validname
- sp_validname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validname
ms.assetid: d51c53c2-1332-407f-b725-4983f2e710eb
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6687528850457d8e0180aab53448d924d1d1f7fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spvalidname-transact-sql"></a>sp_validname(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자 이름을 확인합니다. 모든 진수가 아니고 0이 아닌 데이터를 사용 하 여 저장 될 수 있는 유니코드 데이터를 포함 하는 **nchar**, **nvarchar**, 또는 **ntext** 데이터 형식에 대 한 유효한 문자로 허용 됩니다 식별자 이름입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_validname [@name =] 'name'   
     [, [@raise_error =] raise_error]  
```  
  
## <a name="arguments"></a>인수  
 [ **@name=** ] **'***name***'**  
 이름인는 [식별자](../../relational-databases/databases/database-identifiers.md) 유효성을 확인할 수입니다. *이름* 은 **sysname**, 기본값은 없습니다. *이름* NULL 일 수 없습니다 하 고 빈 문자열일 수 없으며 이진수 0 문자를 포함할 수 없습니다.  
  
 [  **@raise_error=** ] *raise_error*  
 오류를 발생시킬지 여부를 지정합니다. *raise_error* 은 **비트**, 기본값은 1입니다. 이 값은 오류가 표시됨을 의미합니다. 0으로 설정하면 오류 메시지가 발생하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR&#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [nchar 및 nvarchar &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [ntext, text 및 image &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
