---
title: READTEXT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c1659dfcc9ca8908ce756eb41b32fd30649decfa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="readtext-transact-sql"></a>READTEXT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  읽고 **텍스트**, **ntext**, 또는 **이미지** 에서 값을 **텍스트**, **ntext**, 또는 **이미지**  열에서 지정된 된 수의 바이트를 읽고 지정된 된 오프셋에서 시작 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [부분 문자열](../../t-sql/functions/substring-transact-sql.md) 함수를 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>인수  
 *테이블* **합니다.** *column*  
 읽을 테이블과 열의 이름입니다. 테이블 및 열 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. 테이블 및 열 이름은 반드시 지정해야 하지만 데이터베이스 이름과 소유자 이름을 지정하는 것은 선택적입니다.  
  
 *text_ptr*  
 유효한 텍스트 포인터입니다. *text_ptr* 해야 **binary (16)**합니다.  
  
 *offset*  
 바이트 수입니다 (때는 **텍스트** 또는 **이미지** 데이터 유형을 사용 하 여) 또는 문자 (때는 **ntext** 데이터 형식을 사용)를는 읽기전에건너뛸**텍스트**, **이미지**, 또는 **ntext** 데이터입니다.  
  
 *size*  
 바이트 수입니다 (때는 **텍스트** 또는 **이미지** 데이터 유형을 사용 하 여) 또는 문자 (때는 **ntext** 데이터 형식이 사용 됩니다) 읽을 데이터입니다. 경우 *크기* 가 0 이면 4kb의 데이터가 읽혀집니다.  
  
 HOLDLOCK  
 트랜잭션이 끝날 때까지 텍스트 값을 읽을 수 없게 잠급니다. 다른 사용자는 값을 읽을 수 있지만 수정할 수는 없습니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 [TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md) 함수를 유효한 *text_ptr* 값입니다. 에 대 한 포인터를 반환 하는 TEXTPTR는 **텍스트**, **ntext**, 또는 **이미지** 지정된 된 행의 열을 가리키거나는 **텍스트**, **ntext** , 또는 **이미지** 둘 이상의 행이 반환 되는 쿼리에 의해 반환 된 마지막 행의 열입니다. TEXTPTR은 16바이트 이진 문자열을 반환하므로 지역 변수를 선언하여 텍스트 포인터를 보유한 다음 READTEXT로 해당 변수를 사용하는 것이 좋습니다. 지역 변수 선언에 대 한 자세한 내용은 참조 [DECLARE @local_variable &#40; Transact SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 행 내부 텍스트 포인터가 있을 수 있지만 유효하지 않습니다. 에 대 한 자세한 내용은 **행의 텍스트에에서** 옵션 [sp_tableoption &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 텍스트 포인터를 무효화 하는 방법에 대 한 자세한 내용은 참조 [sp_invalidate_textptr &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 값은 @@TEXTSIZE 함수에는 READTEXT에 대해 지정된 된 크기 보다 작을 경우 READTEXT에 대해 지정 된 크기 보다 우선 합니다. @@TEXTSIZE 함수 SET TEXTSIZE 문에서 설정한 반환 될 데이터의 바이트 수에 대 한 제한을 지정 합니다. TEXTSIZE의 세션 설정은 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [SET TEXTSIZE &#40; Transact SQL &#41; ](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 지정한 테이블에 대한 SELECT 권한이 있는 사용자에게 기본적으로 READTEXT 권한이 부여됩니다. SELECT 권한을 위임하는 경우에는 READTEXT 권한도 위임할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `pr_info` 테이블에 있는 `pub_info` 열의 문자를 두 번째 문자부터 26번째 문자까지 읽습니다.  
  
> [!NOTE]  
>  이 예제를 실행 하려면 설치 해야는 **pubs** 예제 데이터베이스.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [@@TEXTSIZE&#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [UPDATETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
