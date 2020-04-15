---
title: 텍스트 파일 드라이버에 대해 프로그래밍 방식으로 옵션 설정 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300753"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>텍스트 파일 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|데이터 원본 이름|급여 또는 인력과 같은 데이터 원본을 식별하는 이름입니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대한 호출에서 **DSN** 키워드를 사용합니다.|  
|형식 정의|텍스트 **형식** 정의 대화 상자상자를 표시하고 데이터 원본 디렉터리에서 개별 테이블에 대한 스키마를 지정할 수 있습니다.|이 옵션은 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대한 호출로 동적으로 설정할 수 없습니다.|  
|설명|데이터 소스내의 데이터에 대한 선택적 설명; 예를 들어 "고용 일자, 급여 이력 및 모든 직원의 현재 검토"를 예로 들 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대한 호출에서 **DESCRIPTION** 키워드를 사용합니다.|  
|디렉터리|대상 디렉터리를 선택합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대한 호출에서 **DEFAULTDIR** 키워드를 사용합니다.|  
|확장 목록|데이터 원본에 텍스트 파일의 파일 이름 확장명을 나열합니다. Text 드라이버를 사용하면 CREATE TABLE 문이 확장이 없는 이름으로 실행될 때 확장이 없는 파일이 만들어집니다. 다른 드라이버는 확장자가 제공되지 않는 경우 기본 확장자가 있는 파일을 만듭니다. .txt 확장명이 있는 파일을 만들려면 확장명이 이름에 포함되어야 합니다. **텍스트 형식 정의** 대화 상자에서 확장명이 없는 파일을 표시하려면 "*"입니다. 확장 목록에 추가되어야 합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대한 호출에서 **확장** 키워드를 사용합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대한 호출에서 **READONLY** 키워드를 사용합니다.|  
|스캔할 행|각 열의 데이터 형식을 결정하기 위해 스캔할 행 수입니다. 데이터 형식은 발견된 데이터의 최대 수에 따라 결정됩니다. 열에 대해 추측된 데이터 형식과 일치하지 않는 데이터가 발생하면 데이터 형식이 NULL 값으로 반환됩니다.<br /><br /> Text 드라이버의 경우 검색할 행 수에 대해 1에서 32767까지의 숫자를 입력할 수 있습니다. 그러나 값은 항상 25로 기본값입니다. (한계를 벗어난 숫자는 오류를 반환합니다.)|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대한 호출에서 **MAXSCANROWS** 키워드를 사용합니다.|  
|디렉터리 선택|액세스하려는 파일이 포함된 디렉터리를 선택할 수 있는 대화 상자를 표시합니다.<br /><br /> 데이터 원본 디렉터리를 정의할 때 가장 일반적으로 사용되는 파일이 있는 디렉터리를 지정합니다. ODBC 드라이버는 이 디렉터리를 기본 디렉터리로 사용합니다. 다른 파일을 자주 사용하는 경우 이 디렉토리에 복사합니다. 또는 SELECT 문에서 디렉터리 이름을 가진 파일 이름을 한정할 수 있습니다.`SELECT * FROM C:\MYDIR\EMP`<br /><br /> 또는 SQL_CURRENT_QUALIFIER 옵션과 함께 **SQLSetConnectOption** 함수를 사용하여 새 기본 디렉토리를 지정할 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)에 대한 호출에서 **DEFAULTDIR** 키워드를 사용합니다.|
