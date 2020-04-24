---
title: READTEXT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- READTEXT_TSQL
- READTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- column reading [SQL Server]
- READTEXT statement
- reading columns
ms.assetid: 91b69853-1381-4306-8343-afdb73105738
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8fde97db271ccd0307d0af75ea0c7d4aacad9703
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634799"
---
# <a name="readtext-transact-sql"></a>READTEXT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**text**, **ntext** 또는 **image** 열에서 **text**, **ntext** 또는 **image** 값을 읽습니다. 지정한 오프셋에서 읽기 시작하여 지정한 바이트 수만큼 읽습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [SUBSTRING](../../t-sql/functions/substring-transact-sql.md) 함수를 사용합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>인수  
_table_ **.** _column_  
읽을 테이블과 열의 이름입니다. 테이블 및 열 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 테이블 및 열 이름은 반드시 지정해야 하지만 데이터베이스 이름과 소유자 이름을 지정하는 것은 선택적입니다.  
  
_text\_ptr_  
유효한 텍스트 포인터입니다. _text\_ptr_은 **binary(16)** 이어야 합니다.  
  
_offset_  
**text** 또는 **image** 데이터 형식을 사용하는 경우 바이트 수입니다. **text**, **image** 또는 **ntext** 데이터를 읽기 전에 건너뛰기 위해 **ntext** 데이터 형식을 사용하는 경우 문자의 바이트 수일 수도 있습니다.  
  
_size_**text** 또는 **image** 데이터 형식을 사용하는 경우 바이트 수입니다. 데이터를 읽기 위해 **ntext** 데이터 형식을 사용하는 경우 문자의 바이트 수일 수도 있습니다. _size_가 0이면 4KB의 데이터를 읽습니다.  
  
HOLDLOCK  
트랜잭션이 끝날 때까지 텍스트 값을 읽을 수 없게 잠급니다. 다른 사용자는 값을 읽을 수 있지만 수정할 수는 없습니다.  
  
## <a name="remarks"></a>설명  
유효한 [text](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)ptr _값을 얻으려면 \_TEXTPTR_ 함수를 사용합니다. TEXTPTR은 지정된 행에 **text**, **ntext** 또는 **image** 열에 대한 포인터를 반환합니다. TEXTPTR은 쿼리에서 둘 이상의 행을 반환하는 경우 반환되는 마지막 행에 **text**, **ntext** 또는 **image** 열에 대한 포인터를 반환할 수도 있습니다. TEXTPTR은 16바이트 이진 문자열을 반환하므로 지역 변수를 선언하여 텍스트 포인터를 보유한 다음 READTEXT로 해당 변수를 사용하는 것이 좋습니다. 지역 변수 선언 방법에 대한 자세한 내용은 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)을 참조하십시오.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 행 내부 텍스트 포인터가 있을 수 있지만 유효하지 않습니다. **text in row** 옵션에 대한 자세한 내용은 [sp_tableoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 참조하십시오. 텍스트 포인터를 무효화하는 방법은 [sp_invalidate_textptr&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)를 참조하십시오.  
  
@@TEXTSIZE 함수의 값은 READTEXT에 대해 지정한 크기보다 작을 경우 READTEXT에 대해 지정한 크기를 대체합니다. @@TEXTSIZE 함수는 SET TEXTSIZE 문에서 설정된 반환되는 데이터 바이트 수의 한도를 지정합니다. TEXTSIZE의 세션 설정 방법에 대한 자세한 내용은 [SET TEXTSIZE&#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
지정한 테이블에 대한 SELECT 권한이 있는 사용자에게 기본적으로 READTEXT 권한이 부여됩니다. SELECT 권한을 위임하는 경우에는 READTEXT 권한도 위임할 수 있습니다.  
  
## <a name="examples"></a>예  
다음 예에서는 `pr_info` 테이블에 있는 `pub_info` 열의 문자를 두 번째 문자부터 26번째 문자까지 읽습니다.  
  
> [!NOTE]  
>  이 예를 실행하려면 **pubs** 예제 데이터베이스를 설치해야 합니다.  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr INNER JOIN publishers p  
      ON pr.pub_id = p.pub_id   
      AND p.pub_name = 'New Moon Books'  
READTEXT pub_info.pr_info @ptrval 1 25;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[@@TEXTSIZE&#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
[UPDATETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
[WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
