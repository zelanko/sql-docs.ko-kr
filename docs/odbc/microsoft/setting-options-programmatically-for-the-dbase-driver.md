---
title: "DBASE 드라이버에 대 한 프로그래밍 방식으로 옵션 설정 | Microsoft Docs"
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
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2760e0b08417121e765582904565461501eb0df6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>DBASE 드라이버에 대 한 프로그래밍 방식으로 옵션 설정
|옵션|Description|메서드|  
|------------|-----------------|------------|  
|대략적인 행 수|테이블 크기 통계 근사화 됩니다 있는지 여부를 결정 합니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.|이 옵션을 동적으로 설정 하려면는 **통계** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|데이터 정렬 순서|필드 정렬 되는 시퀀스입니다.<br /><br /> 시퀀스 수: ASCII (기본값) 또는 국제 합니다.|이 옵션을 동적으로 설정 하려면는 **COLLATINGSEQUENCE** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|Data Source Name|급여 또는 담당자와 같은 데이터 소스를 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면는 **DSN** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|데이터베이스|Microsoft Access 데이터 원본은 선택 하거나 데이터베이스를 만드는 하지 않고 설정할 수 있습니다. 데이터베이스가 없습니다. 설치 시 제공 하는 경우 사용자가 데이터 원본에 연결할 때 데이터베이스 파일을 선택 하려면 나타납니다.|이 옵션을 동적으로 설정 하려면는 **DBQ** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|Description|데이터 소스에서 데이터에 대 한 설명 예를 들어 "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면는 **설명** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|단독|경우는 **단독** 확인란을 선택 하면 데이터베이스 단독 모드에서 열 수와 한 번에 한 명의 사용자만 액세스할 수 있습니다. 단독 모드에서 실행 될 때 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면는 **단독** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|페이지 시간 초과|페이지 (사용 되지 않음) 하는 경우 제거 하기 전에 버퍼에 남아 있는 초의 1/10 초에는 시간 기간을 지정 합니다. 기본값은 600 초 (60 초)의 1/10 초입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 페이지 제한 시간에는 내재 된 지연 때문에 0 일 수 없습니다. 페이지 시간 초과 값 보다 페이지 제한 시간 옵션을 설정 하는 경우에 내재 된 지연 보다 작을 수 없습니다.|이 옵션을 동적으로 설정 하려면는 **PAGETIMEOUT** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면는 **READONLY** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|디렉터리 선택|액세스 하려는 파일이 있는 디렉터리를 선택할 수 있는 대화 상자가 표시 됩니다.<br /><br /> 데이터 원본 디렉터리를 정의할 때 가장 자주 사용 되는 파일이 있는 디렉터리를 지정 합니다. ODBC 드라이버 기본 디렉터리와이 디렉터리를 사용합니다. 자주 사용 하는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름이 포함 된 SELECT 문의 파일 이름을 한정할 수 있습니다.<br /><br /> 선택 \* C:\MYDIR\EMP에서<br /><br /> 또는 사용 하 여 새 기본 디렉터리를 지정할 수는 **SQLSetConnectOption** 함수 SQL_CURRENT_QUALIFIER 옵션입니다.|이 옵션을 동적으로 설정 하려면는 **DEFAULTDIR** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|  
|삭제 된 행 표시|삭제 된 것으로 표시 된 행을 검색 하거나에 배치 될 지 여부를 지정 합니다. 선택을 취소 하면 삭제 된 행 표시 되지 않습니다. 삭제 된 행을 선택 하는 경우 처리 됩니다 삭제 되지 않은 행과 동일 합니다. 기본값은 선택 취소되어 있습니다.|이 옵션을 동적으로 설정 하려면는 **DELETED** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)합니다.|

