---
title: sp_invalidate_textptr (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 81df88f6e451d71dc5778e49162db97def7ed27d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68113188"
---
# <a name="sp_invalidate_textptr-transact-sql"></a>sp_invalidate_textptr(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  트랜잭션에서 지정한 행 내부 텍스트 포인터 또는 모든 행 내부 텍스트 포인터를 무효화합니다. **sp_invalidate_textptr** 은 행 내부 텍스트 포인터에만 사용할 수 있습니다. 이러한 포인터는 **text in row** 옵션을 사용 하는 테이블에서 가져온 것입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_invalidate_textptr [ [ @TextPtrValue = ] textptr_value ]  
```  
  
## <a name="arguments"></a>인수  
`[ @TextPtrValue = ] textptr_value`무효화 될 행 내부 텍스트 포인터입니다. *textptr_value* 는 **varbinary (** 16 **)** 이며 기본값은 NULL입니다. NULL 인 경우 **sp_invalidate_textptr** 는 트랜잭션의 모든 행 내부 텍스트 포인터를 무효화 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 트랜잭션, 데이터베이스별로 최대 1,024개의 활성화된 유효 행 내부 텍스트 포인터를 허용합니다. 단, 두 개 이상의 데이터베이스에 걸쳐 있는 트랜잭션은 각 데이터베이스에서 1,024개의 행 내부 텍스트 포인터를 가질 수 있습니다. **sp_invalidate_textptr** 를 사용 하 여 행 내부 텍스트 포인터를 무효화할 수 있으므로 추가 행 내부 텍스트 포인터를 위한 여유 공간이 확보 됩니다.  
  
 text in row 옵션에 대한 자세한 내용은 [sp_tableoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 참조하십시오.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_tableoption &#40;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [TEXTPTR &#40;Transact-sql&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [TEXTVALID&#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)  
  
  
