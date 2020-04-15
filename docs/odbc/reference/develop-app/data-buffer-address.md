---
title: 데이터 버퍼 주소 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 578e4e37a78818cb640d9f32e2480cec5951df63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305274"
---
# <a name="data-buffer-address"></a>데이터 버퍼 주소
응용 프로그램은 데이터 버퍼의 주소를 *종종 ValuePtr* 또는 유사한 이름인 인수의 드라이버에 전달합니다. 예를 들어 **SQLBindCol에**대한 다음 호출에서 응용 프로그램은 *Date* 변수의 주소를 지정합니다.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 할당 및 [해제 버퍼](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) 섹션에서 설명한 대로 지연된 버퍼의 주소는 버퍼가 언바운드될 때까지 유효해야 합니다.  
  
 특별히 금지되지 않는 한 데이터 버퍼의 주소는 null 포인터가 될 수 있습니다. 드라이버를 통해 데이터를 보내는 데 사용되는 버퍼의 경우 드라이버가 버퍼에 일반적으로 포함된 정보를 무시하게 됩니다. 드라이버에서 데이터를 검색하는 데 사용되는 버퍼의 경우 드라이버가 값을 반환하지 않습니다. 두 경우 모두 드라이버는 해당 데이터 버퍼 길이 인수를 무시합니다.
