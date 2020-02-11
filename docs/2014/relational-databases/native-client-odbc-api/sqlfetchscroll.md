---
title: SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c9614a71c0015d17178a57d33c5fd0d9b62433c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63154694"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
  **Sqlfetchscroll** 은 응용 프로그램에 데이터의 한 행 집합을 반환 합니다. 행 집합의 크기는 [SQLSetStmtAttr](sqlsetstmtattr.md)를 사용 하 여 설정 됩니다. Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client ODBC 드라이버는 다음과 같은 제한 사항을 사용 하 여 정의 된 모든 fetch 명령 (예: SQL_FETCH_RELATIVE)을 지원 합니다.  
  
-   문에 대해 정방향 전용 커서가 정의된 경우 SQL_FETCH_NEXT가 필요하며, 다른 방식으로 인출을 시도하면 오류가 반환됩니다.  
  
-   SQL_FETCH_BOOKMARK는 정적 및 키 집합 커서에 대해서만 지원됩니다.  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLFetchScroll 지원  
 날짜/시간 형식의 결과 열 값은 [SQL에서 C로 변환](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)에 설명 된 대로 변환 됩니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLFetchScroll 지원  
 **Sqlfetchscroll** 은 많은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC&#41;&#40;LARGE CLR 사용자 정의 형식 ](../native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLFetchScroll 함수](https://go.microsoft.com/fwlink/?LinkId=59343)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
