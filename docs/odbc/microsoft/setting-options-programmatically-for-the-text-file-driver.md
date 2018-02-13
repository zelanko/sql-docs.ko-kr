---
title: "프로그래밍 방식으로 텍스트 파일 드라이버에 대 한 옵션 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1a7f971a0ac5d07c451b9a786bdcc563108e3f7
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>프로그래밍 방식으로 텍스트 파일 드라이버에 대 한 옵션 설정
|옵션|Description|메서드|  
|------------|-----------------|------------|  
|Data Source Name|급여 또는 담당자와 같은 데이터 소스를 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면는 **DSN** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|형식 정의|표시는 **텍스트 서식 정의** 대화 상자 및 데이터 원본 디렉터리에 개별 테이블에 대 한 스키마를 지정할 수 있습니다.|호출 하 여이 옵션을 동적으로 설정할 수 없습니다 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|Description|데이터 소스에서 데이터에 대 한 설명 예를 들어 "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면는 **설명** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|디렉터리|대상된 디렉터리를 선택합니다.|이 옵션을 동적으로 설정 하려면는 **DEFAULTDIR** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|확장명 목록|데이터 원본에 있는 텍스트 파일의 파일 이름 확장명을 나열합니다. 텍스트 드라이버를 사용 하면 확장명이 없는 파일 이름 확장명이 없는으로 CREATE TABLE 문이 실행 될 때 생성 됩니다. 다른 드라이버 확장명이 없는 제공 하는 경우 기본 확장명을 가진 파일을 만듭니다. 확장명이.txt 인 파일을 만들려면 이름에 확장명을 포함 해야 합니다. 확장명 없는 파일을 표시 하는 **텍스트 서식 정의** 대화 상자에서 "*." 확장명 목록에 추가 합니다.|이 옵션을 동적으로 설정 하려면는 **확장** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면는 **READONLY** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|검색할 행|각 열의 데이터 형식을 검색할 행 수입니다. 종류의 데이터를 찾을 수는 최대 수를 지정 된 데이터 형식이 결정 됩니다. 추측 된 열 데이터 형식과 일치 하지 않는 데이터가 있을 경우 데이터 형식이 NULL 값으로 반환 됩니다.<br /><br /> 텍스트 드라이버를 입력할 수 있습니다 숫자 1에서 32767 사이의; 검색할 행 수에 대 한 그러나 값은 기본적으로 항상 25입니다. (제한 벗어나는 숫자 오류가 반환 됩니다.)|이 옵션을 동적으로 설정 하려면는 **MAXSCANROWS** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|디렉터리 선택|액세스 하려는 파일을 포함 하는 디렉터리를 선택할 수 있는 대화 상자가 표시 됩니다.<br /><br /> 데이터 원본 디렉터리를 정의 하 파일에 가장 일반적으로 사용 하는 디렉터리를 지정 하는 경우 나와 있습니다. ODBC 드라이버 기본 디렉터리와이 디렉터리를 사용합니다. 자주 사용 하는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름이 포함 된 SELECT 문의 파일 이름을 한정할 수 있습니다. `SELECT * FROM C:\MYDIR\EMP`<br /><br /> 또는 사용 하 여 새 기본 디렉터리를 지정할 수는 **SQLSetConnectOption** 함수 SQL_CURRENT_QUALIFIER 옵션입니다.|이 옵션을 동적으로 설정 하려면는 **DEFAULTDIR** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|
