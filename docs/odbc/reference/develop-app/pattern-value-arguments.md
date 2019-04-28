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
manager: craigg
ms.openlocfilehash: 8f4a32d9ab637de5b52466cfcb628a57ff6c044b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861730"
---
# <a name="pattern-value-arguments"></a>패턴 값 인수
와 같은 카탈로그에서 일부 인수 함수는 *TableName* 에서 인수 **SQLTables**, 검색 패턴을 허용 합니다. 이러한 인수는 검색 패턴 수락 SQL_ATTR_METADATA_ID 문 특성 SQL_FALSE;로 설정 된 경우 이들은이 특성이 SQL_TRUE로 설정 된 경우 검색 패턴을 허용 하지 않는 식별자 인수입니다.  
  
 검색 패턴 문자 다음과 같습니다.  
  
-   밑줄 (_), 모든 단일 문자를 나타냅니다.  
  
-   백분율 기호 (%), 0 개 이상의 문자 시퀀스를 나타냅니다.  
  
-   드라이버 관련 되 고 % 서명 밑줄을 포함 하는 데는 이스케이프 문자 및 이스케이프 문자 리터럴로 합니다. 특수 하지 않은 문자를 이스케이프 문자 뒤에 나오는 경우 이스케이프 문자는 특별 한 의미가 없습니다. 이스케이프 문자는 특수 문자 보다 앞에 오면, 특수 문자를 이스케이프 합니다. "\A"를 처리 하는 두 개의 문자로 예를 들어, "\\" 및 "a", 하지만 "\\%" 특수 하지 않은 단일 문자 "%"로 간주 됩니다.  
  
 이스케이프 문자 SQL_SEARCH_PATTERN_ESCAPE 옵션을 사용 하 여 검색 **SQLGetInfo**합니다. 인수는 리터럴 문자를 포함할 검색 패턴을 허용 하는 모든 밑줄, 백분율 기호 또는 이스케이프 문자 야 합니다. 예제는 다음 표에 표시 됩니다.  
  
|검색 패턴|Description|  
|--------------------|-----------------|  
|%A%|문자를 포함 하는 모든 식별자|  
|ABC_|ABC로 시작 하는 모든 4 문자 식별자|  
|ABC\\_|식별자 ABC_, 가정 이스케이프 문자는 백슬래시 (\\)|  
|\\\\%|백슬래시를 사용 하 여 시작 하는 모든 식별자 (\\), 백슬래시는 이스케이프 문자를 가정 합니다.|  
  
 검색 패턴의에서 이스케이프 문자 검색 패턴을 허용 하는 인수에는 특별히 주의 해야 합니다. 식별자에서 일반적으로 사용 되는 밑줄 문자를 사용 하는 경우 특히 그렇습니다. 응용 프로그램에서 일반적인 실수는 카탈로그 함수 중 하나에서 값을 검색 하 고 다른 카탈로그 함수에는 검색 패턴 인수를 해당 값을 전달 하는 것입니다. 예를 들어, 응용 프로그램 검색 결과에서 MY_TABLE 설정에 대 한 테이블 이름을 **SQLTables** 에 전달 **SQLColumns** MY_TABLE의 열 목록을 검색 하려면. MY_TABLE에 대 한 열을 가져오지 대신 응용 프로그램 MY_TABLE, MY1TABLE, MY2TABLE, 등과 같은 MY_TABLE 검색 패턴과 일치 하는 모든 테이블에 대 한 열을 받습니다.  
  
> [!NOTE]
>  ODBC 2입니다. *x* 드라이버의 검색 패턴을 지원 하지 않는 합니다 *CatalogName* 에서 인수 **SQLTables**합니다. ODBC 3 *.x* SQL_OV_ODBC2로 설정 된 경우이 인수에서 검색 패턴을 받지 않는; 드라이버 SQL_ATTR_ ODBC_VERSION 환경 특성 SQL_OV_ODBC3로 설정 된 경우이 인수에서 검색 패턴을 허용 합니다.  
  
 검색 패턴 인수에 null 포인터를 전달 인수;에 지정 된 검색을 제한 하지 않습니다. 즉, null 포인터, 검색 패턴 % (문자가)는 동일 합니다. 그러나-즉, 유효한 포인터에 길이가 0 인 문자열-길이가 0 인 검색 패턴과 일치만 빈 문자열 ("").
