---
title: 열 데이터의 길이 | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e53cd64eaa0afb2ba042190b0649721c65979de7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="length-of-column-data"></a>열 데이터의 길이
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 상태로 결과 집합에 바인딩된 각 길이/표시기 버퍼 캐시에는 버퍼를 만들고 **SQLBindCol**합니다. 생성 하려면 이러한 버퍼에 값을 사용는 **여기서** 에뮬레이트하 위치 지정된 업데이트 또는 delete 문 절. 위치 지정된 update 문을 실행할 때 데이터 원본에서 데이터를 인출할 때 행 집합 버퍼에서 이러한 버퍼를 업데이트 합니다.  
  
 데이터 버퍼의 C 형식이 SQL_C_CHAR 또는 SQL_C_BINARY 길이/표시기 값은 SQL_NTS 하는 경우 데이터의 문자열 길이 길이/표시기 버퍼에 배치 됩니다.  
  
> [!NOTE]  
>  커서 라이브러리 경우 열에 대 한 캐시를 업데이트 하지 않습니다 **StrLen_or_IndPtr* 해당 행 집합의 버퍼는 SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다.
