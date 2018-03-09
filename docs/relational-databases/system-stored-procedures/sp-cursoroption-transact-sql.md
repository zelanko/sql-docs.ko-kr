---
title: sp_cursoroption (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs: TSQL
helpviewer_keywords: sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0fcd7b9c009d0af70e48982f9630f783bce057d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spcursoroption-transact-sql"></a>sp_cursoroption(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sp_cursoropen 저장 프로시저에서 만든 커서 정보를 반환 하거나 커서 옵션을 설정 합니다. sp_cursoroption가 ID를 지정 하 여 호출 = 표 형식 데이터 TDS (stream) 패킷의 8입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>인수  
 *cursor*  
 이 *처리* 값에 의해 생성 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하며 sp_cursoropen 저장 프로시저에서 반환 합니다. *커서* 필요는 **int** 실행에 대 한 값을 입력 합니다.  
  
 *코드*  
 커서 반환 값의 여러 요인을 규정하는 데 사용됩니다. *코드* 다음 중 하나 필요로 **int** 값 입력:  
  
|값|이름|Description|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|지정된 특정 텍스트 또는 이미지 열에 대해 실제 데이터가 아닌 텍스트 포인터를 반환합니다.<br /><br /> TEXTPTR_ONLY 텍스트 포인터를으로 사용할 수 있도록 *핸들* 선택적으로 나중에 검색 수 또는 사용 하 여 업데이트 가능한 blob 개체에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 DBLIB 기능 (예: [!INCLUDE[tsql](../../includes/tsql-md.md)]READTEXT 또는 DBLIB DBWRITETEXT)입니다.<br /><br /> "0" 값을 할당하면 선택 목록에 있는 모든 텍스트 및 이미지 열이 데이터가 아닌 텍스트 포인터를 반환합니다.|  
|0x0002|CURSOR_NAME|에 지정 된 이름을 할당 *값* 커서입니다. 이 있습니다 사용할 ODBC [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_cursoropen을 통해 연 커서에 위치 지정 UPDATE/DELETE 문을 합니다.<br /><br /> 문자열은 원하는 문자나 유니코드 데이터 형식으로 지정할 수 있습니다.<br /><br /> 이후 [!INCLUDE[tsql](../../includes/tsql-md.md)] 위치 지정된 UPDATE/DELETE 문은 운영 fat 커서의 첫 번째 행에는 기본적으로 sp_cursor SETPOSITION 위치 지정된 UPDATE/DELETE 문을 실행 하기 전에 커서의 위치를 사용 해야 합니다.|  
|0x0003|TEXTDATA|후속 인출에서 특정 텍스트 또는 이미지 열에 대해 텍스트 포인터가 아닌 실제 데이터를 반환합니다. 즉, TEXTPTR_ONLY의 효과를 실행 취소합니다.<br /><br /> 특정 열에 대해 TEXTDATA를 설정하면 행을 다시 인출하거나 새로 고치며, 그런 다음 행을 TEXTPTR_ONLY로 다시 설정할 수 있습니다. TEXTPTR_ONLY와 마찬가지로 값 매개 변수는 열 번호를 지정하는 정수이며, 값이 0이면 모든 텍스트 또는 이미지 열이 반환됩니다.|  
|0x0004|SCROLLOPT|스크롤 옵션입니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "반환 코드 값"을 참조하십시오.|  
|0x0005|CCOPT|동시성 제어 옵션입니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "반환 코드 값"을 참조하십시오.|  
|0x0006|ROWCOUNT|현재 결과 집합에 있는 행의 수입니다.<br /><br /> 참고: 행 개수 값이 비동기 채우기를 사용 중인 경우 sp_cursoropen에서 반환 된 이후 변경 되었습니다. 행 수를 알 수 없는 경우에는 값 -1이 반환됩니다.|  
  
 *value*  
 반환 되는 값을 지정 *코드*합니다. *값* 는 0x0001, 0x0002 또는 0x0003 필요로 하는 필수 매개 변수 *코드* 값을 입력 합니다.  
  
> [!NOTE]  
>  A *코드* 2의 값은 문자열 데이터 형식입니다. 다른 모든 *코드* 값에서 반환 하거나 입력 *값* 는 정수입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 *값* 매개 변수는 다음 중 하나를 반환할 수 있습니다 *코드* 값입니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 *값* 매개 변수는 다음 SCROLLOPT 값 중 하나를 반환 합니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 *값* 매개 변수는 다음 CCOPT 값 중 하나를 반환 합니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 또는 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
