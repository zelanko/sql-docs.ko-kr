---
description: 표시 크기
title: 표시 크기 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 747c2076c528df8c312c9b3ed45e45a165299d59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456588"
---
# <a name="display-size"></a>표시 크기
열의 표시 크기는 문자 형식으로 데이터를 표시 하는 데 필요한 최대 문자 수입니다. 다음 표에서는 각 ODBC SQL 데이터 형식에 대 한 표시 크기를 정의 합니다.  
  
|SQL 유형 식별자|표시 크기|  
|-------------------------|------------------|  
|모든 문자 형식 [a]|문자 형식으로 데이터를 표시 하는 데 필요한 문자 수 (고정 형식의 경우) 또는 최대값 (변수 형식의 경우)입니다.|  
|SQL_DECIMAL SQL_NUMERIC|열의 전체 자릿수에 2 (부호, *전체 자릿수* , 소수 자릿수)를 더한 값입니다. 예를 들어 숫자 (10, 3)로 정의 된 열의 표시 크기는 12입니다.|  
|SQL_BIT|1 자리 숫자입니다.|  
|SQL_TINYINT|부호 있는 경우 4 (부호 및 3 자리) 또는 3 자리 부호 없는 경우 3입니다.|  
|SQL_SMALLINT|부호 있는 경우 6 (부호 및 5 자리)이 고 부호 없는 경우 5 (5 자리)입니다.|  
|SQL_INTEGER|부호 있는 경우 11 (부호 및 10 자리)이 고 부호 없는 경우 10 (10 자리)입니다.|  
|SQL_BIGINT|20 (부호가 있으면 부호 및 19 자리, 부호 없는 경우 20 자리)|  
|SQL_REAL|14 (부호, 7 자리, 소수점, 문자 *E*, 부호 및 2 자리)입니다.|  
|SQL_FLOAT SQL_DOUBLE|24 (부호, 15 자리, 소수점, 문자 *E*, 부호 및 3 자리)|  
|모든 이진 형식 [a]|열 시간 2의 정의 된 또는 최대값 (변수 형식의 경우) 길이입니다. 각 이진 바이트는 2 자리 16 진수 숫자로 표시 됩니다.|  
|SQL_TYPE_DATE|10 ( *yyyy-mm-dd*형식의 날짜).|  
|SQL_TYPE_TIME|8 ( *hh: mm: ss*형식의 시간)<br /><br /> -또는-<br /><br /> 9 + *s* ( *hh: mm: ss*[. fff ...] 형식의 시간). 여기서 *s* 는 소수 자릿수 초의 전체 자릿수입니다.|  
|SQL_TYPE_TIMESTAMP|19 ( *yyyy-mm-dd hh: mm: ss* 형식의 타임 스탬프)<br /><br /> -또는-<br /><br /> 20 + *s* ( *yyyy-mm-dd hh: mm: ss*[. fff ...] 형식의 타임 스탬프). 여기서 *s* 는 소수 자릿수 초의 전체 자릿수입니다.|  
|모든 interval 데이터 형식|[Interval 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md)를 참조 하세요.|  
|SQL_GUID|36 ( *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* 형식의 문자 수|  
  
 [a] 드라이버에서 변수 형식의 열 또는 매개 변수 길이를 확인할 수 없는 경우 SQL_NO_TOTAL 반환 합니다.
