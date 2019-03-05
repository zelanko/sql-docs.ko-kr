---
title: WRITETEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 5dd029115c99ae4826bf1070a7556c7fbdcb8c55
ms.sourcegitcommit: 670082cb47f7d3d82e987b549b6f8e3a8968b5db
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57334610"
---
# <a name="writetext-transact-sql"></a>WRITETEXT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 **text**, **ntext** 또는 **image** 열의 최소 로깅 대화형 업데이트를 허용합니다. WRITETEXT는 영향을 받는 열에 있는 모든 기존 데이터를 덮어씁니다. WRITETEXT는 뷰 내의 **text**, **ntext** 및 **image** 열에서 사용할 수 없습니다.  
  
> [!IMPORTANT]
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 큰 값 데이터 형식 및 [UPDATE](../../t-sql/queries/update-transact-sql.md) 문의 **.** WRITE 절을 사용합니다.  
  
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
  
 *table* **.column**  
 업데이트할 테이블 및 **text**, **ntext** 또는 **image** 열의 이름입니다. 테이블 이름 및 열 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 필요에 따라 데이터베이스 이름과 소유자 이름을 지정할 수 있습니다.  
  
 *text_ptr*  
 **text**, **ntext** 또는 **image** 데이터에 대한 포인터를 저장하는 값입니다. *text_ptr*은 **이진(16)** 이어야 합니다. 텍스트 포인터를 만들려면 **text**, **ntext** 또는 **image** 열에 대해 Null이 아닌 데이터를 사용하여 [INSERT](../../t-sql/statements/insert-transact-sql.md) 또는 [UPDATE](../../t-sql/queries/update-transact-sql.md) 문을 실행합니다.  
  
 WITH LOG  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 무시됩니다. 로깅은 데이터베이스에 영향을 주는 복구 모델에 의해 결정됩니다.  
  
 *data*  
 저장할 실제 **text**, **ntext** 또는 **image** 데이터입니다. *data*는 리터럴 또는 매개 변수일 수 있습니다. WRITETEXT와 함께 대화형으로 삽입할 수 있는 텍스트의 최대 길이는 **text**, **ntext** 또는 **image** 데이터의 경우 약 120KB입니다.  
  
## <a name="remarks"></a>Remarks  
 WRITETEXT를 사용하여 **text**, **ntext** 및 **image** 데이터를 바꾸고 UPDATETEXT를 사용하여 **text**, **ntext** 및 **image** 데이터를 수정합니다. UPDATETEXT는 **text**, **ntext** 또는 **image** 열의 전체가 아닌 일부만 변경하므로 더 융통성이 있습니다.  
  
 최상의 성능을 위해 **text**, **ntext** 및 **image** 데이터를 8,040바이트의 배수가 되는 청크 크기로 삽입하거나 업데이트하는 것이 좋습니다.  
  
 데이터베이스 복구 모델이 단순 또는 대량 로그 복구 모델인 경우 새 데이터가 삽입 또는 추가되었을 때 WRITETEXT를 사용하는 **text**, **ntext** 및 **image** 작업은 최소 로그 작업입니다.  
  
> [!NOTE]  
>  기존 값이 업데이트되면 최소 로깅이 사용되지 않습니다.  
  
 WRITETEXT가 제대로 작동하려면 열에는 반드시 유효한 텍스트 포인터가 있어야 합니다.  
  
 테이블에 행 내부 텍스트가 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 INSERT로 명시적 또는 암시적 Null 값이 **text** 열에 추가되고 이러한 Null 값에 대해 텍스트 포인터를 가져올 수 없을 때 **text** 열을 초기화하지 않음으로써 공백을 저장합니다. **text** 열을 NULL로 초기화하려면 UPDATE 문을 사용합니다. 테이블에 행 내부 텍스트가 있는 경우에는 text 열을 Null로 초기화할 필요 없이 항상 텍스트 포인터를 가져올 수 있습니다.  
  
 ODBC SQLPutData 함수는 WRITETEXT보다 빠르며 동적 메모리를 덜 사용합니다. 이 함수는**text**, **ntext** 또는 **image** 데이터를 2GB까지 삽입할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **text**, **ntext** 또는 **image** 데이터에 대한 행 내부 텍스트 포인터가 있어도 유효하지 않을 수 있습니다. 행의 텍스트 옵션에 대한 자세한 내용은 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 참조하세요. 텍스트 포인터를 무효화하는 방법은 [sp_invalidate_textptr&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)를 참조하십시오.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
