---
title: sp_cursoroption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 560c425c5bda4ee1f9dd7ecf454c65d3ba7eab1e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831727"
---
# <a name="sp_cursoroption-transact-sql"></a>sp_cursoroption(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  커서 옵션을 설정 하거나 sp_cursoropen 저장 프로시저에서 만든 커서 정보를 반환 합니다. sp_cursoroption은 TDS (tabular data stream) 패킷에서 ID = 8을 지정 하 여 호출 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>인수  
 *cursor*  
 는에서 *handle* 생성 되 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 sp_cursoropen 저장 프로시저에서 반환 하는 핸들 값입니다. *커서* 를 실행 하려면 **int** 입력 값이 필요 합니다.  
  
 *code*  
 커서 반환 값의 여러 요인을 규정하는 데 사용됩니다. *코드* 에는 다음 **int** 입력 값 중 하나가 필요 합니다.  
  
|값|속성|설명|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|지정된 특정 텍스트 또는 이미지 열에 대해 실제 데이터가 아닌 텍스트 포인터를 반환합니다.<br /><br /> TEXTPTR_ONLY 사용 하 여 텍스트 포인터를 blob 개체에 대 한 *핸들로* 사용할 수 있습니다 .이 개체는 나중에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 DBLIB 시설 (예: [!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT 또는 DBLIB dbwritetext)을 사용 하 여 선택적으로 검색 하거나 업데이트할 수 있습니다.<br /><br /> "0" 값을 할당하면 선택 목록에 있는 모든 텍스트 및 이미지 열이 데이터가 아닌 텍스트 포인터를 반환합니다.|  
|0x0002|CURSOR_NAME|*값* 에 지정 된 이름을 커서에 할당 합니다. 이렇게 하면 ODBC가 [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_cursoropen를 통해 열린 커서에 대해 위치 지정 UPDATE/DELETE 문을 사용할 수 있습니다.<br /><br /> 문자열은 원하는 문자나 유니코드 데이터 형식으로 지정할 수 있습니다.<br /><br /> [!INCLUDE[tsql](../../includes/tsql-md.md)]위치 지정 update/delete 문은 기본적으로 fat 커서의 첫 번째 행에서 작동 하므로 위치 지정 update/delete 문을 실행 하기 전에 SP_CURSOR SETPOSITION을 사용 하 여 커서를 배치 해야 합니다.|  
|0x0003|TEXTDATA|후속 인출에서 특정 텍스트 또는 이미지 열에 대해 텍스트 포인터가 아닌 실제 데이터를 반환합니다. 즉, TEXTPTR_ONLY의 효과를 실행 취소합니다.<br /><br /> 특정 열에 대해 TEXTDATA를 설정하면 행을 다시 인출하거나 새로 고치며, 그런 다음 행을 TEXTPTR_ONLY로 다시 설정할 수 있습니다. TEXTPTR_ONLY와 마찬가지로 값 매개 변수는 열 번호를 지정하는 정수이며, 값이 0이면 모든 텍스트 또는 이미지 열이 반환됩니다.|  
|0x0004|SCROLLOPT|스크롤 옵션입니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "반환 코드 값"을 참조하십시오.|  
|0x0005|CCOPT|동시성 제어 옵션입니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "반환 코드 값"을 참조하십시오.|  
|0x0006|ROWCOUNT|현재 결과 집합에 있는 행의 수입니다.<br /><br /> 참고: 비동기 채우기를 사용 하는 경우 sp_cursoropen에서 반환 된 값 이후에 ROWCOUNT가 변경 되었을 수 있습니다. 행 수를 알 수 없는 경우-1 값이 반환 됩니다.|  
  
 *value*  
 *코드*에서 반환 되는 값을 지정 합니다. *값* 은 0x0001, 0x0002 또는 0x0003 *코드* 입력 값을 호출 하는 필수 매개 변수입니다.  
  
> [!NOTE]  
>  *코드* 값 2는 문자열 데이터 형식입니다. 다른 모든 *코드* 값 입력 또는 *값* 으로 반환 되는 값은 정수입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 *값* 매개 변수는 다음 *코드* 값 중 하나를 반환할 수 있습니다.  
  
|반환 값|설명|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 *값* 매개 변수는 다음 SCROLLOPT 값 중 하나를 반환 합니다.  
  
|반환 값|설명|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 *값* 매개 변수는 다음 값 중 하나를 반환 합니다.  
  
|반환 값|설명|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 또는 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_cursor &#40;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [Transact-sql&#41;sp_cursoropen &#40;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
