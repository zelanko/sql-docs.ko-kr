---
title: DBASE 드라이버에 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27f675cca5115a8336f2be4b7fa96c091aee1b62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063549"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>dBASE 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|대략적인 행 개수|테이블 크기 통계는 계산 하는지 여부를 결정 합니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.|이 옵션을 동적으로 설정 하려면 합니다 **통계** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|정렬 순서|필드 정렬 되는 시퀀스입니다.<br /><br /> 시퀀스 될 수 있습니다. ASCII (기본값) 또는 International입니다.|이 옵션을 동적으로 설정 하려면 합니다 **COLLATINGSEQUENCE** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|Data Source Name|직원 급여 등, 데이터 소스를 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면 합니다 **DSN** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|데이터베이스|Microsoft Access 데이터 소스를 선택 하거나 데이터베이스를 작성 하지 않고 설정할 수 있습니다. 설치 시 제공 된 데이터베이스가 없는 경우에 사용자에 게 데이터 원본에 연결할 때 데이터베이스 파일을 선택 하려면 메시지가 있습니다.|이 옵션을 동적으로 설정 하려면 합니다 **DBQ** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|설명|데이터 소스의 데이터에 대 한 설명 예를 들어, "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면 합니다 **설명** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|전용|경우는 **배타적** 확인란을 선택 하면 데이터베이스에서 단독 모드로 열립니다 및 한 번에 한 명의 사용자만 액세스할 수 있습니다. 단독 모드에서 실행 될 때 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면를 **배타적** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|페이지 시간 제한|1/10 초를 제거 하기 전에 (사용 되지 않음) 하는 경우 페이지를 버퍼에 남아 있는 기간을 지정 합니다. 기본값은 600 초 (60 초)의 1/10 초입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 페이지 시간 초과 내재 된 지연으로 인해 0 일 수 없습니다. 페이지 시간 제한은 해당 값 보다 작은 페이지 제한 시간 옵션을 설정한 경우에 고유한 지연 보다 작을 수 없습니다.|이 옵션을 동적으로 설정 하려면 합니다 **PAGETIMEOUT** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면 합니다 **읽기 전용** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|디렉터리 선택|액세스 하려는 파일을 포함 하는 디렉터리를 선택할 수 있는 대화 상자를 표시 합니다.<br /><br /> 데이터 원본 디렉터리를 정의할 때 가장 자주 사용 되는 파일이 있는 디렉터리를 지정 합니다. ODBC 드라이버는 기본 디렉터리로이 디렉터리를 사용 합니다. 자주 사용 되는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름이 포함 된 SELECT 문에서 파일 이름을 한정할 수 있습니다.<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 또는 사용 하 여 새 기본 디렉터리를 지정할 수는 **SQLSetConnectOption** SQL_CURRENT_QUALIFIER 옵션을 사용 하 여 함수입니다.|이 옵션을 동적으로 설정 하려면 합니다 **DEFAULTDIR** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|삭제 된 행 표시|삭제 된 것으로 표시 된 행 검색 되거나 배치할 수 있는지 여부를 지정 합니다. 선택을 취소 하는 경우에 삭제 된 행 표시 되지 않습니다. 삭제 된 행 처리할지 선택 하는 경우 삭제 되지 않은 행와 동일 합니다. 기본값은 선택 취소되어 있습니다.|이 옵션을 동적으로 설정 하려면 합니다 **DELETED** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|
