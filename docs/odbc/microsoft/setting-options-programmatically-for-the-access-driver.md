---
title: "프로그래밍 방식으로 액세스 드라이버에 대 한 옵션 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed08d24f96b66b69bbff409cbc2c9e203526041b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>프로그래밍 방식으로 액세스 드라이버에 대 한 옵션 설정
|옵션|Description|메서드|  
|------------|-----------------|------------|  
|버퍼 크기|내부 버퍼의 (킬로바이트), 디스크에서 데이터를 전송 하려면 Microsoft Access에서 사용 되는 크기입니다. 기본 버퍼 크기는 2048 KB (2048으로 표시 됨). 256로 나눌 정수 값을 입력할 수 있습니다.|이 옵션을 동적으로 설정 하려면 MAXBUFFERSIZE 키워드를 사용에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|Data Source Name|급여 또는 담당자와 같은 데이터 소스를 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면는 **DSN** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|데이터베이스|Microsoft Access 데이터 원본은 선택 하거나 데이터베이스를 만드는 하지 않고 설정할 수 있습니다. 데이터베이스가 없습니다. 설치 시 제공 하는 경우에 사용자 데이터 원본에 연결할 때 데이터베이스 파일을 선택할 수 나타납니다.|이 옵션을 동적으로 설정 하려면는 **DBQ** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|Description|데이터 소스에서 데이터에 대 한 설명 예를 들어 "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면는 **설명** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|단독|경우는 **단독** 확인란을 선택 하면 데이터베이스 단독 모드에서 열 수와 한 번에 한 명의 사용자만 액세스할 수 있습니다. 단독 모드에서 실행할 때 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면는 **단독** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|ImplicitCommitSync|데이터베이스에 트랜잭션 외부에서 변경한 내용을 쓰는 방법을 결정 합니다. 이 값은 처음 의미 Microsoft Access 드라이버 완료 하는 데 내부/암시적 트랜잭션 커밋을 대기 하는 "예"로 설정 됩니다.|이 옵션에 포함 되어는 **고급 옵션 설정** Microsoft Access 드라이버에 대 한 대화 상자.|  
|페이지 시간 초과|시간, 페이지 (사용 되지 않음) 하는 경우 제거 하기 전에 버퍼에 남아 있는 밀리초 단위로 지정 합니다. Microsoft Access 드라이버에 대 한 기본값은 500 밀리초 (0.5 초)입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 페이지 제한 시간에는 내재 된 지연 때문에 0 일 수 없습니다. 페이지 시간 초과 값 보다 페이지 제한 시간 옵션을 설정 하는 경우에 내재 된 지연 보다 작을 수 없습니다.|이 옵션을 동적으로 설정 하려면는 **PAGETIMEOUT** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면는 **READONLY** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|시스템 데이터베이스|액세스 하려는 Microsoft Access 데이터베이스에서 사용 되는 Microsoft Access 시스템 데이터베이스의 전체 경로입니다.<br /><br /> 클릭는 **시스템 데이터베이스** 단추를 사용할 수는 시스템 데이터베이스를 선택 합니다. ODBC Microsoft Access 드라이버 메시지 이름 및 암호에 대 한 사용자를 표시합니다. 기본 이름은 관리자 이며 Microsoft access Admin 사용자에 대 한 기본 암호는 빈 문자열입니다.<br /><br /> Microsoft Access 데이터베이스의 보안을 강화 하려면 관리자 사용자를 대체 하 고 관리자 사용자를 삭제 하려면 새 사용자를 만들거나 Admin 사용자 액세스 권한을 있는 개체를 변경 합니다.|이 옵션을 동적으로 설정 하려면는 **SYSTEMDB** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드 수를 지정 합니다. Microsoft Access 드라이버에 대 한이 값이 3, 기본적으로 사용 되지만 변경할 수 있습니다. 사용자는 많은 양의 활동을 데이터베이스에 없는 경우 스레드 수를 늘려야 할 수 있습니다.<br /><br /> 이 옵션에 포함 되어는 **고급 옵션 설정** Microsoft Access 드라이버에 대 한 대화 상자.|이 옵션을 동적으로 설정 하려면는 **스레드** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|UserCommitSync|Microsoft Access 드라이버는 명시적 사용자 정의 트랜잭션을 비동기적으로 수행 여부를 결정 합니다. 이 값은 처음 의미 Microsoft Access 드라이버 완료 하는 데 사용자 정의 트랜잭션 커밋을 대기 하는 "예"로 설정 됩니다.<br /><br /> 이 옵션을 False로 설정 하면 다중 사용자 환경에서 예기치 않은 결과가 발생할 있을 수 있습니다.|이 옵션을 동적으로 설정 하려면는 **USERCOMMITSYNC** 키워드에 대 한 호출에서 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|
