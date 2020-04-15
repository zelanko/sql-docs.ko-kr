---
title: 열 데이터 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff89566efa65c88325d98422fe17788f27d2c8ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306594"
---
# <a name="column-data"></a>열 데이터
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 커서 라이브러리는 **SQLBindCol로**결과 집합에 바인딩된 각 데이터 버퍼에 대한 버퍼를 캐시에 만듭니다. 이러한 버퍼의 값을 사용하여 위치 가 있는 업데이트 또는 delete 문을 에뮬레이트할 때 **WHERE** 절을 생성합니다. 데이터 원본에서 데이터를 가져오고 위치 가 있는 업데이트 문을 실행할 때 행 집합 버퍼에서 이러한 버퍼를 업데이트합니다.  
  
 커서 라이브러리가 행 집합 버퍼에서 캐시를 업데이트하면 **SQLBindCol**에 지정된 C 데이터 형식에 따라 데이터를 전송합니다. 예를 들어 행 집합 버퍼의 C 데이터 형식이 SQL_C_SLONG 커서 라이브러리는 4바이트의 데이터를 전송합니다. SQL_C_CHAR *버퍼길이10이면* 커서 라이브러리는 10바이트의 데이터를 전송합니다. 커서 라이브러리는 전송하는 데이터에 대한 형식 검사 또는 변환을 수행하지 않습니다.  
  
> [!NOTE]  
>  해당 행 집합 버퍼의*StrLen_or_IndPtr* SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과인 경우 커서 라이브러리는 열에 대한 캐시를 업데이트하지 않습니다.  
  
 열을 업데이트할 때 데이터 원본 은 고정 길이 문자 데이터와 필요에 따라 고정 길이 이진 데이터를 고정 패드로 고정합니다. 예를 들어 데이터 원본은 CHAR(10) 열에 "Smith"를 "Smith"로 저장합니다. 커서 라이브러리는 위치 가 있는 업데이트 문을 실행한 후 이 데이터를 캐시에 복사할 때 행 집합 버퍼의 빈 패드 또는 제로 패드 데이터를 사용하지 않습니다. 따라서 응용 프로그램에서 커서 라이브러리의 캐시의 값이 빈 패딩 또는 0 패딩된 값이어야 하는 경우 위치 지정 업데이트 문을 실행하기 전에 행 집합 버퍼의 값을 블랭크 패드 또는 제로 패드로 표시해야 합니다.
