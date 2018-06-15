---
title: UPDATETEXT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf01a97b6337f154de8d6d8e2c0fb71f7c4a1dd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33065500"
---
# <a name="updatetext-transact-sql"></a>UPDATETEXT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 **text**, **ntext** 또는 **image** 필드를 업데이트합니다. UPDATETEXT를 사용하여 **text**, **ntext** 또는 **image** 열의 일부만 변경할 수 있습니다. WRITETEXT를 사용하여 **text**, **ntext** 또는 **image** 필드 전체를 업데이트하고 바꿀 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 큰 값 데이터 형식 및 [UPDATE](../../t-sql/queries/update-transact-sql.md) 문의 **.** WRITE 절을 사용합니다.  
  
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
  
 *table_name* **.** *dest_column_name*  
 업데이트할 테이블 및 **text**, **ntext** 또는 **image** 열의 이름입니다. 테이블 이름과 열 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다. 필요에 따라 데이터베이스 이름과 소유자 이름을 지정할 수 있습니다.  
  
 *dest_text_ptr*  
 업데이트할 **text**, **ntext** 또는 **image** 데이터를 가리키는 텍스트 포인터 값(TEXTPTR 함수에서 반환된 값)입니다. *text_ptr*은 **이진(** 16 **)** 이여야 합니다.  
  
 *insert_offset*  
 업데이트의 경우 0부터 시작하는 시작 위치입니다. **text** 또는 **image** 열의 경우 *insert_offset*은 새 데이터를 삽입하기 전에 기존 열의 시작점에서부터 건너뛰어야 하는 바이트 수입니다. **ntext** 열의 경우 *insert_offset*는 문자 수입니다(각 **ntext** 문자는 2 바이트를 사용합니다). 0부터 시작하는 시작 위치에 있는 기존의 **text**, **ntext** 또는 **image** 데이터는 새 데이터에 필요한 공간을 만들기 위해 오른쪽으로 옮겨집니다. 값이 0이면 기존 데이터의 시작점에 새 데이터를 삽입합니다. 값이 NULL이면 기존의 데이터 값에 데이터를 새로 추가합니다.  
  
 *delete_length*  
 기존의 **text**, **ntext** 또는 **image** 열에서 삭제할 데이터의 길이로, *insert_offset* 위치부터 삭제됩니다. *delete_length* 값은 **text** 및 **image** 열에서는 바이트로 그리고 **ntext** 열에서는 문자로 지정됩니다. 각 **ntext** 문자는 2바이트를 사용합니다. 값이 0이면 데이터를 삭제하지 않습니다. 값이 NULL이면 *insert_offset*위치에서 기존의 **text** 또는 **image** 열의 끝까지 데이터를 모두 삭제합니다.  
  
 WITH LOG  
 로깅은 데이터베이스에 영향을 주는 복구 모델에 의해 결정됩니다.  
  
 *inserted_data*  
 *insert_offset* 위치에서 기존 **text**, **ntext** 또는 **image** 열로 삽입할 데이터입니다. 이것은 단일 **char**, **nchar**, **varchar**, **nvarchar**, **binary**, **varbinary**, **text**, **ntext** 또는 **image** 값입니다. *inserted_data*는 리터럴 또는 변수일 수 있습니다.  
  
 *table_name.src_column_name*  
 삽입된 데이터 원본으로 사용되는 **text**, **ntext** 또는 **image** 열 이름과 테이블의 이름입니다. 테이블 이름과 열 이름은 식별자 규칙을 따라야 합니다.  
  
 *src_text_ptr*  
 삽입된 데이터 원본으로 사용되는 **text**, **ntext** 또는 **image** 열을 가리키는 텍스트 포인터 값(TEXTPTR 함수에서 반환되는 값)입니다.  
  
> [!NOTE]  
>  *scr_text_ptr* 값은 *dest_text_ptr* 값과 같아서는 안됩니다.  
  
## <a name="remarks"></a>Remarks  
 새로 삽입되는 데이터는 단일 *inserted_data* 상수, 테이블 이름, 열 이름 또는 텍스트 포인터일 수 있습니다.  
  
|업데이트 동작|UPDATETEXT 매개 변수|  
|-------------------|---------------------------|  
|기존 데이터를 바꾸려면|Null이 아닌 *insert_offset* 값, 0이 아닌 *delete_length* 값 및 삽입할 새 데이터를 지정합니다.|  
|기존 데이터를 삭제하려면|Null이 아닌 *insert_offset* 값과 0이 아닌 *delete_length*를 지정합니다. 삽입할 새 데이터를 지정하지 않습니다.|  
|새 데이터를 삽입하려면|*insert_offset* 값, 0의 *delete_length* 및 삽입할 새 데이터를 지정합니다.|  
  
 최고의 성능을 위해 **text**, **ntext** 및 **image** 데이터는 8,040바이트의 배수인 청크 크기로 삽입하거나 업데이트하는 것이 좋습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **text**, **ntext** 또는 **image** 데이터에 대한 행 내부 텍스트 포인터가 있어도 유효하지 않을 수 있습니다. text in row 옵션에 대한 자세한 내용은 [sp_tableoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 참조하십시오. 텍스트 포인터를 무효화하는 방법은 [sp_invalidate_textptr&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)를 참조하십시오.  
  
 **text** 열을 NULL로 초기화하려면 WRITETEXT를 사용합니다. UPDATETEXT는 **text** 열을 빈 문자열로 초기화합니다.  
  
## <a name="permissions"></a>사용 권한  
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
  
## <a name="see-also"></a>참고 항목  
 [READTEXT&#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR&#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
