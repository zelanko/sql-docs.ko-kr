---
title: 패턴 값 인수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b8e7b7de64d8051118089a54cf14eb45dc96f74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282383"
---
# <a name="pattern-value-arguments"></a>패턴 값 인수
**SQLTable의** *TableName* 인수와 같은 카탈로그 함수의 일부 인수는 검색 패턴을 허용합니다. 이러한 인수는 SQL_ATTR_METADATA_ID 문 특성이 SQL_FALSE 설정된 경우 검색 패턴을 허용합니다. 이 특성이 SQL_TRUE 설정된 경우 검색 패턴을 허용하지 않는 식별자 인수입니다.  
  
 검색 패턴 문자는 다음과 같습니다.  
  
-   모든 단일 문자를 나타내는 밑줄(_)입니다.  
  
-   0자 이상의 시퀀스를 나타내는 백분율 기호(%)입니다.  
  
-   드라이버에 따라 지체, 백분율 표시 및 이스케이프 문자를 리터럴로 포함하는 데 사용되는 이스케이프 문자입니다. 이스케이프 문자가 특수하지 않은 문자 앞에 있는 경우 이스케이프 문자는 특별한 의미가 없습니다. 이스케이프 캐릭터가 특수 문자 앞에 오면 특수 문자를 탈출합니다. 예를 들어 "\a"는 ""와\\"a"라는 두 문자로\\처리되지만 "%"는 특수하지 않은 단일 문자 "%"로 처리됩니다.  
  
 이스케이프 문자는 **SQLGetInfo**에서 SQL_SEARCH_PATTERN_ESCAPE 옵션으로 검색됩니다. 검색 패턴을 리터럴로 포함하도록 허용하는 인수에서 밑줄, 백분율 기호 또는 이스케이프 문자 앞에 선행해야 합니다. 예제는 다음 표에 나와 있습니다.  
  
|검색 패턴|설명|  
|--------------------|-----------------|  
|%A%|문자 A를 포함하는 모든 식별자|  
|ABC_|ABC로 시작하는 네 개의 문자 식별자 모두|  
|ABC\\_|이스케이프 문자가 백슬래시() 라고\\가정하면 식별자가 ABC_.|  
|\\\\%|백슬래시()로\\시작하는 모든 식별자는 이스케이프 문자가 백슬래시라고 가정합니다.|  
  
 검색 패턴을 허용하는 인수에서 검색 패턴 문자를 이스케이프하려면 특별한 주의를 기울여야 합니다. 식별자에서 일반적으로 사용되는 밑줄 문자의 경우 특히 그렇습니다. 응용 프로그램의 일반적인 실수는 한 카탈로그 함수에서 값을 검색하고 해당 값을 다른 카탈로그 함수의 검색 패턴 인수에 전달하는 것입니다. 예를 들어 응용 프로그램이 **SQLTables에** 대한 결과 집합에서 테이블 이름을 MY_TABLE 검색하고 **이를 SQLColumns에** 전달하여 MY_TABLE 열 목록을 검색한다고 가정합니다. MY_TABLE 대한 열을 가져오는 대신 응용 프로그램은 MY_TABLE, MY1TABLE, MY2TABLE 등과 같은 검색 패턴 MY_TABLE 일치하는 모든 테이블에 대한 열을 가져옵니다.  
  
> [!NOTE]
>  ODBC 2. *x* 드라이버는 **SQLTables의** *CatalogName* 인수에서 검색 패턴을 지원하지 않습니다. ODBC 3 *.x* 드라이버는 SQL_ATTR_ ODBC_VERSION 환경 특성이 SQL_OV_ODBC3 설정된 경우 이 인수에서 검색 패턴을 허용합니다. 이 인수가 SQL_OV_ODBC2 설정된 경우 검색 패턴을 수락하지 않습니다.  
  
 null 포인터를 검색 패턴 인수에 전달해도 해당 인수에 대한 검색이 제한되지는 않습니다. 즉, null 포인터와 검색 패턴 %(모든 문자)은 동일합니다. 그러나 길이 가0(길이 0)에 대한 유효한 포인터인 0 길이 검색 패턴은 빈 문자열("")만 일치합니다.
