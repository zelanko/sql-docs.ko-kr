---
title: 역설 드라이버에 대한 프로그래밍 방식으로 옵션 설정 | 마이크로 소프트 문서
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
ms.openlocfilehash: d04de1f0de4baca5b3f474ef9fbcf3f886e6906f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300763"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Paradox 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|디렉터리|대상 디렉터리를 설정합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **DEFAULTDIR** 키워드를 사용합니다.|  
|정렬 시퀀스|필드가 정렬되는 시퀀스입니다.<br /><br /> 시퀀스는 ASCII(기본값), 국제, 스웨덴어-핀란드어 또는 노르웨이어-덴마크어일 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **COLLATINGSEQUENCE** 키워드를 사용합니다.|  
|설명|데이터 소스내의 데이터에 대한 선택적 설명; 예를 들어 "고용 일자, 급여 이력 및 모든 직원의 현재 검토"를 예로 들 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **DESCRIPTION** 키워드를 사용합니다.|  
|단독|**배타적** 상자를 선택하면 데이터베이스가 단독 모드에서 열리며 한 번에 한 명의 사용자만 액세스할 수 있습니다. 배타적 모드에서 실행할 때 성능이 향상됩니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **EXCLUSIVE** 키워드를 사용합니다.|  
|네트 스타일|역설 데이터에 액세스할 때 사용할 네트워크 액세스 스타일: 역설 3에 대 한 "3.*x"* 중 하나. *x* 또는 "4. *x*" 역설 4. *x* 또는 5. *x*. "3으로 설정할 수 있습니다. *x*" 또는 "4. *x*" 버전이 역설 4인 경우. *x* 또는 5. *x;* 버전이 역설 3인 경우. *x,* 스타일은 "3이어야 합니다. *x*".|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **PARADOXNETSTYLE** 키워드를 사용합니다.|  
|페이지 시간 시간|페이지(사용하지 않은 경우)가 제거되기 전에 버퍼에 남아 있는 기간을 1초의 10분의 1로 지정합니다. 기본값은 초당 600분의 1초(60초)입니다. 이 옵션은 ODBC 드라이버를 사용하는 모든 데이터 원본에 적용됩니다.<br /><br /> 고유한 지연으로 인해 페이지 시간 시간이 0이 될 수 없습니다. 페이지 시간 초과 옵션이 해당 값 아래로 설정되어 있더라도 페이지 시간 초과가 내재지연보다 적을 수 없습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **PAGETIMEOUT** 키워드를 사용합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **READONLY** 키워드를 사용합니다.|  
|디렉터리 선택|액세스하려는 파일이 포함된 디렉터리를 선택할 수 있는 대화 상자를 표시합니다.<br /><br /> 데이터 원본 디렉터리를 정의할 때 가장 일반적으로 사용되는 파일이 있는 디렉터리를 지정합니다. ODBC 드라이버는 이 디렉터리를 기본 디렉터리로 사용합니다. 다른 파일을 자주 사용하는 경우 이 디렉토리에 복사합니다. 또는 SELECT 문에서 디렉터리 이름을 가진 파일 이름을 한정할 수 있습니다.<br /><br /> C에서 선택:\MYDIR\EMP \*<br /><br /> 또는 SQL_CURRENT_QUALIFIER 옵션과 함께 **SQLSetConnectOption** 함수를 사용하여 새 기본 디렉토리를 지정할 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **DEFAULTDIR** 키워드를 사용합니다.|  
|네트워크 디렉터리 선택|역설 잠금 데이터베이스를 포함하는 디렉토리의 전체 경로는 Pdoxusrs.net 파일(역설 4)을 포함하기 때문입니다.* x)* 또는 Paradox.net 파일(역설 5에서).* x)를*참조하십시오. 디렉터리에 이러한 파일 중 하나가 없는 경우 역설 드라이버가 만듭니다. 이러한 파일에 대한 자세한 내용은 역설 문서를 참조하십시오.<br /><br /> 네트워크 디렉터리를 선택하려면 먼저 **사용자 이름** 텍스트 상자에 역설 사용자 이름을 입력해야 합니다. **네트워크 디렉터리 선택을** 클릭하여 네트워크 디렉터리를 선택합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **PARADOXNETPATH** 키워드를 사용합니다.|  
|사용자 이름|역설 사용자 이름입니다. 이 이름은 잠금이 발생할 때 Paradox 파일의 다른 사용자에게 표시되는 이름입니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)에 대한 호출에서 **PARADOXUSERNAME** 키워드를 사용합니다.|
