---
title: dBASE 드라이버에 대해 프로그래밍 방식으로 옵션 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75889d9ff3ccfe01f9b8d5141df7774205522815
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300783"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>dBASE 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|대략적인 행 수|테이블 크기 통계의 근사치 여부를 결정합니다. 이 옵션은 ODBC 드라이버를 사용하는 모든 데이터 원본에 적용됩니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **통계** 키워드를 사용합니다.|  
|정렬 시퀀스|필드가 정렬되는 시퀀스입니다.<br /><br /> 시퀀스는 ASCII(기본값) 또는 국제순서일 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **COLLATINGSEQUENCE** 키워드를 사용합니다.|  
|데이터 원본 이름|급여 또는 인력과 같은 데이터 원본을 식별하는 이름입니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **DSN** 키워드를 사용합니다.|  
|데이터베이스|Microsoft Access 데이터 원본은 데이터베이스를 선택하거나 만들지 않고도 설정할 수 있습니다. 설정 시 데이터베이스가 제공되지 않으면 데이터 원본에 연결할 때 데이터베이스 파일을 선택하라는 메시지가 표시됩니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **DBQ** 키워드를 사용합니다.|  
|설명|데이터 소스내의 데이터에 대한 선택적 설명; 예를 들어 "고용 일자, 급여 이력 및 모든 직원의 현재 검토"를 예로 들 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **DESCRIPTION** 키워드를 사용합니다.|  
|단독|**배타적** 상자를 선택하면 데이터베이스가 단독 모드에서 열리며 한 번에 한 명의 사용자만 액세스할 수 있습니다. 배타적 모드에서 실행되면 성능이 향상됩니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **EXCLUSIVE** 키워드를 사용합니다.|  
|페이지 시간 시간|페이지가 제거되기 전에 버퍼에 남아 있는 페이지(사용하지 않은 경우)의 10분의 1로 기간을 지정합니다. 기본값은 초당 600분의 1초(60초)입니다. 이 옵션은 ODBC 드라이버를 사용하는 모든 데이터 원본에 적용됩니다.<br /><br /> 고유한 지연으로 인해 페이지 시간 시간이 0이 될 수 없습니다. 페이지 시간 초과 옵션이 해당 값 아래로 설정되어 있더라도 페이지 시간 초과가 내재지연보다 적을 수 없습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **PAGETIMEOUT** 키워드를 사용합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **READONLY** 키워드를 사용합니다.|  
|디렉터리 선택|액세스하려는 파일이 포함된 디렉터리를 선택할 수 있는 대화 상자를 표시합니다.<br /><br /> 데이터 원본 디렉터리를 정의할 때 가장 자주 사용되는 파일이 있는 디렉터리를 지정합니다. ODBC 드라이버는 이 디렉터리를 기본 디렉터리로 사용합니다. 다른 파일을 자주 사용하는 경우 이 디렉토리에 복사합니다. 또는 SELECT 문에서 디렉터리 이름을 가진 파일 이름을 한정할 수 있습니다.<br /><br /> C에서 선택:\MYDIR\EMP \*<br /><br /> 또는 SQL_CURRENT_QUALIFIER 옵션과 함께 **SQLSetConnectOption** 함수를 사용하여 새 기본 디렉토리를 지정할 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **DEFAULTDIR** 키워드를 사용합니다.|  
|삭제된 행 표시|삭제된 것으로 표시된 행을 검색하거나 배치할 수 있는지 여부를 지정합니다. 이 옵션을 선택취소하면 삭제된 행이 표시되지 않습니다. 이 옵션을 선택하면 삭제된 행이 삭제되지 않은 행과 동일하게 처리됩니다. 기본값은 선택 취소되어 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대한 호출에서 **DELETED** 키워드를 사용합니다.|
