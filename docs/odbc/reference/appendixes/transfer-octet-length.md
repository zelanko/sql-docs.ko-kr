---
title: 8 진수 길이 전송 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8f64172685c42a5dde8de9027c8c7e621ddd9f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735069"
---
# <a name="transfer-octet-length"></a>8진수 길이 전송
전송 8 진수 길이 열의 데이터는 기본 C 데이터 형식으로 전송 될 때 응용 프로그램에 반환 된 바이트의 최대입니다. 문자 데이터에 대 한 전송 8 진수 길이 null 종료 문자에 대 한 공간이 포함 되지 않습니다. 열의 전송 8 진수 길이 데이터 원본에서 데이터를 저장 하는 데 필요한 바이트의 수보다 달라질 수 있습니다.  
  
 8 진수 길이 전송 각 ODBC SQL 데이터 형식에 대해 정의 된 다음 표에 표시 됩니다.  
  
|SQL 유형 식별자|길이|  
|-------------------------|------------|  
|모든 문자 형식 [a]|정의 된 또는 바이트의 열 (변수 형식)에 대 한 최대 길이입니다. 설명자 필드 SQL_DESC_OCTET_LENGTH와 동일한 값입니다.|  
|SQL_DECIMAL<br />SQL_NUMERIC|문자 집합을 ANSI 이면이 데이터의 문자 표시를 보유 하는 데 필요한 바이트 수를 두 번이 숫자는 유니코드 문자 집합 데이터를 문자열로 반환 되 고 숫자, 기호와 소수점에 필요한 문자 때문에 두 숫자의 최대 수입니다. 예를 들어 전송 길이의 NUMERIC(10,3)로 정의 된 열은 12입니다.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|문자 집합을 ANSI 이면이 데이터의 문자 표시를 보유 하는 데 필요한 바이트 수 및이 두 배 문자 집합 이므로 경우 유니코드를 기본적으로이 데이터 형식은 문자열로 반환 됩니다. 문자 표현 20 자 이루어져 있습니다. 숫자 및 기호를 서명 하는 경우에 대 한 19 또는 20 자리의 서명 되지 않은 경우. 따라서 길이 20 개입니다.|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|모든 이진 형식 [a]|변수 유형에 대해 최대 문자 수 또는 고정된 유형에 대해 정의 된 저장 하는 데 필요한 바이트 수입니다.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (SQL_DATE_STRUCT 또는 SQL_TIME_STRUCT 구조체의 크기).|  
|SQL_TYPE_TIMESTAMP|16 (SQL_TIMESTAMP_STRUCT 구조체의 크기).|  
|모든 간격 데이터 형식|34 (간격 구조체의 크기).|  
|SQL_GUID|16 (GUID 구조체의 크기).|  
  
 [a] 드라이버 변수 형식에 대 한 열 또는 매개 변수 길이 확인할 수 없습니다, SQL_NO_TOTAL을 반환 합니다.
