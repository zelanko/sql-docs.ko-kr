---
title: 열 데이터의 길이 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d2998eace4772624a1e6590ab2541577147f5c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041614"
---
# <a name="length-of-column-data"></a>열 데이터의 길이
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 **SQLBindCol**를 사용 하 여 결과 집합에 바인딩된 각 길이/표시기 버퍼에 대 한 버퍼를 캐시에 만듭니다. 이러한 버퍼의 값을 사용 하 여 WHERE update 또는 delete 문을 에뮬레이트합니다 **where** 절을 생성 합니다. 데이터 원본에서 데이터를 인출 하 고 위치 지정 update 문을 실행 하는 경우 행 집합 버퍼에서 이러한 버퍼를 업데이트 합니다.  
  
 데이터 버퍼의 C 형식이 SQL_C_CHAR 또는 SQL_C_BINARY이 고 길이/표시기 값이 SQL_NTS 이면 데이터의 문자열 길이가 길이/표시기 버퍼에 배치 됩니다.  
  
> [!NOTE]  
>  해당 행 집합 버퍼의 **StrLen_or_IndPtr* SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과인 경우 커서 라이브러리는 열에 대 한 캐시를 업데이트 하지 않습니다.
