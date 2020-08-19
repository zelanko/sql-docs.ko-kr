---
description: 열 데이터
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f4ea57de9dfefd21b6d71bb3b248d5aed5dd50d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449005"
---
# <a name="column-data"></a>열 데이터
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 **SQLBindCol**를 사용 하 여 결과 집합에 바인딩된 각 데이터 버퍼에 대 한 버퍼를 캐시에 만듭니다. 이러한 버퍼의 값을 사용 하 여 위치 지정 update 또는 delete 문을 에뮬레이트하는 **where** 절을 생성 합니다. 데이터 원본에서 데이터를 인출 하 고 위치 지정 update 문을 실행 하는 경우 행 집합 버퍼에서 이러한 버퍼를 업데이트 합니다.  
  
 커서 라이브러리는 행 집합 버퍼에서 캐시를 업데이트할 때 **SQLBindCol**에 지정 된 C 데이터 형식에 따라 데이터를 전송 합니다. 예를 들어 행 집합 버퍼의 C 데이터 형식이 SQL_C_SLONG 경우 커서 라이브러리는 4 바이트의 데이터를 전송 합니다. SQL_C_CHAR 하 고 *Bufferlength* 가 10 이면 커서 라이브러리는 10 바이트의 데이터를 전송 합니다. 커서 라이브러리는 전송 하는 데이터에 대 한 형식 검사 또는 변환을 수행 하지 않습니다.  
  
> [!NOTE]  
>  해당 행 집합 버퍼의 **StrLen_or_IndPtr* SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과인 경우 커서 라이브러리는 열에 대 한 캐시를 업데이트 하지 않습니다.  
  
 열을 업데이트 하는 경우 데이터 원본은 고정 길이 문자 데이터를 입력 하 고 필요에 따라 0 채움 고정 길이 이진 데이터를 채웁니다. 예를 들어 데이터 원본은 CHAR (10) 열에 "smith"를 "Smith"로 저장 합니다. 커서 라이브러리는 위치 지정 update 문을 실행 한 후이 데이터를 캐시에 복사할 때 행 집합 버퍼에서 데이터를 입력 하거나 패딩 하지 않습니다. 따라서 응용 프로그램에서 커서 라이브러리의 캐시에 있는 값이 비어 있거나 0으로 채워져 있어야 하는 경우에는 위치 지정 update 문을 실행 하기 전에 행 집합 버퍼에서 값을 비워 둘 수 있습니다.
