---
title: WRITETEXT (Transact SQL) | Microsoft Docs
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
- WRITETEXT_TSQL
- WRITETEXT
dev_langs:
- TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5bf092ec05c2ae07864c12f092cf8b98f97234fa
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="writetext-transact-sql"></a>WRITETEXT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  최소 로깅 대화형 업데이트 기존 허용 **텍스트**, **ntext**, 또는 **이미지** 열입니다. WRITETEXT는 영향을 받는 열에 있는 모든 기존 데이터를 덮어씁니다. WRITETEXT는에서 사용할 수 없습니다 **텍스트**, **ntext**, 및 **이미지** 뷰에 열입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]큰 값 데이터 형식을 사용 하 고 **.** WRITE 절을는 [업데이트](../../t-sql/queries/update-transact-sql.md) 문 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
WRITETEXT [BULK]  
  { table.column text_ptr }  
  [ WITH LOG ] { data }  
```  
  
## <a name="arguments"></a>인수  
 BULK  
 이진 데이터 스트림을 업로드하기 위해 업로드 도구를 사용합니다. 스트림은 도구가 TDS 프로토콜 수준에서 제공해야 합니다. 데이터 스트림이 없으면 쿼리 프로세서는 BULK 옵션을 무시합니다.  
  
> [!IMPORTANT]  
>  BULK 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기반 응용 프로그램에서 사용하지 않는 것이 좋습니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 버전에서 변경 또는 제거될 수 있습니다.  
  
 *테이블* **.column**  
 테이블의 이름 및 **텍스트**, **ntext**, 또는 **이미지** 열을 업데이트 합니다. 테이블 및 열 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. 필요에 따라 데이터베이스 이름과 소유자 이름을 지정할 수 있습니다.  
  
 *text_ptr*  
 포인터를 저장 하는 값은 **텍스트**, **ntext**, 또는 **이미지** 데이터입니다. *text_ptr* 해야 **binary (16)**합니다. 텍스트 포인터를 만들려면 다음을 실행 한 [삽입](../../t-sql/statements/insert-transact-sql.md) 또는 [업데이트](../../t-sql/queries/update-transact-sql.md) 에 대 한 null이 아닌 데이터를 사용 하 여 문을 **텍스트**, **ntext**, 또는 **이미지** 열입니다.  
  
 WITH LOG  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 무시됩니다. 로깅은 데이터베이스에 영향을 주는 복구 모델에 의해 결정됩니다.  
  
 *데이터*  
 실제 **텍스트**, **ntext** 또는 **이미지** 데이터를 저장 합니다. *데이터* 는 리터럴 또는 매개 변수가 될 수 있습니다. WRITETEXT와 함께 대화형으로 삽입할 수 있는 텍스트의 최대 길이 약 120KB입니다 **텍스트**, **ntext**, 및 **이미지** 데이터입니다.  
  
## <a name="remarks"></a>주의  
 WRITETEXT를 사용 하 여 대체 **텍스트**, **ntext**, 및 **이미지** 데이터 및 수정 하는 UPDATETEXT **텍스트**, **ntext**, 및 **이미지** 데이터입니다. UPDATETEXT는의 일부를 변경 하기 때문에 보다 유연한는 **텍스트**, **ntext**, 또는 **이미지** 전체 열이 아니라 열입니다.  
  
 최상의 성능을 위해 좋습니다 **텍스트**, **ntext**, 및 **이미지** 데이터 삽입 하거나 업데이트 8, 040 바이트의 배수인 청크 크기로 합니다.  
  
 데이터베이스 복구 모델은 단순 또는 대량 로그 경우 **텍스트**, **ntext**, 및 **이미지** 새 데이터가 되었을 때 WRITETEXT를 사용 하는 작업은 최소 로그 작업 삽입 또는 추가 합니다.  
  
> [!NOTE]  
>  기존 값이 업데이트되면 최소 로깅이 사용되지 않습니다.  
  
 WRITETEXT가 제대로 작동하려면 열에는 반드시 유효한 텍스트 포인터가 있어야 합니다.  
  
 테이블에 행 내부 텍스트가 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 초기화 하지 않음으로써 공간을 절약 **텍스트** 열에 명시적 또는 암시적 null 값을 추가 하면 **텍스트** 삽입 및 텍스트 포인터가 있는 열 수 있습니다. 이러한 null에 대 한 가져옵니다. 초기화 **텍스트** 열을 NULL UPDATE 문을 사용 합니다. 테이블에 행 내부 텍스트가 있는 경우에는 text 열을 Null로 초기화할 필요 없이 항상 텍스트 포인터를 가져올 수 있습니다.  
  
 ODBC SQLPutData 함수는 버퍼 및 WRITETEXT 보다 덜 동적 메모리를 사용 합니다. 이 함수는 최대 2gb의 삽입할 수 **텍스트**, **ntext**, 또는 **이미지** 데이터입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 텍스트 포인터를 행 **텍스트**, **ntext**, 또는 **이미지** 데이터가 있을 수 있지만 올바르지 않을 수 있습니다. Text in row 옵션에 대 한 정보를 참조 하십시오. [sp_tableoption &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 텍스트 포인터를 무효화 하는 방법에 대 한 정보를 참조 하십시오. [sp_invalidate_textptr &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 지정된 테이블에 대해 UPDATE 권한이 필요합니다. UPDATE 권한이 부여되면 이를 위임할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 텍스트 포인터를 지역 변수인 `@ptrval`에 둔 다음 `WRITETEXT`이 지정한 행에 `@ptrval`로 새 텍스트 문자열을 넣습니다.  
  
> [!NOTE]  
>  이 예를 실행하려면 pubs 예제 데이터베이스를 설치해야 합니다.  
  
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
WRITETEXT pub_info.pr_info @ptrval 'New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!';  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Updatetext&#40; Transact SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
