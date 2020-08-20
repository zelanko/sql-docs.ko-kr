---
description: Paradox 드라이버에 프로그래밍 방식으로 옵션 설정
title: Paradox 드라이버에 대해 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 85b63df9e18b835c96bc0e59f7c937ece69f3999
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471575"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Paradox 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|디렉터리|대상 디렉터리를 설정 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **DEFAULTDIR** 키워드를 사용 합니다.|  
|데이터 정렬 순서|필드가 정렬 되는 순서입니다.<br /><br /> 시퀀스는 ASCII (기본값), 국제, 스웨덴어-핀란드어 또는 노르웨이어-덴마크어 일 수 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **COLLATINGSEQUENCE** 키워드를 사용 합니다.|  
|설명|데이터 원본에 있는 데이터에 대 한 선택적 설명입니다. 예: "채용 날짜, 급여 기록 및 모든 직원의 현재 검토"|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **DESCRIPTION** 키워드를 사용 합니다.|  
|단독|**배타** 확인란을 선택 하면 데이터베이스가 단독 모드로 열리고 한 번에 한 사용자만 액세스할 수 있습니다. 배타적 모드로 실행 하면 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에 **EXCLUSIVE** 키워드를 사용 합니다.|  
|네트워크 스타일|Paradox 데이터에 액세스할 때 사용할 네트워크 액세스 스타일입니다. Paradox 3의 경우 "*3(sp3)"입니다.* *x* 또는 "4. *x*"의 경우 4입니다. *x* 또는 5입니다. *x*. "3"으로 설정할 수 있습니다. *x*"or" 4. *x*"버전은 Paradox 4입니다. *x* 또는 5입니다. *x*; 버전이 Paradox 3 인 경우 *x*의 스타일은 "3" 이어야 합니다. *x*".|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **PARADOXNETSTYLE** 키워드를 사용 합니다.|  
|페이지 시간 제한|페이지가 제거 되기 전에 버퍼에 유지 되는 시간 (초)을 지정 합니다. 기본값은 600 1/10 초 (60 초)입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 고유 지연으로 인해 페이지 시간 제한이 0 일 수 없습니다. 페이지 시간 제한 값이 해당 값 아래에서 설정 된 경우에도 페이지 제한 시간은 내재 된 지연 보다 적을 수 없습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **PAGETIMEOUT** 키워드를 사용 합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **READONLY** 키워드를 사용 합니다.|  
|디렉터리 선택|액세스 하려는 파일이 포함 된 디렉터리를 선택할 수 있는 대화 상자를 표시 합니다.<br /><br /> 데이터 원본 디렉터리를 정의할 때 가장 일반적으로 사용 되는 파일이 있는 디렉터리를 지정 합니다. ODBC 드라이버는이 디렉터리를 기본 디렉터리로 사용 합니다. 자주 사용 되는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름을 사용 하 여 SELECT 문에서 파일 이름을 한정할 수 있습니다.<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 또는 SQL_CURRENT_QUALIFIER 옵션과 함께 **SQLSetConnectOption** 함수를 사용 하 여 새 기본 디렉터리를 지정할 수 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **DEFAULTDIR** 키워드를 사용 합니다.|  
|네트워크 디렉터리 선택|Pdoxusrs.net 파일 (Paradox 4)이 포함 되어 있기 때문에 Paradox 잠금 데이터베이스를 포함 하는 디렉터리의 전체 경로입니다.* x*) 또는 Paradox.net 파일 (Paradox 5* ) x*). 디렉터리에 이러한 파일 중 하나가 포함 되어 있지 않으면 Paradox 드라이버가 하나를 만듭니다. 이러한 파일에 대 한 자세한 내용은 Paradox 설명서를 참조 하세요.<br /><br /> 네트워크 디렉터리를 선택 하기 전에 **사용자 이름** 텍스트 상자에 Paradox 사용자 이름을 입력 해야 합니다. 네트워크 디렉터리 **선택** 을 클릭 하 여 네트워크 디렉터리를 선택 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **PARADOXNETPATH** 키워드를 사용 합니다.|  
|사용자 이름|Paradox 사용자 이름입니다. 이 이름은 잠금이 발생 했을 때 Paradox 파일의 다른 사용자에 게 표시 되는 이름입니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대 한 호출에서 **PARADOXUSERNAME** 키워드를 사용 합니다.|
