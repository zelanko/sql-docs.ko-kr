---
title: Paradox 드라이버에 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd92344552371e2e052a958485340b70522cc121
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313565"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Paradox 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|Description|메서드|  
|------------|-----------------|------------|  
|디렉터리|대상된 디렉터리를 설정합니다.|이 옵션을 동적으로 설정 하려면 합니다 **DEFAULTDIR** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|정렬 순서|필드 정렬 되는 시퀀스입니다.<br /><br /> 시퀀스는 ASCII (기본값) 일 수 있습니다 국제, 스웨덴어-핀란드어, 노르웨이어 덴마크어 합니다.|이 옵션을 동적으로 설정 하려면 합니다 **COLLATINGSEQUENCE** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|Description|데이터 소스의 데이터에 대 한 설명 예를 들어, "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면 합니다 **설명** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|전용|경우는 **배타적** 확인란을 선택 하면 데이터베이스에서 단독 모드로 열립니다 및 한 번에 한 명의 사용자만 액세스할 수 있습니다. 전용 모드에서 실행할 때 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면를 **배타적** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|Net 스타일|Paradox 데이터에 액세스할 때 사용할 네트워크 액세스 스타일: 하거나 "3.*x*" Paradox 3. *x* 또는 "4. *x*"Paradox 4에 대 한. *x* 5 또는. *x*합니다. "3 설정할 수 있습니다. *x*"또는" 4. *x*"버전이 4. *x* 5 또는. *x*같으면 버전이 Paradox 3. *x*, 스타일 이어야 합니다 "3. *x*"입니다.|이 옵션을 동적으로 설정 하려면 합니다 **PARADOXNETSTYLE** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|페이지 시간 제한|1/10 초, 페이지 (사용 되지 않음) 하는 경우 제거 하기 전에 버퍼에 남아 있는 기간을 지정 합니다. 기본값은 600 초 (60 초)의 1/10 초입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 페이지 시간 초과 내재 된 지연으로 인해 0 일 수 없습니다. 페이지 시간 제한은 해당 값 보다 작은 페이지 제한 시간 옵션을 설정한 경우에 고유한 지연 보다 작을 수 없습니다.|이 옵션을 동적으로 설정 하려면 합니다 **PAGETIMEOUT** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면 합니다 **읽기 전용** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|디렉터리 선택|액세스 하려는 파일이 포함 된 디렉터리를 선택할 수 있는 대화 상자를 표시 합니다.<br /><br /> 데이터 소스 디렉터리를 정의 하는 가장 일반적으로 사용 되는 파일 디렉터리를 지정 하는 경우 배치 됩니다. ODBC 드라이버는 기본 디렉터리로이 디렉터리를 사용 합니다. 자주 사용 되는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름이 포함 된 SELECT 문에서 파일 이름을 한정할 수 있습니다.<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 또는 사용 하 여 새 기본 디렉터리를 지정할 수는 **SQLSetConnectOption** SQL_CURRENT_QUALIFIER 옵션을 사용 하 여 함수입니다.|이 옵션을 동적으로 설정 하려면 합니다 **DEFAULTDIR** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|네트워크 디렉터리를 선택 합니다.|Pdoxusrs.net 파일을 포함 하기 때문에 Paradox 잠금 데이터베이스를 포함 하는 디렉터리의 전체 경로 (Paradox 4에서. *x*) 또는 Paradox.net 파일 (Paradox 5에서. *x*). 디렉터리에 이러한 파일 중 하나가 없으면 Paradox 드라이버 하나 만듭니다. 이러한 파일에 대 한 내용은 Paradox 설명서를 참조 하십시오.<br /><br /> 네트워크 디렉터리를 선택 하기 전에 있는 Paradox 사용자 이름을 입력 해야 합니다는 **사용자 이름** 입력란입니다. 클릭 **네트워크 디렉터리 선택** 네트워크 디렉터리를 선택 합니다.|이 옵션을 동적으로 설정 하려면 합니다 **PARADOXNETPATH** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|사용자 이름|Paradox 사용자 이름입니다. 이것이 잠금이 발생 하는 경우 Paradox 파일의 다른 사용자에 게 표시 되는 이름입니다.|이 옵션을 동적으로 설정 하려면 합니다 **PARADOXUSERNAME** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|
