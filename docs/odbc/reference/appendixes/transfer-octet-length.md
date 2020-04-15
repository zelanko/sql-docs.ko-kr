---
title: 전송 옥텟 길이 | 마이크로 소프트 문서
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
ms.openlocfilehash: 4204b47816747506a5672241eeeef736eca54856
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302814"
---
# <a name="transfer-octet-length"></a>8진수 길이 전송
열의 전송 옥텟 길이는 데이터가 기본 C 데이터 유형으로 전송될 때 응용 프로그램에 반환되는 최대 바이트 수입니다. 문자 데이터의 경우 전송 옥텟 길이에는 null 종료 문자에 대한 공백이 포함되지 않습니다. 열의 전송 옥텟 길이는 데이터 원본에 데이터를 저장하는 데 필요한 바이트 수와 다를 수 있습니다.  
  
 각 ODBC SQL 데이터 형식에 대해 정의된 전송 옥텟 길이는 다음 표에 나와 있습니다.  
  
|SQL 유형 식별자|길이|  
|-------------------------|------------|  
|모든 문자 유형[a]|정의된 또는 최대(가변 형식의 경우) 열의 길이(가변 형식)입니다. 이 값은 설명자 필드 SQL_DESC_OCTET_LENGTH 동일한 값입니다.|  
|SQL_DECIMAL<br />SQL_NUMERIC|문자 집합이 ANSI인 경우 이 데이터의 문자 표현을 유지하는 데 필요한 바이트 수와 문자 집합이 UNICODE인 경우 이 숫자의 두 배입니다. 데이터가 문자 문자열로 반환되고 숫자, 기호 및 소수점에 문자가 필요하기 때문에 최대 숫자 수와 두 자리입니다. 예를 들어 NUMERIC(10,3)으로 정의된 열의 전송 길이는 12입니다.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|모든 바이너리 유형[a]|정의된(고정 형식의 경우) 또는 최대(변수 형식의 경우) 문자 수를 유지하는 데 필요한 바이트 수입니다.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (SQL_DATE_STRUCT 또는 SQL_TIME_STRUCT 구조의 크기).|  
|SQL_TYPE_TIMESTAMP|16 (SQL_TIMESTAMP_STRUCT 구조의 크기).|  
|모든 간격 데이터 형식|34(간격 구조의 크기).|  
|SQL_GUID|16(GUID 구조의 크기).|  
| &nbsp; | &nbsp; |

 [a] 드라이버가 변수 형식의 열 또는 매개 변수 길이를 확인할 수 없는 경우 SQL_NO_TOTAL 반환합니다.
