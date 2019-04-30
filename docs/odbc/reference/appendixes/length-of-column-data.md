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
manager: craigg
ms.openlocfilehash: 6d14fa4303dd1f67a77bf14dcebeeb933ccce9e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188832"
---
# <a name="length-of-column-data"></a>열 데이터의 길이
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 캐시 결과 집합을 바인딩할 각 길이/표시기 버퍼에 있는 버퍼를 만듭니다 **SQLBindCol**합니다. 생성 하려면이 버퍼의 값을 사용 된 **여기서** 에뮬레이션 위치 지정된 업데이트 또는 delete 문의 경우 절. 데이터 원본 및 위치 지정된 update 문을 실행할 때 데이터를 인출 하는 경우 이러한 버퍼는 행 집합 버퍼에서 업데이트 됩니다.  
  
 데이터 버퍼의 C 형식이 SQL_C_CHAR 또는 SQL_C_BINARY 길이/표시기 값은 SQL_NTS을 하는 경우 데이터의 문자열 길이 길이/표시기 버퍼에 배치 됩니다.  
  
> [!NOTE]  
>  커서 라이브러리 경우 열에 대 한 해당 캐시를 업데이트 하지 않습니다 **StrLen_or_IndPtr* 해당 행 집합의 버퍼 인지 SQL_DATA_AT_EXEC SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다.
