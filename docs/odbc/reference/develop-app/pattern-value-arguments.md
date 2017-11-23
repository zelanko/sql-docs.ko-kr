---
title: "값 인수 패턴 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 28caa361e4363aa2224d6cfa63a8830675aeece8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="pattern-value-arguments"></a>패턴 값 인수
와 같은 일부 인수 카탈로그에서 함수가 *TableName* 인수 **SQLTables**, 검색 패턴을 사용할 합니다. 이 인수는 검색 패턴을 사용할 SQL_ATTR_METADATA_ID 문 특성이 SQL_FALSE;로 설정 된 경우 이 특성은 SQL_TRUE로 설정 하는 경우 검색 패턴을 허용 하지 않는 식별자 인수 않은 것입니다.  
  
 검색 패턴 문자에는  
  
-   밑줄 (_), 모든 단일 문자를 나타냅니다.  
  
-   백분율 기호 (%), 0 개 이상의 문자로 구성 된 시퀀스를 나타냅니다.  
  
-   드라이버 관련 되 고 % 서명 밑줄을 포함 하는 데 사용 되는 이스케이프 문자 및 이스케이프 문자를 리터럴로 합니다. 이스케이프 문자는 특수 하지 않은 문자 뒤에 나오는 경우 이스케이프 문자는 특별 한 의미가 없습니다. 이스케이프 문자는 특수 문자 뒤에 나오는 경우 특수 문자를 이스케이프 합니다. 두 개의 문자로 처리 됩니다 "\a" 예를 들어 "\\" 및 "a", 하지만 "\\%" 특수 하지 않은 단일 문자 "%"로 처리 됩니다.  
  
 이스케이프 문자 SQL_SEARCH_PATTERN_ESCAPE 옵션에서 검색 됩니다 **SQLGetInfo**합니다. 그 앞에 야 모든 밑줄, 백분율 기호 또는 이스케이프 문자 리터럴 문자를 포함할 검색 패턴을 허용 하는 인수에 있습니다. 예제는 다음 표에 표시 됩니다.  
  
|검색 패턴|Description|  
|--------------------|-----------------|  
|% A %|문자 A를 포함 하는 모든 식별자입니다.|  
|ABC_|ABC로 시작 하는 모든 4 가지 문자 식별자|  
|ABC\\_|이스케이프 문자를 가정 ABC_ 식별자는 백슬래시 (\\)|  
|\\\\%|백슬래시로 시작 하는 모든 식별자 (\\), 백슬래시는 이스케이프 문자를 가정 합니다.|  
  
 검색 패턴의에서 이스케이프 문자 검색 패턴을 허용 하는 인수를 특별히 주의 해야 합니다. 식별자에서 일반적으로 사용 되는 밑줄 문자에 대 한 경우 특히 그렇습니다. 응용 프로그램에서 일반적인 실수는 하나의 카탈로그 함수에서 값을 검색 하 고 다른 카탈로그 함수에서는 검색 패턴 인수에 해당 값을 전달 하는 것입니다. 예를 들어, 응용 프로그램 검색 결과에서 MY_TABLE 설정에 대 한 테이블 이름 **SQLTables** 전달 하려면이 **SQLColumns** MY_TABLE에 있는 열의 목록을 검색할 수 있습니다. 대신, MY_TABLE에 대 한 열을 가져올 응용 프로그램 MY_TABLE, MY1TABLE, MY2TABLE, 등 MY_TABLE 검색 패턴과 일치 하는 모든 테이블의 열을을 받습니다.  
  
> [!NOTE]  
>  ODBC 2입니다. *x* 드라이버의 검색 패턴을 지원 하지 않습니다는 *CatalogName* 인수 **SQLTables**합니다. ODBC 3*.x* SQL_OV_ODBC2로 설정 된 경우이 인수의 검색 패턴을 받지 않는; 드라이버 SQL_ATTR_ ODBC_VERSION 환경 특성이 SQL_OV_ODBC3로 설정 된 경우이 인수의 검색 패턴을 허용 합니다.  
  
 Null 포인터는 검색 패턴 인수를 전달 인수에 지정 된;에 대 한 검색을 제한 하지 않습니다. 즉, null 포인터와 검색 패턴 % (문자)는 동일 합니다. 길이가 0 인 패턴을 검색 하는 반면-즉,에 대 한 유효한 포인터는 문자열 길이 0-빈 문자열만 일치 ("").
