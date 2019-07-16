---
title: 열 데이터 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4bc57a5a0b500dc8828d5b0e35c2d6023165ac5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019254"
---
# <a name="column-data"></a>열 데이터
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 캐시 결과 집합에 바인딩된 각 데이터 버퍼에 있는 버퍼를 만듭니다 **SQLBindCol**합니다. 이러한 버퍼의 값을 사용 하 여 생성 하는 **여기서** 절을 위치 지정을 에뮬레이션 하는 경우 update 또는 delete 문. 데이터 원본 및 위치 지정된 update 문을 실행할 때 데이터를 인출 하는 경우 이러한 버퍼는 행 집합 버퍼에서 업데이트 됩니다.  
  
 행 집합 버퍼에서 캐시를 업데이트 하는 커서 라이브러리를 지정 된 C 데이터 형식에 따라 데이터를 전송할 **SQLBindCol**합니다. 예를 들어, C 데이터 형식의 행 집합 버퍼 SQL_C_SLONG 인 커서 라이브러리 4 바이트 데이터 전송 SQL_C_CHAR 경우 및 *BufferLength* 변수가 10, 커서 라이브러리는 10 바이트의 데이터를 전송 합니다. 커서 라이브러리 데이터 전송에 대해 형식 검사 또는 변환을 수행 하지 않습니다.  
  
> [!NOTE]  
>  커서 라이브러리 경우 열에 대 한 해당 캐시를 업데이트 하지 않습니다 **StrLen_or_IndPtr* 해당 행 집합의 버퍼 인지 SQL_DATA_AT_EXEC SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다.  
  
 때 열, 데이터 원본 빈 패드 고정 길이 문자 데이터 및 필요에 따라 0-패드 고정 길이의 이진 데이터 업데이트 합니다. 예를 들어, 데이터 원본 "Smith"으로 CHAR(10) 열에 "Smith"를 저장 합니다. 커서 라이브러리 위치 지정된 update 문을 실행 한 후이 데이터는 캐시에 복사 하는 경우 행 집합 버퍼의 데이터를 빈 패드 또는 0 패딩 되지 않습니다. 따라서 응용 프로그램에는 커서 라이브러리 캐시에 값이 빈 패딩 되거나 0으로 채워집니다가 필요한 경우 해야 빈 패드 또는 0-패드 행 집합 버퍼의 값 위치 지정된 update 문을 실행 하기 전에 합니다.
