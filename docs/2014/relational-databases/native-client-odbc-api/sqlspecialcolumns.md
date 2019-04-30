---
title: SQLSpecialColumns | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ea811151e9c81ed515b774f279297d236c608f5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188735"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
  행 식별자(*IdentifierType* SQL_BEST_ROWID)를 요청할 경우 **SQLSpecialColumns** 는 SQL_SCOPE_CURROW 이외의 모든 요청 범위에 대해 빈 결과 집합(데이터 행 없음)을 반환합니다. 즉, 생성된 결과 집합은 열이 이 범위 내에서만 유효하다는 것을 나타냅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 식별자에 대한 의사 열을 지원하지 않습니다. **SQLSpecialColumns** 결과 집합은 모든 열을 SQL_PC_NOT_PSEUDO로 식별합니다.  
  
 **SQLSpecialColumns** 는 정적 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 커서(키 집합 커서 또는 동적 커서)에 대해 **SQLSpecialColumns** 를 실행하려고 하면 커서 유형이 변경되었음을 나타내는 SQL_SUCCESS_WITH_INFO가 반환됩니다.  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLSpecialColumns 지원  
 날짜/시간 형식에서 DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH 및 DECIMAL_DIGTS 열에 반환되는 값에 대한 자세한 내용은 [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md)를 참조하십시오.  
  
 자세한 내용은 참조 하세요. [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLSpecialColumns 지원  
 **SQLSpecialColumns** 는 큰 CLR UDT(사용자 정의 형식)를 지원합니다. 자세한 내용은 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLSpecialColumns 함수](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
