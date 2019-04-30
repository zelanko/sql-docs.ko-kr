---
title: 필드를 지연 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c7800e7da867b4eb0c34fa3feeba5edb2d41cd6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049875"
---
# <a name="deferred-fields"></a>지연 필드
값 *필드를 지연* 시간을 설정 하지만 드라이버 지연된 효과 대 한 변수의 주소를 저장 하는 경우에 사용 되지 않습니다. 응용 프로그램 매개 변수 설명자를 드라이버를 사용 하 여 변수의 내용을 호출 시 **SQLExecDirect** 하거나 **SQLExecute**합니다. 응용 프로그램 행 설명자를 드라이버 인출 시 변수의 내용을 사용합니다.  
  
 다음은 지연 된 필드입니다.  
  
-   설명자 레코드의 SQL_DESC_DATA_PTR 및 SQL_DESC_INDICATOR_PTR 필드입니다.  
  
-   응용 프로그램 설명자 레코드의 SQL_DESC_OCTET_LENGTH_PTR 필드입니다.  
  
-   다중 행 페치를 경우 SQL_DESC_ARRAY_STATUS_PTR 및 SQL_DESC_ROWS_PROCESSED_PTR 설명자 헤더 필드입니다.  
  
 설명자 할당 될 때 각 설명자 레코드의 지연 된 필드는 처음에 null 값을 갖습니다. Null 값의 의미는 다음과 같습니다.  
  
-   SQL_DESC_ARRAY_STATUS_PTR에 null 값을 다중 행 인출 행별 진단 정보의이 구성 요소를 반환 되지 않습니다.  
  
-   SQL_DESC_DATA_PTR null 값이 있으면 레코드 바인딩된 아닙니다.  
  
-   카드가의 SQL_DESC_OCTET_LENGTH_PTR 필드에 null 값이 있으면 드라이버는 해당 열에 대 한 길이 정보를 반환 하지 않습니다.  
  
-   드라이버는 APD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 null 값 및 매개 변수는 문자열을 하는 경우 해당 문자열은 null로 끝나는 것을 가정 합니다. 이 필드에 null 값을 출력 동적 매개 변수에 대 한 길이 정보를 반환 합니다. 드라이버를 방지 합니다. (SQL_DESC_TYPE 필드는 문자열 매개 변수를 나타내지 않습니다 SQL_DESC_OCTET_LENGTH_PTR 필드는 무시 됩니다.)  
  
 응용 프로그램 할당을 취소 하거나 필드를 사용 하 여 연결 하는 시간 및 드라이버를 읽거나 씁니다 시간 간의 지연 된 필드에 대해 사용 되는 변수를 삭제 하지 해야 합니다.
