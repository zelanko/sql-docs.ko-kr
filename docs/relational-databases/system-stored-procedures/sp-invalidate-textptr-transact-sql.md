---
title: sp_invalidate_textptr (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_invalidate_textptr_TSQL
- sp_invalidate_textptr
dev_langs:
- TSQL
helpviewer_keywords:
- sp_invalidate_textptr
ms.assetid: dd9920e1-7064-4c05-93d8-9303103fa1d6
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77b48427c017b543d73bf93e03a09fd7c4d50c78
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spinvalidatetextptr-transact-sql"></a>sp_invalidate_textptr(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  트랜잭션에서 지정한 행 내부 텍스트 포인터 또는 모든 행 내부 텍스트 포인터를 무효화합니다. **sp_invalidate_textptr** 행 내부 텍스트 포인터에만 사용할 수 있습니다. 이 있는 테이블에서 이러한 포인터는는 **행의 텍스트에에서** 옵션을 사용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_invalidate_textptr [ [ @TextPtrValue = ] textptr_value ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@TextPtrValue=** ] *textptr_value*  
 무효화될 행 내부 텍스트 포인터입니다. *textptr_value* 은 **varbinary (**16**)**, 기본값은 NULL입니다. NULL 인 경우 **sp_invalidate_textptr** 트랜잭션의 모든 행 내부 텍스트 포인터를 무효화 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 트랜잭션, 데이터베이스별로 최대 1,024개의 활성화된 유효 행 내부 텍스트 포인터를 허용합니다. 단, 두 개 이상의 데이터베이스에 걸쳐 있는 트랜잭션은 각 데이터베이스에서 1,024개의 행 내부 텍스트 포인터를 가질 수 있습니다. **sp_invalidate_textptr** 는 행 내부 텍스트 포인터를 무효화 하 고 추가 행 내부 텍스트 포인터에 대 한 공간을 확보 하는 데 사용할 수 있습니다.  
  
 Text in row 옵션에 대 한 자세한 내용은 참조 [sp_tableoption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_tableoption & #40; Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [TEXTPTR&#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [TEXTVALID&#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)  
  
  
