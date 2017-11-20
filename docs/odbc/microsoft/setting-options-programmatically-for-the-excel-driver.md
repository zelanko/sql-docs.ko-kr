---
title: "프로그래밍 방식으로 Excel 드라이버에 대 한 옵션 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da1f2ed6bbca3709c8223713f4841ed34288f5a3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>프로그래밍 방식으로 Excel 드라이버에 대 한 옵션 설정
|옵션|Description|메서드|  
|------------|-----------------|------------|  
|Data Source Name|급여 또는 담당자와 같은 데이터 소스를 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면는 **DSN** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|데이터베이스|Microsoft Access 데이터 원본은 선택 하거나 데이터베이스를 만드는 하지 않고 설정할 수 있습니다. 데이터베이스가 없습니다. 설치 시 제공 하는 경우에 사용자 데이터 원본에 연결할 때 데이터베이스 파일을 선택할 수 나타납니다.|이 옵션을 동적으로 설정 하려면는 **DBQ** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|Description|데이터 소스에서 데이터에 대 한 설명 예를 들어 "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면는 **설명** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|디렉터리|현재 선택 된 디렉터리를 표시합니다.<br /><br /> Microsoft Excel 3.0/4.0 파일에 대 한 경로 디스플레이 Microsoft Excel 5.0에 대해 "Directory"을 라는 7.0 또는 97 파일 경로 표시 "통합" 라고 합니다.|이 옵션을 동적으로 설정 하려면는 **DEFAULTDIR** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면는 **READONLY** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|검색할 행|각 열의 데이터 형식을 검색할 행 수입니다. 종류의 데이터를 찾을 수는 최대 수를 지정 된 데이터 형식이 결정 됩니다. 추측 된 열 데이터 형식과 일치 하지 않는 데이터가 있을 경우 데이터 형식이 NULL 값으로 반환 됩니다.<br /><br /> Microsoft Excel 드라이버에 대 한 검색할 행에 대 한 16 개가 하 1에서 숫자를 입력할 수 있습니다. 기본값은 8; 0으로 설정 하는 경우 모든 행이 검색 됩니다. (제한 벗어나는 숫자 오류가 반환 됩니다.)|이 옵션을 동적으로 설정 하려면는 **MAXSCANROWS** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|  
|디렉터리 선택|액세스 하려는 파일을 포함 하는 디렉터리를 선택할 수 있는 대화 상자가 표시 됩니다.<br /><br /> (Microsoft Access를 제외한 모든 드라이버)에 대 한 데이터 원본 디렉터리를 정의할 때 가장 일반적으로 사용된 파일이 있는 디렉터리를 지정 합니다. ODBC 드라이버 기본 디렉터리와이 디렉터리를 사용합니다. 자주 사용 하는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름이 포함 된 SELECT 문의 파일 이름을 한정할 수 있습니다.<br /><br /> 선택 \* C:\MYDIR\EMP에서<br /><br /> 또는 사용 하 여 새 기본 디렉터리를 지정할 수는 **SQLSetConnectOption** 함수 SQL_CURRENT_QUALIFIER 옵션입니다.<br /><br /> Microsoft Excel 3.0 또는 4.0 파일에 대 한 경로 표시 "Directory" 레이블이 및 경로 선택 단추에는 "디렉터리 선택" 레이블이 지정 됩니다. 5.0, 7.0, 또는 97 Microsoft Excel 파일에 대 한 경로 표시 "통합" 레이블이 및 경로 선택 단추에 "통합 문서 선택" 레이블이 지정 됩니다. 데이터 원본 디렉터리를 정의할 때 가장 흔히 사용 되는 Microsoft Excel 파일이 있는 Microsoft Excel 3.0/4.0, 디렉터리 또는 5.0, 7.0, 또는 97 Microsoft excel 통합 문서 파일이 있는 디렉터리를 지정 합니다. **현재 디렉터리를 사용 하 여** 5.0, 7.0 및 97 Microsoft Excel에 표시 되지 않습니다.|이 옵션을 동적으로 설정 하려면는 **DEFAULTDIR** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)합니다.|

