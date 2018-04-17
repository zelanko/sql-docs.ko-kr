---
title: 필드를 지연 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47e9d94d3a3f6e39864d27fee1c82f8e69f24b37
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="deferred-fields"></a>지연 된 필드
값 *필드 지연* 시간을 설정 하지만 드라이버는 지연 된 효과 대 한 변수의 주소를 저장 하는 경우에 사용 되지 않습니다. 변수의 내용을에 대 한 호출 시 드라이버는 응용 프로그램 매개 변수 설명자에 대 한 사용 **SQLExecDirect** 또는 **SQLExecute**합니다. 응용 프로그램 행 설명자를 사용 하는 드라이버 변수의 내용을 인출 시간에 사용합니다.  
  
 다음은 지연 된 필드입니다.  
  
-   설명자 레코드의 SQL_DESC_DATA_PTR 및 SQL_DESC_INDICATOR_PTR 필드.  
  
-   응용 프로그램 설명자 레코드의 SQL_DESC_OCTET_LENGTH_PTR 필드입니다.  
  
-   다중 행 인출의 경우 설명자 헤더의 SQL_DESC_ARRAY_STATUS_PTR 및 SQL_DESC_ROWS_PROCESSED_PTR 필드입니다.  
  
 설명자가 할당 되 면 각 설명자 레코드의 지연 된 필드는 처음에 null 값을 갖습니다. Null 값의 의미는 다음과 같습니다.  
  
-   SQL_DESC_ARRAY_STATUS_PTR null 값이 있으면 다중 행 인출 행별 진단 정보의이 구성 요소를 반환 하는 실패 합니다.  
  
-   SQL_DESC_DATA_PTR null 값이 있으면 레코드 바인딩된 않습니다.  
  
-   카드가의 SQL_DESC_OCTET_LENGTH_PTR 필드에 null 값이 있으면 드라이버는 해당 열에 대 한 길이 정보를 반환 하지 않습니다.  
  
-   매개 변수는 문자열이 APD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 null 값을 해당 문자열은 null로 끝나는 드라이버 가정 합니다. 이 필드에 null 값을 출력 동적 매개 변수에 대 한 길이 정보를 반환 합니다. 드라이버를 방지 합니다. (SQL_DESC_TYPE 필드는 문자열 매개 변수를 나타내지 않습니다 SQL_DESC_OCTET_LENGTH_PTR 필드는 무시 됩니다.)  
  
 응용 프로그램 하지 할당을 취소 하거나 필드와 함께 연결 시간 및 드라이버를 읽거나 씁니다 시간 간의 지연 된 필드에 대해 사용 되는 변수를 삭제 해야 합니다.
