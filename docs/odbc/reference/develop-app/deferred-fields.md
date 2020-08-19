---
description: 지연 필드
title: 지연 필드 | Microsoft Docs
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
ms.openlocfilehash: f8b313f2d77270e95830de1a524706aa7fe36e33
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424695"
---
# <a name="deferred-fields"></a>지연 필드
*지연 된 필드* 값은 설정 될 때 사용 되지 않지만 드라이버는 지연 된 효과에 대 한 변수 주소를 저장 합니다. 응용 프로그램 매개 변수 설명자의 경우, 드라이버는 **Sqlexecdirect** 또는 **sqlexecute**를 호출할 때 변수의 내용을 사용 합니다. 응용 프로그램 행 설명자의 경우 드라이버는 인출 시 변수의 내용을 사용 합니다.  
  
 연기 된 필드는 다음과 같습니다.  
  
-   설명자 레코드의 SQL_DESC_DATA_PTR 및 SQL_DESC_INDICATOR_PTR 필드입니다.  
  
-   응용 프로그램 설명자 레코드의 SQL_DESC_OCTET_LENGTH_PTR 필드입니다.  
  
-   다중 행 페치의 경우 설명자 헤더의 SQL_DESC_ARRAY_STATUS_PTR 및 SQL_DESC_ROWS_PROCESSED_PTR 필드가 있습니다.  
  
 설명자가 할당 될 때 각 설명자 레코드의 지연 된 필드는 처음에 null 값을 갖습니다. Null 값의 의미는 다음과 같습니다.  
  
-   SQL_DESC_ARRAY_STATUS_PTR에 null 값이 있는 경우 다중 행 페치에서 행 단위 진단 정보의이 구성 요소를 반환 하지 못합니다.  
  
-   SQL_DESC_DATA_PTR에 null 값이 있으면 해당 레코드는 바인딩되지 않습니다.  
  
-   SQL_DESC_OCTET_LENGTH_PTR 필드의 값이 null 이면 드라이버는 해당 열에 대 한 길이 정보를 반환 하지 않습니다.  
  
-   APD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 null 값이 있고 매개 변수가 문자열이 면 드라이버는 문자열이 null로 종료 된 것으로 가정 합니다. 출력 동적 매개 변수의 경우이 필드에 null 값이 있으면 드라이버가 길이 정보를 반환 하지 않습니다. SQL_DESC_TYPE 필드가 문자 문자열 매개 변수를 나타내지 않는 경우에는 SQL_DESC_OCTET_LENGTH_PTR 필드가 무시 됩니다.)  
  
 응용 프로그램은 필드에 연결 하는 시간과 드라이버가 읽거나 쓰는 시간 사이에 지연 된 필드에 사용 되는 변수를 할당 취소 하거나 취소 하지 않아야 합니다.
