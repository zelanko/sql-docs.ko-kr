---
title: 이연 필드 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 094aba353e10ed568e1959b1d655109296507dee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305974"
---
# <a name="deferred-fields"></a>지연 필드
*지연된 필드의* 값은 설정될 때 사용되지 않지만 드라이버는 지연된 효과에 대한 변수의 주소를 저장합니다. 응용 프로그램 매개 변수 설명자의 경우 드라이버는 **SQLExecDirect** 또는 **SQLExecute**에 대한 호출 시 변수의 내용을 사용합니다. 응용 프로그램 행 설명자의 경우 드라이버는 가져오기 시 변수의 내용을 사용합니다.  
  
 다음은 지연된 필드입니다.  
  
-   설명자 레코드의 SQL_DESC_DATA_PTR 및 SQL_DESC_INDICATOR_PTR 필드입니다.  
  
-   응용 프로그램 설명자 레코드의 SQL_DESC_OCTET_LENGTH_PTR 필드입니다.  
  
-   다중 행 가져오기의 경우 설명자 헤더의 SQL_DESC_ARRAY_STATUS_PTR 및 SQL_DESC_ROWS_PROCESSED_PTR 필드입니다.  
  
 설명자가 할당되면 각 설명자 레코드의 지연된 필드에는 처음에 null 값이 있습니다. null 값의 의미는 다음과 같습니다.  
  
-   SQL_DESC_ARRAY_STATUS_PTR null 값이 있는 경우 multirow fetch는 행별 진단 정보의 이 구성 요소를 반환하지 못합니다.  
  
-   SQL_DESC_DATA_PTR null 값이 있으면 레코드가 언바운드됩니다.  
  
-   ARD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 null 값이 있는 경우 드라이버는 해당 열에 대한 길이 정보를 반환하지 않습니다.  
  
-   APD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 null 값이 있고 매개 변수가 문자 문자열인 경우 드라이버는 해당 문자열이 null-terminated라고 가정합니다. 출력 동적 매개 변수의 경우 이 필드의 null 값은 드라이버가 길이 정보를 반환하지 못하도록 합니다. SQL_DESC_TYPE 필드가 character-string 매개 변수를 나타내지 않으면 SQL_DESC_OCTET_LENGTH_PTR 필드는 무시됩니다.  
  
 응용 프로그램은 지연된 필드에 사용되는 변수를 필드와 연결하는 시간과 드라이버가 읽거나 쓰는 시간 사이에 변수를 할당 하거나 삭제해서는 안 됩니다.
