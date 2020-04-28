---
title: 텍스트 파일 드라이버에 대해 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e19c3b49479047bc92a7b6f72359d4951d8df16e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300753"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>텍스트 파일 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|데이터 원본 이름|급여 또는 직원과 같은 데이터 원본을 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대 한 호출에서 **DSN** 키워드를 사용 합니다.|  
|형식 정의|**텍스트 형식 정의** 대화 상자를 표시 하 고 데이터 원본 디렉터리의 개별 테이블에 대 한 스키마를 지정할 수 있습니다.|이 옵션은 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)를 호출 하 여 동적으로 설정할 수 없습니다.|  
|설명|데이터 원본에 있는 데이터에 대 한 선택적 설명입니다. 예: "채용 날짜, 급여 기록 및 모든 직원의 현재 검토"|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대 한 호출에서 **DESCRIPTION** 키워드를 사용 합니다.|  
|디렉터리|대상 디렉터리를 선택 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대 한 호출에서 **DEFAULTDIR** 키워드를 사용 합니다.|  
|확장 프로그램 목록|데이터 원본에 있는 텍스트 파일의 파일 이름 확장명을 나열 합니다. 텍스트 드라이버를 사용 하는 경우 확장명이 없는 이름을 사용 하 여 CREATE TABLE 문을 실행할 때 확장명이 없는 파일이 생성 됩니다. 다른 드라이버는 확장명이 제공 되지 않은 경우 기본 확장명으로 파일을 만듭니다. 확장명이 .txt 인 파일을 만들려면 확장명을 이름에 포함 해야 합니다. **텍스트 형식 정의** 대화 상자에서 확장명이 없는 파일을 표시 하려면 "*"를 사용 합니다. 확장명 목록에 추가 해야 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대 한 호출에서 **EXTENSIONS** 키워드를 사용 합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대 한 호출에서 **READONLY** 키워드를 사용 합니다.|  
|검색할 행|각 열의 데이터 형식을 결정 하기 위해 검색할 행 수입니다. 데이터 형식은 검색 된 데이터의 최대 종류 수에 따라 결정 됩니다. 열에 대해 추측 된 데이터 형식과 일치 하지 않는 데이터가 발견 되 면 데이터 형식이 NULL 값으로 반환 됩니다.<br /><br /> 텍스트 드라이버의 경우 검색할 행 수에 대해 1에서 32767 사이의 숫자를 입력할 수 있습니다. 그러나이 값은 항상 기본값 25입니다. 제한 밖의 숫자는 오류를 반환 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대 한 호출에서 **MAXSCANROWS** 키워드를 사용 합니다.|  
|디렉터리 선택|액세스 하려는 파일이 포함 된 디렉터리를 선택할 수 있는 대화 상자를 표시 합니다.<br /><br /> 데이터 원본 디렉터리를 정의할 때 가장 일반적으로 사용 되는 파일이 있는 디렉터리를 지정 합니다. ODBC 드라이버는이 디렉터리를 기본 디렉터리로 사용 합니다. 자주 사용 되는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름을 사용 하 여 SELECT 문에서 파일 이름을 한정할 수 있습니다.`SELECT * FROM C:\MYDIR\EMP`<br /><br /> 또는 SQL_CURRENT_QUALIFIER 옵션과 함께 **SQLSetConnectOption** 함수를 사용 하 여 새 기본 디렉터리를 지정할 수 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대 한 호출에서 **DEFAULTDIR** 키워드를 사용 합니다.|
