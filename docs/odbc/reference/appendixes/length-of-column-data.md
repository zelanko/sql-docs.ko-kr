---
title: 열 데이터의 길이 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d0b7ad515661cce4c5b1d407be768cc3da131bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304934"
---
# <a name="length-of-column-data"></a>열 데이터의 길이
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 커서 라이브러리는 **SQLBindCol로**결과 집합에 바인딩된 각 길이/표시기 버퍼에 대한 버퍼를 캐시에 만듭니다. 이러한 버퍼의 값을 사용하여 위치 업데이트 또는 삭제 문을 에뮬레이트할 때 **WHERE** 절을 생성합니다. 데이터 원본에서 데이터를 가져오고 위치 가 있는 업데이트 문을 실행할 때 행 집합 버퍼에서 이러한 버퍼를 업데이트합니다.  
  
 데이터 버퍼의 C 형식이 SQL_C_CHAR 또는 SQL_C_BINARY 길이/표시기 값이 SQL_NTS 경우 데이터의 문자열 길이가 길이/표시기 버퍼에 배치됩니다.  
  
> [!NOTE]  
>  해당 행 집합 버퍼의*StrLen_or_IndPtr* SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과인 경우 커서 라이브러리는 열에 대한 캐시를 업데이트하지 않습니다.
