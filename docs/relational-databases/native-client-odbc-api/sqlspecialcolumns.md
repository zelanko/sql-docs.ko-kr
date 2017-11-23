---
title: SQLSpecialColumns | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ff6889d81489b0009d4c48b5194d772abaec014
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  행 식별자(*IdentifierType* SQL_BEST_ROWID)를 요청할 경우 **SQLSpecialColumns** 는 SQL_SCOPE_CURROW 이외의 모든 요청 범위에 대해 빈 결과 집합(데이터 행 없음)을 반환합니다. 즉, 생성된 결과 집합은 열이 이 범위 내에서만 유효하다는 것을 나타냅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 식별자에 대한 의사 열을 지원하지 않습니다. **SQLSpecialColumns** 결과 집합은 모든 열을 SQL_PC_NOT_PSEUDO로 식별합니다.  
  
 **SQLSpecialColumns** 는 정적 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 커서(키 집합 커서 또는 동적 커서)에 대해 **SQLSpecialColumns** 를 실행하려고 하면 커서 유형이 변경되었음을 나타내는 SQL_SUCCESS_WITH_INFO가 반환됩니다.  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLSpecialColumns 지원  
 값에 대 한 정보 반환 된 열에 대 한 DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH 및 DECIMAL_DIGTS 날짜/시간 형식에 대 한 참조 [카탈로그 메타 데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)합니다.  
  
 자세한 내용은 참조 하십시오. [날짜 및 시간 기능 향상 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLSpecialColumns 지원  
 **SQLSpecialColumns** 는 큰 CLR UDT(사용자 정의 형식)를 지원합니다. 자세한 내용은 참조 [Large CLR User-Defined 형식 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLSpecialColumns 함수](http://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
