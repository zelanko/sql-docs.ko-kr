---
title: 열 데이터 | Microsoft Docs
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
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1aa5125d58c2d630a9233b5564ad3c58203a669f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="column-data"></a>열 데이터
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 상태로 결과 집합에 바인딩된 각 데이터 버퍼에 대 한 캐시에는 버퍼를 만들고 **SQLBindCol**합니다. 생성 하려면 이러한 버퍼에 값을 사용 하기는 **여기서** 절을 위치 지정을 에뮬레이션 하는 경우 업데이트 또는 삭제 문의 합니다. 위치 지정된 update 문을 실행할 때 데이터 원본에서 데이터를 인출할 때 행 집합 버퍼에서 이러한 버퍼를 업데이트 합니다.  
  
 행 집합 버퍼에서 캐시를 업데이트 하는 커서 라이브러리에 지정 된 C 데이터 형식에 따라 데이터 전송할 **SQLBindCol**합니다. 예를 들어 행 집합 버퍼의 C 데이터 형식 SQL_C_SLONG 이면 커서 라이브러리 4 바이트의 데이터 전송 SQL_C_CHAR 이면 및 *BufferLength* 변수가 10, 10 바이트의 데이터를 전송 하는 커서 라이브러리입니다. 커서 라이브러리 전송 데이터에 대해 형식 검사 또는 변환을 수행 하지 않습니다.  
  
> [!NOTE]  
>  커서 라이브러리 경우 열에 대 한 캐시를 업데이트 하지 않습니다 **StrLen_or_IndPtr* 해당 행 집합의 버퍼는 SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다.  
  
 때 하나의 열, 데이터 원본 blank 패드 고정 길이 문자 데이터 및 필요에 따라 0 패드 고정 길이 이진 데이터 업데이트 합니다. 예를 들어 데이터 원본 "Smith"로 char (10) 열에 "Smith"를 저장합니다. 커서 라이브러리 위치 지정된 update 문을 실행 한 후이 데이터는 캐시를 복사 하는 경우 빈 값 패드 또는 영 (0) 하지 버퍼의에서 데이터는 행 집합을 수행 합니다. 따라서 응용 프로그램 필요한 경우 빈 값을 채우는 또는 0을 채우는 커서 라이브러리의 캐시에 값으로, 다음 조건을 충족 해야 blank 패드 또는 영 (0) 행 집합 버퍼에 값 위치 지정된 update 문을 실행 하기 전에.
