---
title: 데이터 버퍼 주소 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f07f835361fcf29143376fe468a55f0bf26e31e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471132"
---
# <a name="data-buffer-address"></a>데이터 버퍼 주소
응용 프로그램 종종 명명 된 인수를 드라이버에 데이터 버퍼의 주소를 전달 *ValuePtr* 또는 비슷한 이름입니다. 예를 들어, 다음에서에 호출할 **SQLBindCol**, 응용 프로그램의 주소를 지정 합니다 *날짜* 변수:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 에 설명 된 대로 합니다 [Allocating 및 버퍼를 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) 섹션에서는 지연 된 버퍼의 주소를 유효한 상태로 유지 되어야 버퍼 바인딩 해제할 때까지 유지 합니다.  
  
 특히 금지 하지 않는 한 데이터 버퍼의 주소는 null 포인터를 수 있습니다. 드라이버에 데이터를 보내는 데 사용 하는 버퍼에 대 한 일반적으로 버퍼에 포함 된 정보를 무시 하도록 하면이 합니다. 드라이버에서 데이터를 검색 하는 데 사용 하는 버퍼에 대 한 드라이버에 값을 반환 하지 그러면 합니다. 두 경우 모두 해당 데이터 버퍼 길이 인수를 무시 합니다.
