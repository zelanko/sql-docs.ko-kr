---
title: DBASE 드라이버에 대해 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300783"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>dBASE 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|대략적인 행 개수|테이블 크기 통계가 근사 인지 여부를 결정 합니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **STATISTICS** 키워드를 사용 합니다.|  
|데이터 정렬 순서|필드가 정렬 되는 순서입니다.<br /><br /> 이 시퀀스는 ASCII (기본값) 또는 국제 일 수 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **COLLATINGSEQUENCE** 키워드를 사용 합니다.|  
|데이터 원본 이름|급여 또는 직원과 같은 데이터 원본을 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **DSN** 키워드를 사용 합니다.|  
|데이터베이스|데이터베이스를 선택 하거나 만들지 않고도 Microsoft Access 데이터 원본을 설정할 수 있습니다. 설치 시 데이터베이스를 제공 하지 않으면 사용자가 데이터 원본에 연결할 때 데이터베이스 파일을 선택 하 라는 메시지가 표시 됩니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **dbq** 키워드를 사용 합니다.|  
|설명|데이터 원본에 있는 데이터에 대 한 선택적 설명입니다. 예: "채용 날짜, 급여 기록 및 모든 직원의 현재 검토"|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **DESCRIPTION** 키워드를 사용 합니다.|  
|단독|**배타** 확인란을 선택 하면 데이터베이스가 단독 모드로 열리고 한 번에 한 사용자만 액세스할 수 있습니다. 전용 모드에서 실행 하는 경우 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에 **EXCLUSIVE** 키워드를 사용 합니다.|  
|페이지 시간 제한|페이지 (사용 되지 않는 경우)가 제거 되기 전에 버퍼에 유지 되는 기간을 초 단위로 지정 합니다. 기본값은 600 1/10 초 (60 초)입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 고유 지연으로 인해 페이지 시간 제한이 0 일 수 없습니다. 페이지 시간 제한 값이 해당 값 아래에서 설정 된 경우에도 페이지 제한 시간은 내재 된 지연 보다 적을 수 없습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **PAGETIMEOUT** 키워드를 사용 합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **READONLY** 키워드를 사용 합니다.|  
|디렉터리 선택|액세스 하려는 파일이 포함 된 디렉터리를 선택할 수 있는 대화 상자를 표시 합니다.<br /><br /> 데이터 원본 디렉터리를 정의 하는 경우 가장 자주 사용 하는 파일이 있는 디렉터리를 지정 합니다. ODBC 드라이버는이 디렉터리를 기본 디렉터리로 사용 합니다. 자주 사용 되는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름을 사용 하 여 SELECT 문에서 파일 이름을 한정할 수 있습니다.<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 또는 SQL_CURRENT_QUALIFIER 옵션과 함께 **SQLSetConnectOption** 함수를 사용 하 여 새 기본 디렉터리를 지정할 수 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **DEFAULTDIR** 키워드를 사용 합니다.|  
|삭제 된 행 표시|삭제 된 것으로 표시 된 행을 검색 하거나 배치할 수 있는지 여부를 지정 합니다. 이 옵션의 선택을 취소 하면 삭제 된 행이 표시 되지 않습니다. 이를 선택 하면 삭제 된 행이 삭제 되지 않은 행과 동일 하 게 처리 됩니다. 기본값은 선택 취소되어 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)에 대 한 호출에서 **DELETED** 키워드를 사용 합니다.|
