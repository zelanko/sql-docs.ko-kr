---
title: UPDATETEXT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATETEXT
- UPDATETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text updates [SQL Server]
- updating data [SQL Server]
- data updates [SQL Server], UPDATETEXT statement
- UPDATETEXT statement
ms.assetid: d73c28ee-3972-4afd-af8d-ebbbd9e50793
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49bd324f97f6ba1d2e8a8120bb502199b4ca0f06
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="updatetext-transact-sql"></a>UPDATETEXT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 업데이트 **텍스트**, **ntext**, 또는 **이미지** 필드입니다. UPDATETEXT를 사용 하 여의 일부를 변경 하는 **텍스트**, **ntext**, 또는 **이미지** 있던 열입니다. WRITETEXT를 사용 하 여 업데이트 하 고 전체 대체 **텍스트**, **ntext**, 또는 **이미지** 필드입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]큰 값 데이터 형식을 사용 하 고 **.** WRITE 절을는 [업데이트](../../t-sql/queries/update-transact-sql.md) 문 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATETEXT [BULK] { table_name.dest_column_name dest_text_ptr }  
  { NULL | insert_offset }  
     { NULL | delete_length }  
     [ WITH LOG ]  
     [ inserted_data  
    | { table_name.src_column_name src_text_ptr } ]  
```  
  
## <a name="arguments"></a>인수  
 BULK  
 이진 데이터 스트림을 업로드하기 위해 업로드 도구를 사용합니다. 스트림은 도구가 TDS 프로토콜 수준에서 제공해야 합니다. 데이터 스트림이 없으면 쿼리 프로세서는 BULK 옵션을 무시합니다.  
  
> [!IMPORTANT]  
>  BULK 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기반 응용 프로그램에서 사용하지 않는 것이 좋습니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 버전에서 변경 또는 제거될 수 있습니다.  
  
 *table_name* **합니다.** *dest_column_name*  
 테이블의 이름 및 **텍스트**, **ntext**, 또는 **이미지** 열을 업데이트할 수 있습니다. 테이블 이름, 열 이름에 대 한 규칙을 사용 하 여 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. 필요에 따라 데이터베이스 이름과 소유자 이름을 지정할 수 있습니다.  
  
 *dest_text_ptr*  
 텍스트 포인터를 가리키는 값 (TEXTPTR 함수에서 반환)는 **텍스트**, **ntext**, 또는 **이미지** 데이터를 업데이트 합니다. *dest_text_ptr* 해야 **이진 (**16**)**합니다.  
  
 *insert_offset*  
 업데이트의 경우 0부터 시작하는 시작 위치입니다. 에 대 한 **텍스트** 또는 **이미지** 열 *insert_offset* 기존 열의 처음부터 새 데이터를 삽입 하기 전에 건너뛸 바이트 수입니다. 에 대 한 **ntext** 열 *insert_offset*문자 수가 됩니다 (각 **ntext** 2 바이트를 사용 하는 문자)입니다. 기존 **텍스트**, **ntext**, 또는 **이미지** 이 0부터 시작 위치에서 시작 하는 데이터는 새 데이터에 대 한 공간을 만들기 위해 오른쪽으로 이동 합니다. 값이 0이면 기존 데이터의 시작점에 새 데이터를 삽입합니다. 값이 NULL이면 기존의 데이터 값에 데이터를 새로 추가합니다.  
  
 *delete_length*  
 기존 계획에서 삭제할 데이터의 길이 **텍스트**, **ntext**, 또는 **이미지** 에서 시작 하는 열은 *insert_offset* 위치입니다. *delete_length*바이트에 대 한에 값이 지정 **텍스트** 및 **이미지** 열 및 문자 수에 대 한 **ntext** 열입니다. 각 **ntext** 문자는 2 바이트를 사용 합니다. 값이 0이면 데이터를 삭제하지 않습니다. NULL 값에 데이터를 모두 삭제는 *insert_offset* 기존의 끝에 위치 **텍스트** 또는 **이미지** 열입니다.  
  
 WITH LOG  
 로깅은 데이터베이스에 영향을 주는 복구 모델에 의해 결정됩니다.  
  
 *inserted_data*  
 기존에 삽입할 데이터가 **텍스트**, **ntext**, 또는 **이미지** 열에는 *insert_offset* 위치 합니다. 단일 **char**, **nchar**, **varchar**, **nvarchar**, **이진**,  **varbinary**, **텍스트**, **ntext**, 또는 **이미지** 값입니다. *inserted_data* 는 리터럴 또는 변수일 수 있습니다.  
  
 *table_name.src_column_name*  
 테이블의 이름 및 **텍스트**, **ntext**, 또는 **이미지** 삽입된 된 데이터의 원본으로 사용 되는 열입니다. 테이블 이름과 열 이름은 식별자 규칙을 따라야 합니다.  
  
 *src_text_ptr*  
 텍스트 포인터를 가리키는 값 (TEXTPTR 함수에서 반환)는 **텍스트**, **ntext**, 또는 **이미지** 삽입된 된 데이터의 원본으로 사용 되는 열입니다.  
  
> [!NOTE]  
>  *scr_text_ptr* 값 아니어야 동일 *dest_text_ptr*값입니다.  
  
## <a name="remarks"></a>주의  
 새로 삽입된 된 데이터는 단일 가능 *inserted_data* 상수, 테이블 이름, 열 이름 또는 텍스트 포인터입니다.  
  
|업데이트 동작|UPDATETEXT 매개 변수|  
|-------------------|---------------------------|  
|기존 데이터를 바꾸려면|Null이 아닌 지정 *insert_offset* 값을 0이 아닌 *delete_length* 값 및 새 데이터를 삽입할 수 있습니다.|  
|기존 데이터를 삭제하려면|Null이 아닌 지정 *insert_offset* 값과 0이 아닌 *delete_length*합니다. 삽입할 새 데이터를 지정하지 않습니다.|  
|새 데이터를 삽입하려면|지정 된 *insert_offset* 값은 *delete_length* 0 및 삽입할 새 데이터.|  
  
 최상의 성능을 위해 좋습니다 **텍스트**, **ntext** 및 **이미지** 데이터 삽입 하거나 업데이트 8, 040 바이트의 배수인 청크 크기로 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 행 내부 텍스트 포인터를 **텍스트**, **ntext**, 또는 **이미지** 데이터가 있을 수 있지만 올바르지 않을 수 있습니다. Text in row 옵션에 대 한 정보를 참조 하십시오. [sp_tableoption &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 텍스트 포인터를 무효화 하는 방법에 대 한 정보를 참조 하십시오. [sp_invalidate_textptr &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 초기화 **텍스트** WRITETEXT;를 사용 하 여 열을 NULL Updatetext **텍스트** 열을 빈 문자열로 합니다.  
  
## <a name="permissions"></a>Permissions  
 지정된 테이블에 대해 UPDATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음은 텍스트 포인터를 지역 변수인 `@ptrval`에 둔 다음 `UPDATETEXT`를 사용하여 맞춤법 오류를 업데이트하는 예입니다.  
  
> [!NOTE]  
>  이 예를 실행하려면 pubs 데이터베이스를 설치해야 합니다.  
  
```  
USE pubs;  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
DECLARE @ptrval binary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr, publishers p  
      WHERE p.pub_id = pr.pub_id   
      AND p.pub_name = 'New Moon Books'  
UPDATETEXT pub_info.pr_info @ptrval 88 1 'b';  
GO  
ALTER DATABASE pubs SET RECOVERY FULL;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Readtext&#40; Transact SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40; Transact SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
