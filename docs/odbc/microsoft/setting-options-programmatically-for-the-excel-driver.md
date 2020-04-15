---
title: Excel 드라이버에 대한 프로그래밍 방식으로 옵션 설정 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fcd5542e4beee1f7c7a30d5e0ee9f2815a3f0b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300773"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Excel 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|데이터 원본 이름|급여 또는 인력과 같은 데이터 원본을 식별하는 이름입니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대한 호출에서 **DSN** 키워드를 사용합니다.|  
|데이터베이스|Microsoft Access 데이터 원본은 데이터베이스를 선택하거나 만들지 않고도 설정할 수 있습니다. 설정 시 데이터베이스가 제공되지 않으면 데이터 원본에 연결할 때 데이터베이스 파일을 선택하라는 메시지가 표시됩니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대한 호출에서 **DBQ** 키워드를 사용합니다.|  
|설명|데이터 소스내의 데이터에 대한 선택적 설명; 예를 들어 "고용 일자, 급여 이력 및 모든 직원의 현재 검토"를 예로 들 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대한 호출에서 **DESCRIPTION** 키워드를 사용합니다.|  
|디렉터리|현재 선택한 디렉터리를 표시합니다.<br /><br /> Microsoft Excel 3.0/4.0 파일의 경우 경로 표시에 "디렉터리"라는 레이블이 지정되고 Microsoft Excel 5.0, 7.0 또는 97 파일의 경우 경로 표시에 "통합 문서"라는 레이블이 지정됩니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대한 호출에서 **DEFAULTDIR** 키워드를 사용합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대한 호출에서 **READONLY** 키워드를 사용합니다.|  
|스캔할 행|각 열의 데이터 형식을 결정하기 위해 스캔할 행 수입니다. 데이터 형식은 발견된 데이터의 최대 수에 따라 결정됩니다. 열에 대해 추측된 데이터 형식과 일치하지 않는 데이터가 발생하면 데이터 형식이 NULL 값으로 반환됩니다.<br /><br /> Microsoft Excel 드라이버의 경우 행을 스캔할 수 있도록 1에서 16까지의 숫자를 입력할 수 있습니다. 값은 기본값은 8입니다. 0으로 설정하면 모든 행이 검색됩니다. (한계를 벗어난 숫자는 오류를 반환합니다.)|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대한 호출에서 **MAXSCANROWS** 키워드를 사용합니다.|  
|디렉터리 선택|액세스하려는 파일이 포함된 디렉터리를 선택할 수 있는 대화 상자를 표시합니다.<br /><br /> Microsoft Access를 제외한 모든 드라이버에 대해 데이터 원본 디렉터리를 정의할 때 가장 일반적으로 사용되는 파일이 있는 디렉터리를 지정합니다. ODBC 드라이버는 이 디렉터리를 기본 디렉터리로 사용합니다. 다른 파일을 자주 사용하는 경우 이 디렉토리에 복사합니다. 또는 SELECT 문에서 디렉터리 이름을 가진 파일 이름을 한정할 수 있습니다.<br /><br /> C에서 선택:\MYDIR\EMP \*<br /><br /> 또는 SQL_CURRENT_QUALIFIER 옵션과 함께 **SQLSetConnectOption** 함수를 사용하여 새 기본 디렉토리를 지정할 수 있습니다.<br /><br /> Microsoft Excel 3.0 또는 4.0 파일의 경우 경로 표시에 "디렉터리"라는 레이블이 지정되고 경로 선택 단추에는 "디렉터리 선택"이라는 레이블이 지정됩니다. Microsoft Excel 5.0, 7.0 또는 97 파일의 경우 경로 표시에 "통합 문서"라는 레이블이 지정되고 경로 선택 단추에는 "통합 문서 선택"이라는 레이블이 지정됩니다. 데이터 원본 디렉터리를 정의할 때 가장 일반적으로 사용되는 Microsoft Excel 파일이 Microsoft Excel 3.0/4.0에 있는 디렉터리 또는 통합 문서 파일이 Microsoft Excel 5.0, 7.0 또는 97용디렉터에 있는 디렉터리를 지정합니다. 현재 **디렉토리 사용** 은 Microsoft Excel 5.0, 7.0 및 97에서 사용할 수 없습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)에 대한 호출에서 **DEFAULTDIR** 키워드를 사용합니다.|
