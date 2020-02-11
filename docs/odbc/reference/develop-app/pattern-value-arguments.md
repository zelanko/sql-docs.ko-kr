---
title: 패턴 값 인수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 53c091fd0b7a6cfdf390997fb5163fbc9d98e18c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023347"
---
# <a name="pattern-value-arguments"></a>패턴 값 인수
**Sqltables**의 *TableName* 인수와 같은 카탈로그 함수의 일부 인수는 검색 패턴을 허용 합니다. 이러한 인수는 SQL_ATTR_METADATA_ID statement 특성이 SQL_FALSE로 설정 된 경우 검색 패턴을 허용 합니다. 이 특성이 SQL_TRUE로 설정 된 경우 검색 패턴을 허용 하지 않는 식별자 인수입니다.  
  
 검색 패턴 문자는 다음과 같습니다.  
  
-   단일 문자를 나타내는 밑줄 (_)입니다.  
  
-   0 개 이상의 문자 시퀀스를 나타내는 백분율 기호 (%)입니다.  
  
-   드라이버와 관련 된 이스케이프 문자 이며 밑줄, 백분율 기호 및 이스케이프 문자를 리터럴로 포함 하는 데 사용 됩니다. 이스케이프 문자가 특수 문자가 아닌 문자 앞에 오면 이스케이프 문자에 특별 한 의미가 없습니다. 이스케이프 문자가 특수 문자 앞에 오면 특수 문자를 이스케이프 합니다. 예를 들어 "\a"는 두 문자 "\\" 및 "a"로 처리 되지만 "\\%"는 특수 한 단일 문자 "%"로 처리 됩니다.  
  
 **SQLGetInfo**의 SQL_SEARCH_PATTERN_ESCAPE 옵션을 사용 하 여 이스케이프 문자를 검색 합니다. 해당 문자를 리터럴로 포함 하는 검색 패턴을 허용 하는 인수에서 밑줄, 백분율 기호 또는 이스케이프 문자 앞에와 야 합니다. 다음 표에 예제가 나와 있습니다.  
  
|검색 패턴|Description|  
|--------------------|-----------------|  
|은|문자 A를 포함 하는 모든 식별자|  
|ABC_|ABC로 시작 하는 네 개의 모든 문자 식별자|  
|ABC\\_|식별자 ABC_ (이스케이프 문자는 백슬래시 (\\) 라고 가정 합니다.|  
|\\\\%|백슬래시 (\\)로 시작 하는 모든 식별자 (이스케이프 문자는 백슬래시 라고 가정)|  
  
 검색 패턴을 허용 하는 인수에서 검색 패턴 문자를 이스케이프 하려면 특별 한 주의를 기울여야 합니다. 이는 특히 식별자에 사용 되는 밑줄 문자에 적용 됩니다. 응용 프로그램의 일반적인 실수는 한 카탈로그 함수에서 값을 검색 하 고 해당 값을 다른 카탈로그 함수의 검색 패턴 인수에 전달 하는 것입니다. 예를 들어 응용 프로그램이 **Sqltables** 의 결과 집합에서 MY_TABLE 테이블 이름을 검색 하 고이를 **sqltables** 에 전달 하 여 MY_TABLE에서 열 목록을 검색 한다고 가정 합니다. 응용 프로그램은 MY_TABLE 열을 가져오는 대신 MY_TABLE, MY1TABLE, MY2TABLE 등의 검색 패턴 MY_TABLE 일치 하는 모든 테이블에 대 한 열을 가져옵니다.  
  
> [!NOTE]
>  ODBC 2. *x* 드라이버는 **Sqltables**의 *CatalogName* 인수에서 검색 패턴을 지원 하지 않습니다. ODBC 3.x*드라이버는* SQL_ATTR_ ODBC_VERSION 환경 특성이 SQL_OV_ODBC3으로 설정 된 경우이 인수에 검색 패턴을 적용 합니다. SQL_OV_ODBC2로 설정 된 경우이 인수에서 검색 패턴을 허용 하지 않습니다.  
  
 검색 패턴 인수에 null 포인터를 전달 해도 해당 인수에 대 한 검색은 제한 되지 않습니다. 즉, null 포인터와 검색 패턴% (모든 문자)가 동일 합니다. 그러나 길이가 0 인 검색 패턴 즉, 길이가 0 인 문자열에 대 한 유효한 포인터는 빈 문자열 ("")만 일치 시킵니다.
