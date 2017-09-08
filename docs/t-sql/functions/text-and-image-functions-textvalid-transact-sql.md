---
title: TEXTVALID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs:
- TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 279022316af7e3a396c7089f48933281264f900f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>텍스트 및 이미지 함수-TEXTVALID (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A **텍스트**, **ntext**, 또는 **이미지** 특정 텍스트 포인터가 유효한 지 여부를 확인 하는 함수입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대체 기능을 사용할 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
TEXTVALID ( 'table.column' ,text_ ptr )  
```  
  
## <a name="arguments"></a>인수  
 *table*  
 사용할 테이블의 이름입니다.  
  
 *열*  
 사용할 열의 이름입니다.  
  
 *text_ptr*  
 확인할 텍스트 포인터입니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 포인터가 유효하면 1, 유효하지 않으면 0을 반환합니다. 에 대 한 식별자는 **텍스트** 열은 테이블 이름을 포함 해야 합니다. 유효한 텍스트 포인터가 없으면 UPDATETEXT, WRITETEXT 또는 READTEXT를 사용할 수 없습니다.  
  
 다음 함수와 문에도 유용으로 작업할 때 **텍스트**, **ntext**, 및 **이미지** 데이터입니다.  
  
|함수 또는 문|Description|  
|---------------------------|-----------------|  
|PATINDEX**(**'*% 패턴 %**'***,** *식***)**|에 지정 된 문자열의 문자 위치를 반환 **텍스트** 및 **ntext** 열입니다.|  
|DATALENGTH**(***식***)**|에 데이터의 길이 반환 **텍스트**, **ntext**, 및 **이미지** 열입니다.|  
|SET TEXTSIZE|제한 (바이트) 반환 합니다.는 **텍스트**, **ntext**, 또는 **이미지** SELECT 문으로 반환 될 데이터입니다.|  
  
## <a name="examples"></a>예  
 다음 예에서는 `logo` 테이블의 `pub_info` 열에 있는 각 값에 대해 유효한 텍스트 포인터가 있는지 여부를 보고합니다.  
  
> [!NOTE]  
>  이 예제를 실행 하려면 설치 해야는 **pubs** 데이터베이스입니다.  
  
```  
USE pubs;  
GO  
SELECT pub_id, 'Valid (if 1) Text data'   
   = TEXTVALID ('pub_info.logo', TEXTPTR(logo))   
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id Valid (if 1) Text data   
------ ----------------------   
0736   1                        
0877   1                        
1389   1                        
1622   1                        
1756   1                        
9901   1                        
9952   1                        
9999   1                        
  
(8 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DATALENGTH &#40; Transact SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40; Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [SET TEXTSIZE &#40; Transact SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [텍스트 및 이미지 함수 &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40; Transact SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  
