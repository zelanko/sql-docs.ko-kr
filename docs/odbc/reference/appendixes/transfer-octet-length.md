---
description: 8진수 길이 전송
title: 전송 옥텟 길이 | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c89a9cb1423693e7d92114233f967d6fb5dcee1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386349"
---
# <a name="transfer-octet-length"></a>8진수 길이 전송
열의 전송 옥텟 길이는 데이터를 기본 C 데이터 형식으로 전송할 때 응용 프로그램에 반환 되는 최대 바이트 수입니다. 문자 데이터의 경우 전송 8 진수 길이는 null 종료 문자에 대 한 공간을 포함 하지 않습니다. 열의 전송 옥텟 길이는 데이터 원본에 데이터를 저장 하는 데 필요한 바이트 수와 다를 수 있습니다.  
  
 각 ODBC SQL 데이터 형식에 대해 정의 된 전송 옥텟 길이는 다음 표에 나와 있습니다.  
  
|SQL 유형 식별자|길이|  
|-------------------------|------------|  
|모든 문자 형식 [a]|열의 정의 된 또는 최대값 (변수 형식의 경우) 길이 (바이트)입니다. SQL_DESC_OCTET_LENGTH 설명자 필드와 동일한 값입니다.|  
|SQL_DECIMAL<br />SQL_NUMERIC|문자 집합이 ANSI 이면이 데이터의 문자 표현을 보유 하는 데 필요한 바이트 수이 고, 문자 집합이 UNICODE 이면이 숫자의 두 배입니다. 데이터는 문자열로 반환 되 고 숫자, 부호 및 소수점에는 문자가 필요 하기 때문에이 값은 최대 자릿수에 2를 더한 값입니다. 예를 들어 숫자 (10, 3)로 정의 된 열의 전송 길이는 12입니다.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|모든 이진 형식 [a]|정의 된을 보유 하는 데 필요한 바이트 수 (고정 형식의 경우) 또는 최대 (변수 형식)의 문자 수입니다.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (SQL_DATE_STRUCT 또는 SQL_TIME_STRUCT 구조의 크기)|  
|SQL_TYPE_TIMESTAMP|16 (SQL_TIMESTAMP_STRUCT 구조체의 크기)|  
|모든 interval 데이터 형식|34 (간격 구조의 크기)|  
|SQL_GUID|16 (GUID 구조의 크기)|  
| &nbsp; | &nbsp; |

 [a] 드라이버에서 변수 형식의 열 또는 매개 변수 길이를 확인할 수 없는 경우 SQL_NO_TOTAL 반환 합니다.
