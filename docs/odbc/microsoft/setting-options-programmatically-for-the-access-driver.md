---
description: Access 드라이버에 프로그래밍 방식으로 옵션 설정
title: 액세스 드라이버에 대 한 프로그래밍 방식으로 옵션 설정 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ae798b3c3d91917e461bb6b5a58cb06734870d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412419"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Access 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|버퍼 크기|Microsoft Access에서 디스크와 데이터를 전송 하는 데 사용 하는 내부 버퍼의 크기 (kb)입니다. 기본 버퍼 크기는 2048 KB (2048으로 표시)입니다. 256으로 나눌 수 있는 정수 값을 입력할 수 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 MAXBUFFERSIZE 키워드를 사용 합니다.|  
|데이터 원본 이름|급여 또는 직원과 같은 데이터 원본을 식별 하는 이름입니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 **DSN** 키워드를 사용 합니다.|  
|데이터베이스|데이터베이스를 선택 하거나 만들지 않고도 Microsoft Access 데이터 원본을 설정할 수 있습니다. 설치 시 데이터베이스를 제공 하지 않으면 데이터 원본에 연결할 때 데이터베이스 파일을 선택 하 라는 메시지가 표시 됩니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 **dbq** 키워드를 사용 합니다.|  
|설명|데이터 원본에 있는 데이터에 대 한 선택적 설명입니다. 예: "채용 날짜, 급여 기록 및 모든 직원의 현재 검토"|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 **DESCRIPTION** 키워드를 사용 합니다.|  
|단독|**배타** 확인란을 선택 하면 데이터베이스가 단독 모드로 열리고 한 번에 한 사용자만 액세스할 수 있습니다. 배타적 모드로 실행 하면 성능이 향상 됩니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에 **EXCLUSIVE** 키워드를 사용 합니다.|  
|ImplicitCommitSync|트랜잭션 외부에서 수행 된 변경 내용이 데이터베이스에 기록 되는 방법을 결정 합니다. 처음에는이 값이 "예"로 설정 되어 있습니다. 즉, Microsoft Access 드라이버에서 내부/암시적 트랜잭션의 커밋이 완료 될 때까지 대기 합니다.|이 옵션은 Microsoft Access driver에 대 한 **고급 옵션 설정** 대화 상자에 포함 되어 있습니다.|  
|페이지 시간 제한|페이지가 제거 되기 전에 버퍼에 유지 되는 시간 (밀리초)을 지정 합니다. Microsoft Access driver의 경우 기본값은 500 밀리초 (0.5 초)입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 고유 지연으로 인해 페이지 시간 제한이 0 일 수 없습니다. 페이지 시간 제한 값이 해당 값 아래에서 설정 된 경우에도 페이지 제한 시간은 내재 된 지연 보다 적을 수 없습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 **PAGETIMEOUT** 키워드를 사용 합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 **READONLY** 키워드를 사용 합니다.|  
|시스템 데이터베이스|액세스 하려는 Microsoft Access 데이터베이스에 사용할 Microsoft Access system 데이터베이스의 전체 경로입니다.<br /><br /> **시스템 데이터베이스** 단추를 클릭 하 여 사용할 시스템 데이터베이스를 선택 합니다. ODBC Microsoft Access 드라이버에서 사용자에 게 이름과 암호를 입력 하 라는 메시지를 표시 합니다. 기본 이름은 Admin이 고 Microsoft Access의 관리자 사용자에 대 한 기본 암호는 빈 문자열입니다.<br /><br /> Microsoft Access 데이터베이스의 보안을 강화 하려면 새 사용자를 만들어 관리 사용자를 바꾸고 관리 사용자를 삭제 하거나 관리자가 액세스할 수 있는 개체를 변경 합니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 **systemdb** 키워드를 사용 합니다.|  
|스레드|엔진에서 사용할 백그라운드 스레드 수입니다. Microsoft Access driver의 경우이 값의 기본값은 3 이지만 변경할 수 있습니다. 사용자는 데이터베이스에 작업이 많은 경우 스레드 수를 늘려야 할 수 있습니다.<br /><br /> 이 옵션은 Microsoft Access driver에 대 한 **고급 옵션 설정** 대화 상자에 포함 되어 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 **THREADS** 키워드를 사용 합니다.|  
|UserCommitSync|Microsoft Access driver가 명시적 사용자 정의 트랜잭션을 비동기적으로 수행할지 여부를 결정 합니다. 처음에는이 값이 "예"로 설정 되어 있으므로 Microsoft Access 드라이버가 사용자 정의 트랜잭션의 커밋이 완료 될 때까지 대기 합니다.<br /><br /> 이 옵션을 False로 설정 하면 다중 사용자 환경에서 예기치 않은 결과가 발생할 수 있습니다.|이 옵션을 동적으로 설정 하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대 한 호출에서 **usercommitsync** 키워드를 사용 합니다.|
