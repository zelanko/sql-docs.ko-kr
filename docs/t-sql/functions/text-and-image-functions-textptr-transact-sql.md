---
title: TEXTPTR(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTPTR_TSQL
- TEXTPTR
dev_langs:
- TSQL
helpviewer_keywords:
- TEXTPTR function
- viewing text pointer values
- text-pointer values
- displaying text pointer values
ms.assetid: 2672b8cb-f747-46f3-9358-9b49b3583b8e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d0e511e34b782c444bcdf6c778bb89dfebd4fab4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68099030"
---
# <a name="text-and-image-functions---textptr-transact-sql"></a>텍스트 및 이미지 함수 - TEXTPTR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **text**, **ntext** 또는 **image** 열에 해당하는 텍스트 포인터 값을 **varbinary** 형식으로 반환합니다. 검색한 텍스트 포인터 값은 READTEXT, WRITETEXT 및 UPDATETEXT 문에서 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대체 기능을 사용할 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
TEXTPTR ( column )  
```  
  
## <a name="arguments"></a>인수  
 *column*  
 사용될 **text**, **ntext** 또는 **image** 열입니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary**  
  
## <a name="remarks"></a>설명  
 행 내부 텍스트가 있는 테이블의 경우, TEXTPTR 함수는 처리할 텍스트에 대한 핸들을 반환합니다. 텍스트 값이 null이어도 유효한 텍스트 포인터를 얻을 수 있습니다.  
  
 뷰의 열에서는 TEXTPTR 함수를 사용할 수 없습니다. 테이블의 열에만 사용할 수 있습니다. 뷰의 열에 TEXTPTR 함수를 사용하려면 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 사용하여 호환성 수준을 80으로 설정해야 합니다. 테이블에 행 내부 텍스트가 없고 UPDATETEXT 문으로 **text**, **ntext** 또는 **image** 열을 초기화하지 않은 경우 TEXTPTR는 null 포인터를 반환합니다.  
  
 TEXTVALID를 사용하여 텍스트 포인터의 존재 여부를 테스트하십시오. 유효한 텍스트 포인터가 없으면 UPDATETEXT, WRITETEXT 또는 READTEXT를 사용할 수 없습니다.  
  
 이러한 함수와 문은 **text**, **ntext** 및 **image** 데이터를 사용하는 작업에도 유용합니다.  
  
|함수 또는 문|Description|  
|---------------------------|-----------------|  
|PATINDEX<b>(‘</b> _%pattern%_ **’ ,** _expression_ **)**|**text** 또는 **ntext** 열에서 지정된 문자열의 문자 위치를 반환합니다.|  
|DATALENGTH<b>(</b>_expression_ **)**|**text**, **ntext** 및 **image** 열의 데이터 길이를 반환합니다.|  
|SET TEXTSIZE|SELECT 문으로 반환할 **text**, **ntext** 또는 **image** 데이터의 크기 제한(바이트)을 반환합니다.|  
|SUBSTRING<b>(</b>_text_column_, _start_, _length_ **)**|지정한 *start* 오프셋과 *length*로 지정한 **varchar** 문자열을 반환합니다. 길이는 8KB보다 작아야 합니다.|  
  
## <a name="examples"></a>예  
  
> [!NOTE]  
>  다음 예를 실행하려면 **pubs** 데이터베이스를 설치해야 합니다.  
  
### <a name="a-using-textptr"></a>A. TEXTPTR 사용  
 다음 예에서는 `TEXTPTR` 함수를 사용하여 `pubs` 데이터베이스의 `pub_info` 테이블에서 `New Moon Books`와 관련된 **image** 열 `logo`를 찾는 방법을 보여 줍니다. 텍스트 포인터는 지역 변수인 `@ptrval.`로 설정합니다.  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(logo)  
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books';  
GO  
```  
  
### <a name="b-using-textptr-with-in-row-text"></a>B. 행 내부 텍스트와 함께 TEXTPTR 사용  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다음 예와 같이 트랜잭션 내에서 행 내부 텍스트 포인터를 사용해야 합니다.  
  
```  
CREATE TABLE t1 (c1 int, c2 text);  
EXEC sp_tableoption 't1', 'text in row', 'on';  
INSERT t1 VALUES ('1', 'This is text.');  
GO  
BEGIN TRAN;  
   DECLARE @ptrval VARBINARY(16);  
   SELECT @ptrval = TEXTPTR(c2)  
   FROM t1  
   WHERE c1 = 1;  
   READTEXT t1.c2 @ptrval 0 1;  
COMMIT;  
```  
  
### <a name="c-returning-text-data"></a>C. 텍스트 데이터 반환  
 다음 예에서는 `pub_id` 테이블에서 `pr_info` 열 및 `pub_info` 열의 16바이트 텍스트 포인터를 선택하는 방법을 보여 줍니다.  
  
```  
USE pubs;  
GO  
SELECT pub_id, TEXTPTR(pr_info)  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id                                      
------ ----------------------------------   
0736   0x6c0000000000feffb801000001000100   
0877   0x6d0000000000feffb801000001000300   
1389   0x6e0000000000feffb801000001000500   
1622   0x700000000000feffb801000001000900   
1756   0x710000000000feffb801000001000b00   
9901   0x720000000000feffb801000001000d00   
9952   0x6f0000000000feffb801000001000700   
9999   0x730000000000feffb801000001000f00   
  
(8 row(s) affected)  
```  
  
 다음 예에서는 TEXTPTR를 사용하지 않고 텍스트의 처음 `8000`바이트를 반환하는 방법을 보여 줍니다.  
  
```  
USE pubs;  
GO  
SET TEXTSIZE 8000;  
SELECT pub_id, pr_info  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id pr_info                                                                                                                                                                                                                                                           
------ -----------------------------------------------------------------  
0736   New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!                                                                                                             
0877   This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washington, D.C.  
  
This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washi   
1389   This is sample text data for Algodata Infosystems, publisher 1389 in the pubs database. Algodata Infosystems is located in Berkeley, California.  
  
9999   This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in Paris, France.  
  
This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in   
  
(8 row(s) affected)  
```  
  
### <a name="d-returning-specific-text-data"></a>D. 특정 텍스트 데이터 반환  
 다음 예에서는 `pubs` 데이터베이스의 `pub_info` 테이블에서 `pub_id``0736`과 연관된 `text` 열(`pr_info`)을 찾는 방법을 보여 줍니다. 먼저 지역 변수 `@val`을 선언하고 텍스트 포인터(긴 이진 문자열)를 `@val`로 설정한 다음 `READTEXT` 문에 대한 매개 변수로 제공합니다. 이 문은 5번째 바이트(오프셋 4)에서 시작하여 10바이트를 반환합니다.  
  
```  
USE pubs;  
GO  
DECLARE @val varbinary(16);  
SELECT @val = TEXTPTR(pr_info)   
FROM pub_info  
WHERE pub_id = '0736';  
READTEXT pub_info.pr_info @val 4 10;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pr_info                                                                                                                                                                                                                                                           
-----------------------------------------------------------------------  
 is sample  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [DATALENGTH&#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX&#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [READTEXT&#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [SET TEXTSIZE&#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [텍스트 및 이미지 함수&#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [UPDATETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
