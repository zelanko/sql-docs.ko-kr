---
title: Excel 드라이버에 대해 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063519"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Excel 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|Description|방법|  
|------------|-----------------|------------|  
|데이터 원본 이름|급여 또는 직원과 같은 데이터 원본을 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대 한 호출에서 **DSN** 키워드를 사용 합니다.|  
|데이터베이스|데이터베이스를 선택 하거나 만들지 않고도 Microsoft Access 데이터 원본을 설정할 수 있습니다. 설치 시 데이터베이스를 제공 하지 않으면 데이터 원본에 연결할 때 데이터베이스 파일을 선택 하 라는 메시지가 표시 됩니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대 한 호출에서 **dbq** 키워드를 사용 합니다.|  
|Description|데이터 원본에 있는 데이터에 대 한 선택적 설명입니다. 예: "채용 날짜, 급여 기록 및 모든 직원의 현재 검토"|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대 한 호출에서 **DESCRIPTION** 키워드를 사용 합니다.|  
|디렉터리|현재 선택한 디렉터리를 표시 합니다.<br /><br /> Microsoft Excel 3.0/4.0 파일의 경우 경로 표시는 "Directory"로 표시 되 고 Microsoft Excel 5.0, 7.0 또는 97 파일의 경우 경로 표시에 "통합 문서" 라는 레이블이 지정 됩니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대 한 호출에서 **DEFAULTDIR** 키워드를 사용 합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대 한 호출에서 **READONLY** 키워드를 사용 합니다.|  
|검색할 행|각 열의 데이터 형식을 결정 하기 위해 검색할 행 수입니다. 데이터 형식은 검색 된 데이터의 최대 종류 수에 따라 결정 됩니다. 열에 대해 추측 된 데이터 형식과 일치 하지 않는 데이터가 발견 되 면 데이터 형식이 NULL 값으로 반환 됩니다.<br /><br /> Microsoft Excel 드라이버의 경우 검색할 행에 대해 1에서 16 사이의 숫자를 입력할 수 있습니다. 값의 기본값은 8입니다. 0으로 설정 하면 모든 행이 검색 됩니다. 제한 밖의 숫자는 오류를 반환 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대 한 호출에서 **MAXSCANROWS** 키워드를 사용 합니다.|  
|디렉터리 선택|액세스 하려는 파일이 포함 된 디렉터리를 선택할 수 있는 대화 상자를 표시 합니다.<br /><br /> Microsoft Access를 제외한 모든 드라이버에 대 한 데이터 원본 디렉터리를 정의할 때 가장 일반적으로 사용 되는 파일이 있는 디렉터리를 지정 합니다. ODBC 드라이버는이 디렉터리를 기본 디렉터리로 사용 합니다. 자주 사용 되는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름을 사용 하 여 SELECT 문에서 파일 이름을 한정할 수 있습니다.<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 또는 SQL_CURRENT_QUALIFIER 옵션과 함께 **SQLSetConnectOption** 함수를 사용 하 여 새 기본 디렉터리를 지정할 수 있습니다.<br /><br /> Microsoft Excel 3.0 또는 4.0 파일의 경우 경로 표시는 "Directory"로 표시 되 고 경로 선택 단추는 "디렉터리 선택" 이라는 레이블이 지정 됩니다. Microsoft Excel 5.0, 7.0 또는 97 파일의 경우 경로 표시는 "통합 문서"로 표시 되 고 경로 선택 단추는 "통합 문서 선택" 이라는 레이블이 지정 됩니다. 데이터 원본 디렉터리를 정의할 때 microsoft excel 3.0/4.0에 가장 일반적으로 사용 되는 Microsoft Excel 파일이 있는 디렉터리 또는 Microsoft Excel 5.0, 7.0 또는 97에 대 한 통합 문서 파일이 있는 디렉터리를 지정 합니다. Microsoft Excel 5.0, 7.0 및 97에 대 한 **현재 디렉터리 사용** 이 사용 하지 않도록 설정 되어 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대 한 호출에서 **DEFAULTDIR** 키워드를 사용 합니다.|
