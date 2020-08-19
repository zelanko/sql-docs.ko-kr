---
description: 데이터 버퍼 주소
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 301202933ae9cb0206100b6bbf10dda305495be1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429385"
---
# <a name="data-buffer-address"></a>데이터 버퍼 주소
응용 프로그램은 데이터 버퍼의 주소를 인수 (일반적으로 *이름이 지정 된* 인수)의 드라이버에 전달 합니다. 예를 들어 **SQLBindCol**에 대 한 다음 호출에서 응용 프로그램은 *날짜* 변수의 주소를 지정 합니다.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 버퍼 [할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) 섹션에서 설명한 것 처럼 버퍼를 바인딩 해제할 때까지 지연 된 버퍼의 주소는 유효한 상태로 유지 되어야 합니다.  
  
 특별히 금지 되지 않은 경우 데이터 버퍼의 주소는 null 포인터 일 수 있습니다. 드라이버에 데이터를 전송 하는 데 사용 되는 버퍼의 경우이로 인해 드라이버가 일반적으로 버퍼에 포함 된 정보를 무시 합니다. 드라이버에서 데이터를 검색 하는 데 사용 되는 버퍼의 경우 드라이버에서 값을 반환 하지 않습니다. 두 경우 모두 드라이버는 해당 데이터 버퍼 길이 인수를 무시 합니다.
