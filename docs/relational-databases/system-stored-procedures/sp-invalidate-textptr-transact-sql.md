---
title: sp_invalidate_textptr (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_invalidate_textptr_TSQL
- sp_invalidate_textptr
dev_langs:
- TSQL
helpviewer_keywords:
- sp_invalidate_textptr
ms.assetid: dd9920e1-7064-4c05-93d8-9303103fa1d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4409b44a04411357d0109fb643fd13fcff6451b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62960928"
---
# <a name="spinvalidatetextptr-transact-sql"></a>sp_invalidate_textptr(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  트랜잭션에서 지정한 행 내부 텍스트 포인터 또는 모든 행 내부 텍스트 포인터를 무효화합니다. **sp_invalidate_textptr** 행 내부 텍스트 포인터 에서만 사용할 수 있습니다. 이 있는 테이블에서 이러한 포인터는 합니다 **행의 텍스트** 옵션을 사용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_invalidate_textptr [ [ @TextPtrValue = ] textptr_value ]  
```  
  
## <a name="arguments"></a>인수  
`[ @TextPtrValue = ] textptr_value` 행 내부 텍스트 포인터가 무효화 될입니다. *textptr_value* 됩니다 **varbinary (** 16 **)**, 기본값은 NULL입니다. NULL 인 경우 **sp_invalidate_textptr** 트랜잭션에서 모든 행 내부 텍스트 포인터를 무효화 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 트랜잭션, 데이터베이스별로 최대 1,024개의 활성화된 유효 행 내부 텍스트 포인터를 허용합니다. 단, 두 개 이상의 데이터베이스에 걸쳐 있는 트랜잭션은 각 데이터베이스에서 1,024개의 행 내부 텍스트 포인터를 가질 수 있습니다. **sp_invalidate_textptr** 행 내부 텍스트 포인터를 무효화 하 고 따라서 추가 행 내부 텍스트 포인터에 대 한 공간을 사용할 수 있습니다.  
  
 Text in row 옵션에 대 한 자세한 내용은 참조 하세요. [sp_tableoption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_tableoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [TEXTPTR&#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [TEXTVALID&#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)  
  
  
