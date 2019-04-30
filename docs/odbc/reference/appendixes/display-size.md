---
title: 크기를 표시 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7d4a14a6afc2d716e85e687cbae1a202a596d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241246"
---
# <a name="display-size"></a>표시 크기
열 표시 크기가 문자 형식에서 데이터를 표시 하는 데 필요한 문자의 최대 수입니다. 다음 표에서 각 ODBC SQL 데이터 형식에 대 한 표시 크기를 정의합니다.  
  
|SQL 유형 식별자|표시 크기|  
|-------------------------|------------------|  
|모든 문자 형식 [a]|고정 된 유형에 대해 정의 된 또는 변수 유형에 대해 최대 문자 형식에서 데이터를 표시 하는 데 필요한 문자 수입니다.|  
|SQL_DECIMAL SQL_NUMERIC|열 2의 전체 자릿수 (기호, a *정밀도* 숫자와 소수점). 예를 들어 표시 크기 NUMERIC(10,3)로 정의 된 열은 12입니다.|  
|SQL_BIT|1 (1 자리 숫자)입니다.|  
|SQL_TINYINT|4 (로그인 및 3 자리 숫자)를 서명 하는 경우 또는 (3 자리 숫자) 서명 되지 않은 경우 3입니다.|  
|SQL_SMALLINT|(로그인 및 5 자리 숫자)를 서명 하는 경우에 6 또는 5 (5 자리 숫자) 서명 되지 않은 경우.|  
|SQL_INTEGER|(부호 및 10 진수)를 서명 하는 경우 11 또는 10 (10 자리) 서명 되지 않은 경우.|  
|SQL_BIGINT|20 (로그인 및 서명 하는 경우에 19 자리 또는 20 자리의 서명 되지 않은 경우).|  
|SQL_REAL|14 (로그인, 7 자리 숫자, 소수점, 문자 *E*, 기호와 2 자리).|  
|SQL_FLOAT SQL_DOUBLE|24 (기호를 15 자릿수, 소수점, 문자 *E*, 기호와 3 자리 숫자)입니다.|  
|모든 이진 형식 [a]|정의 또는 변수 유형에 대해 최대 열 길이 2 시간입니다. (각 이진 바이트는 2 자리 16 진수 숫자로 표시 됩니다.)|  
|SQL_TYPE_DATE|10 (형식으로 날짜 *yyyy-월-일*).|  
|SQL_TYPE_TIME|8 (형식에서 한 번 *hh: mm:*)<br /><br /> -또는-<br /><br /> 9 + *s* (형식으로 시간 *hh: mm:*[.fff...] 여기서 *s* 소수 자릿수 초의 전체 자릿수)입니다.|  
|SQL_TYPE_TIMESTAMP|19 (타임 스탬프에 대 한 합니다 *h:mm: ss yyyy-월-일* 형식)<br /><br /> -또는-<br /><br /> 20 + *s* (타임 스탬프에 대 한 합니다 *h:mm: ss yyyy-월-일*[.fff...] 형식으로 여기서 *s* 소수 자릿수 초의 전체 자릿수)입니다.|  
|모든 간격 데이터 형식|참조 [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md)입니다.|  
|SQL_GUID|36 (문자 수를 *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* 형식|  
  
 [a] 드라이버 변수 형식의 열 또는 매개 변수 길이 확인할 수 없습니다, SQL_NO_TOTAL을 반환 합니다.
