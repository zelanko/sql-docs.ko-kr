---
title: "데이터 버퍼 주소 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7d57b8ec52324dd4bec320b6179507ab3102e629
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="data-buffer-address"></a>데이터 버퍼 주소입니다.
응용 프로그램이 종종 명명 된 인수에서 드라이버를 데이터 버퍼의 주소를 전달 *ValuePtr* 또는 비슷한 이름입니다. 예를 들어, 다음에 호출에서 **SQLBindCol**, 응용 프로그램의 주소를 지정 된 *날짜* 변수:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 설명한 것 처럼는 [Allocating 및 버퍼 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) 섹션에서 지연 된 버퍼의 주소 유효한 상태로 유지 되어야 버퍼가 바인딩된 때까지 합니다.  
  
 구체적으로 금지 된 경우가 아니면 데이터 버퍼의 주소는 null 포인터를 수 있습니다. 드라이버에 데이터를 보내는 데 사용 하는 버퍼에 대 한이 인해는 드라이버를 일반적으로 버퍼에 포함 된 정보를 무시 합니다. 드라이버에서 데이터를 검색 하는 데 사용 하는 버퍼에 대 한 드라이버를 값을 반환 하지 그러면 합니다. 두 경우 모두, 드라이버는 해당 데이터 버퍼 길이 인수를 무시합니다.

