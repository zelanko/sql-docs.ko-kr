---
title: "프로그래밍 방식으로 Paradox 드라이버에 대 한 옵션 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c353ec7cca4744a4189891a4123eaf6263b8fd51
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>프로그래밍 방식으로 Paradox 드라이버에 대 한 옵션 설정
|옵션|Description|메서드|  
|------------|-----------------|------------|  
|디렉터리|대상된 디렉터리를 설정합니다.|이 옵션을 동적으로 설정 하려면는 **DEFAULTDIR** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|데이터 정렬 순서|필드 정렬 되는 시퀀스입니다.<br /><br /> 시퀀스는 ASCII (기본값) 일 수 있습니다, 국제, 스웨덴어 핀란드어 또는 노르웨이어 덴마크어 합니다.|이 옵션을 동적으로 설정 하려면는 **COLLATINGSEQUENCE** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|Description|데이터 소스에서 데이터에 대 한 설명 예를 들어 "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면는 **설명** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|단독|경우는 **단독** 확인란을 선택 하면 데이터베이스 단독 모드에서 열 수와 한 번에 한 명의 사용자만 액세스할 수 있습니다. 단독 모드에서 실행할 때 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면는 **단독** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|Net 스타일|네트워크 액세스 스타일 Paradox 데이터에 액세스할 때 사용할: 어느 "3.*x*" Paradox 3에 대 한.* x* 또는 "4.* x*"4에 대 한.* x* 개나 5.* x*합니다. "3로 설정할 수 있습니다. *x*"또는" 4.* x*"버전이 4.* x* 개나 5.* x*버전이 Paradox 3;.* x*, 스타일 이어야 합니다 "3.* x*"입니다.|이 옵션을 동적으로 설정 하려면는 **PARADOXNETSTYLE** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|페이지 시간 초과|페이지 (사용 되지 않음) 하는 경우 제거 하기 전에 버퍼에 남아 있는 초의 1/10 초에는 시간 기간을 지정 합니다. 기본값은 600 초 (60 초)의 1/10 초입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 페이지 제한 시간에는 내재 된 지연 때문에 0 일 수 없습니다. 페이지 시간 초과 값 보다 페이지 제한 시간 옵션을 설정 하는 경우에 내재 된 지연 보다 작을 수 없습니다.|이 옵션을 동적으로 설정 하려면는 **PAGETIMEOUT** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면는 **READONLY** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|디렉터리 선택|액세스 하려는 파일을 포함 하는 디렉터리를 선택할 수 있는 대화 상자가 표시 됩니다.<br /><br /> 데이터 원본 디렉터리를 정의 하 파일에 가장 일반적으로 사용 하는 디렉터리를 지정 하는 경우 나와 있습니다. ODBC 드라이버 기본 디렉터리와이 디렉터리를 사용합니다. 자주 사용 하는 경우 다른 파일을이 디렉터리에 복사 합니다. 또는 디렉터리 이름이 포함 된 SELECT 문의 파일 이름을 한정할 수 있습니다.<br /><br /> 선택 \* C:\MYDIR\EMP에서<br /><br /> 또는 사용 하 여 새 기본 디렉터리를 지정할 수는 **SQLSetConnectOption** 함수 SQL_CURRENT_QUALIFIER 옵션입니다.|이 옵션을 동적으로 설정 하려면는 **DEFAULTDIR** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|네트워크 디렉터리를 선택 합니다.|Pdoxusrs.net 파일을 포함 하기 때문에 Paradox 잠금 데이터베이스를 포함 하는 디렉터리의 전체 경로 (Paradox 4에서.* x*) 또는 Paradox.net 파일 (Paradox 5에서.* x*). 디렉터리에 이러한 파일 중 하나가 포함 되어 있지 않으면, Paradox 드라이버에서 만들어집니다. 이러한 파일에 대 한 내용은 Paradox 설명서를 참조 합니다.<br /><br /> 네트워크 디렉터리를 선택 하려면 먼저 있는 Paradox 사용자 이름을 입력 해야는 **사용자 이름** 입력란. 클릭 **네트워크 디렉터리 선택** 네트워크 디렉터리를 선택 합니다.|이 옵션을 동적으로 설정 하려면는 **PARADOXNETPATH** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|  
|사용자 이름|Paradox 사용자 이름입니다. 잠금이 때 Paradox 파일의 다른 사용자에 게 표시 이름입니다.|이 옵션을 동적으로 설정 하려면는 **PARADOXUSERNAME** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)합니다.|

