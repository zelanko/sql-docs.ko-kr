---
title: 텍스트 파일 드라이버에 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04bd9a37d87c91fe3f42cbb1fdf464660ba5a299
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044420"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>텍스트 파일 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|Description|메서드|  
|------------|-----------------|------------|  
|Data Source Name|직원 급여 등, 데이터 소스를 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면 합니다 **DSN** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|형식 정의|표시 된 **텍스트 형식으로 정의** 대화 상자 및 데이터 소스 디렉터리에서 개별 테이블에 대 한 스키마를 지정할 수 있습니다.|호출 하 여이 옵션을 동적으로 설정할 수 없습니다 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|Description|데이터 소스의 데이터에 대 한 설명 예를 들어, "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면 합니다 **설명** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|디렉터리|대상된 디렉터리를 선택합니다.|이 옵션을 동적으로 설정 하려면 합니다 **DEFAULTDIR** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|확장 목록|데이터 원본에 있는 텍스트 파일의 파일 이름 확장명을 나열합니다. 텍스트 드라이버를 사용 하면 확장명이 없는 파일 확장명이 없는 이름으로는 CREATE TABLE 문이 실행 될 때 생성 됩니다. 다른 드라이버 없는 확장을 제공 하는 경우 기본 확장명을 가진 파일을 만듭니다. 확장명이.txt 인 파일을 만들려면 확장 이름에 포함 되어야 합니다. 확장명 없는 파일을 표시 하는 **텍스트 형식으로 정의** 대화 상자에서 "*." 확장 목록에 추가 되어야 합니다.|이 옵션을 동적으로 설정 하려면 합니다 **확장** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면 합니다 **읽기 전용** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|검색할 행|각 열의 데이터 형식을 확인 하려면 검색할 행의 수입니다. 데이터 형식 최대 종류의 데이터를 찾을 수에 따라 결정 됩니다. 열에 대 한 추측 데이터 형식과 일치 하지 않는 데이터가 발견 되 면 데이터 형식이 NULL 값으로 반환 됩니다.<br /><br /> 텍스트 드라이버의 경우 입력할 수 있습니다. 있습니다 숫자 1에서 32767 사이의; 검색할 행의 수 그러나 값은 기본적으로 항상 25입니다. (제한 벗어나는 숫자로 오류가 반환 됩니다.)|이 옵션을 동적으로 설정 하려면 합니다 **MAXSCANROWS** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|  
|디렉터리 선택|액세스 하려는 파일이 포함 된 디렉터리를 선택할 수 있는 대화 상자를 표시 합니다.<br /><br /> 데이터 소스 디렉터리를 정의 하는 가장 일반적으로 사용 되는 파일 디렉터리를 지정 하는 경우 배치 됩니다. ODBC 드라이버는 기본 디렉터리로이 디렉터리를 사용 합니다. 자주 사용 되는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름이 포함 된 SELECT 문에서 파일 이름을 한정할 수 있습니다. `SELECT * FROM C:\MYDIR\EMP`<br /><br /> 또는 사용 하 여 새 기본 디렉터리를 지정할 수는 **SQLSetConnectOption** SQL_CURRENT_QUALIFIER 옵션을 사용 하 여 함수입니다.|이 옵션을 동적으로 설정 하려면 합니다 **DEFAULTDIR** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)합니다.|
