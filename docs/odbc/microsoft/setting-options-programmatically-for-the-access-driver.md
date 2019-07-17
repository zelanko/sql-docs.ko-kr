---
title: Access 드라이버에 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 688716e9b7ba89500a4d2e8a579da42972e43d0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063551"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Access 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|버퍼 크기|내부 버퍼의 (킬로바이트)에서 디스크에서 데이터를 전송 하려면 Microsoft Access에서 사용 되는 크기입니다. 기본 버퍼 크기는 2048KB (2048로 표시 됨). 256 나눌 정수 값을 입력할 수 있습니다.|이 옵션을 동적으로 설정 하려면 호출에서 MAXBUFFERSIZE 키워드를 사용 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|Data Source Name|직원 급여 등, 데이터 소스를 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면 합니다 **DSN** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|데이터베이스|Microsoft Access 데이터 소스를 선택 하거나 데이터베이스를 작성 하지 않고 설정할 수 있습니다. 설치 시 제공 된 데이터베이스가 없는 경우 데이터 원본에 연결할 때 데이터베이스 파일을 선택 하려면 사용자 라는 메시지가 표시 됩니다.|이 옵션을 동적으로 설정 하려면 합니다 **DBQ** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|설명|데이터 소스의 데이터에 대 한 설명 예를 들어, "고용 날짜, 급여 내역, 및 모든 직원의 현재 검토 합니다."|이 옵션을 동적으로 설정 하려면 합니다 **설명** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|전용|경우는 **배타적** 확인란을 선택 하면 데이터베이스에서 단독 모드로 열립니다 및 한 번에 한 명의 사용자만 액세스할 수 있습니다. 전용 모드에서 실행할 때 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면를 **배타적** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|ImplicitCommitSync|트랜잭션 외부에서 변경 내용을 데이터베이스에 작성 되는 방법 결정 합니다. 이 값은 처음에 Microsoft Access 드라이버를 완료할 수 있도록 내부/암시적 트랜잭션 커밋을 대기 함을 의미는 "예"로 설정 됩니다.|이 옵션에 포함 되어는 **고급 옵션 설정** Microsoft Access 드라이버에 대 한 대화 상자.|  
|페이지 시간 제한|(밀리초) (사용 되지 않음) 하는 경우 페이지를 제거 하기 전에 버퍼에 남아 있는 기간을 지정 합니다. Microsoft Access 드라이버의 경우 기본값은 500 밀리초 (0.5 초)입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 페이지 시간 초과 내재 된 지연으로 인해 0 일 수 없습니다. 페이지 시간 제한은 해당 값 보다 작은 페이지 제한 시간 옵션을 설정한 경우에 고유한 지연 보다 작을 수 없습니다.|이 옵션을 동적으로 설정 하려면 합니다 **PAGETIMEOUT** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|읽기 전용|읽기 전용으로 데이터베이스를 지정합니다.|이 옵션을 동적으로 설정 하려면 합니다 **읽기 전용** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|시스템 데이터베이스|액세스 하려는 Microsoft Access 데이터베이스와 함께 사용할 Microsoft Access 시스템 데이터베이스의 전체 경로입니다.<br /><br /> 클릭 합니다 **시스템 데이터베이스** 단추를 사용할 수는 시스템 데이터베이스를 선택 합니다. ODBC Microsoft Access 드라이버 라는 이름 및 암호입니다. 기본 이름은 관리자 및 관리 사용자의 Microsoft Access에서 기본 암호는 빈 문자열입니다.<br /><br /> Microsoft Access 데이터베이스의 보안을 강화 하려면 관리 사용자를 바꾸고 관리 사용자를 삭제 하는 새 사용자 만들기 또는 관리 사용자가 액세스할 수 있는 개체를 변경 합니다.|이 옵션을 동적으로 설정 하려면 합니다 **아닌 SYSTEMDB** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드의 수입니다. Microsoft Access 드라이버의 경우이 값을 3으로 기본적으로 사용 되지만 변경할 수 있습니다. 사용자는 데이터베이스의 작업량이 많은 있으면 스레드 수를 늘릴 수도 있습니다.<br /><br /> 이 옵션에 포함 되어는 **고급 옵션 설정** Microsoft Access 드라이버에 대 한 대화 상자.|이 옵션을 동적으로 설정 하려면 합니다 **스레드** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|  
|UserCommitSync|Microsoft Access 드라이버는 명시적 사용자 정의 트랜잭션을 비동기적으로 수행 하는지 여부를 결정 합니다. 이 값은 처음에 Microsoft Access 드라이버를 완료 하는 사용자 정의 트랜잭션 커밋을 대기 함을 의미는 "예"로 설정 됩니다.<br /><br /> 이 옵션을 False로 설정 다중 사용자 환경에서 예기치 않은 결과가 있을 수 있습니다.|이 옵션을 동적으로 설정 하려면 합니다 **USERCOMMITSYNC** 호출에서 키워드 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)합니다.|
