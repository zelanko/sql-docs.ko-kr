---
title: Excel 드라이버에 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47181fca07aff7b2a0d418b8852cfce47cf9e501
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063519"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Excel 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|Data Source Name|직원 급여 등, 데이터 소스를 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면 합니다 **DSN** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|데이터베이스|Microsoft Access 데이터 소스를 선택 하거나 데이터베이스를 작성 하지 않고 설정할 수 있습니다. 설치 시 제공 된 데이터베이스가 없는 경우 데이터 원본에 연결할 때 데이터베이스 파일을 선택 하려면 사용자 라는 메시지가 표시 됩니다.|이 옵션을 동적으로 설정 하려면 합니다 **DBQ** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|설명|데이터 소스의 데이터에 대 한 설명 예를 들어, "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면 합니다 **설명** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|디렉터리|현재 선택한 디렉터리가 표시 됩니다.<br /><br /> Microsoft Excel 3.0/4.0 파일에 대 한 경로 표시는 레이블이 지정 된 "Directory", Microsoft Excel 5.0에 대 한 7.0 또는 97 파일 경로 표시 "통합" 라고 합니다.|이 옵션을 동적으로 설정 하려면 합니다 **DEFAULTDIR** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면 합니다 **읽기 전용** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|검색할 행|각 열의 데이터 형식을 확인 하려면 검색할 행의 수입니다. 데이터 형식 최대 종류의 데이터를 찾을 수에 따라 결정 됩니다. 열에 대 한 추측 데이터 형식과 일치 하지 않는 데이터가 발견 되 면 데이터 형식이 NULL 값으로 반환 됩니다.<br /><br /> Microsoft Excel 드라이버의 경우 16 검색할 행에 대해 1에서 숫자를 입력할 수 있습니다. 기본값은 8입니다. 0으로 설정 하는 경우 모든 행 검사 됩니다. (제한 벗어나는 숫자로 오류가 반환 됩니다.)|이 옵션을 동적으로 설정 하려면 합니다 **MAXSCANROWS** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|디렉터리 선택|액세스 하려는 파일이 포함 된 디렉터리를 선택할 수 있는 대화 상자를 표시 합니다.<br /><br /> 데이터 원본 디렉터리 (예: Microsoft 액세스를 제외한 모든 드라이버)을 정의할 때 가장 자주 사용 되는 파일이 있는 디렉터리를 지정 합니다. ODBC 드라이버는 기본 디렉터리로이 디렉터리를 사용 합니다. 자주 사용 되는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름이 포함 된 SELECT 문에서 파일 이름을 한정할 수 있습니다.<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 또는 사용 하 여 새 기본 디렉터리를 지정할 수는 **SQLSetConnectOption** SQL_CURRENT_QUALIFIER 옵션을 사용 하 여 함수입니다.<br /><br /> Microsoft Excel 3.0 또는 4.0 파일에 대 한 경로 표시 "Directory" 레이블이 지정 되며 경로 선택 단추를 "디렉터리 선택" 이라고 합니다. 5\.0, 7.0, 또는 97 Microsoft Excel 파일에 대 한 경로 표시 "통합" 레이블이 지정 되며 경로 선택 단추에 "통합 문서 선택" 레이블이 지정 됩니다. 데이터 원본 디렉터리를 정의 하는 경우에 자주 사용 하는 Microsoft Excel 파일이 있는 Microsoft Excel 3.0/4.0에 대 한 디렉터리 또는 Microsoft Excel 97 5.0, 7.0에 대 한 통합 문서 파일이 있는 디렉터리를 지정 합니다. **현재 디렉터리를 사용 하 여** 5.0, 7.0 및 97 Microsoft Excel은 사용할 수 없습니다.|이 옵션을 동적으로 설정 하려면 합니다 **DEFAULTDIR** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|
