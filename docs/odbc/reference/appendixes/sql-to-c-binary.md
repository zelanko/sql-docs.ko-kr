---
description: 'SQL에서 C로: 이진'
title: 'SQL에서 C로: Binary | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 229611308c2dba83a8d793810eb5a5443cbd7062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456556"
---
# <a name="sql-to-c-binary"></a>SQL에서 C로: 이진
이진 ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 다음 표에서는 이진 SQL 데이터가 변환 될 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(데이터의 바이트 길이) \* 2tb < *Bufferlength*<br /><br /> (데이터의 바이트 길이) \* 2 >= *Bufferlength*|데이터<br /><br /> 잘린 데이터|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)|해당 없음<br /><br /> 01004|  
|SQL_C_WCHAR|(데이터의 문자 길이) \* 2tb < *Bufferlength*<br /><br /> (데이터의 문자 길이) \* 2 >= *Bufferlength*|데이터<br /><br /> 잘린 데이터|데이터의 길이 (문자)<br /><br /> 데이터의 길이 (문자)|해당 없음<br /><br /> 01004|  
|SQL_C_BINARY|데이터의 바이트 길이 <= *Bufferlength*<br /><br /> *Bufferlength* > 데이터의 바이트 길이|데이터<br /><br /> 잘린 데이터|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)|해당 없음<br /><br /> 01004|  
  
 이진 SQL 데이터가 문자 C 데이터로 변환 되는 경우 원본 데이터의 각 바이트 (8 비트)는 두 개의 ASCII 문자로 표시 됩니다. 이러한 문자는 16 진수 형식으로 된 숫자의 ASCII 문자 표현입니다. 예를 들어, 이진 00000001은 "01"로 변환 되 고 이진 11111111은 "FF"로 변환 됩니다.  
  
 드라이버는 항상 개별 바이트를 16 진수 숫자로 변환 하 고 문자열을 null 바이트를 사용 하 여 종료 합니다. 이 때문에 *Bufferlength* 가 짝수이 고 변환 된 데이터의 길이 보다 작은 경우 **Targetvalueptr* 버퍼의 마지막 바이트가 사용 되지 않습니다. 변환 된 데이터에는 짝수 바이트가 필요 하 고, 다음에서 마지막 바이트는 null 바이트 이며, 마지막 바이트를 사용할 수 없습니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자는 이진 SQL 데이터를 문자 C 데이터 형식에 바인딩하는 것을 권장 하지 않습니다. 일반적으로 이러한 변환은 비효율적 이며 느립니다.
