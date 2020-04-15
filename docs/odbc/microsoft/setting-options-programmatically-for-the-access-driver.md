---
title: 액세스 드라이버에 대한 프로그래밍 방식으로 옵션 설정 | 마이크로 소프트 문서
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
ms.openlocfilehash: 9a90f0a20569a2a0a5bb93dec7aa4b95b50093dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300793"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Access 드라이버에 프로그래밍 방식으로 옵션 설정

|옵션|설명|메서드|  
|------------|-----------------|------------|  
|버퍼 크기|Microsoft Access에서 디스크로 데이터를 전송하는 데 사용되는 내부 버퍼의 크기(킬로바이트)입니다. 기본 버퍼 크기는 2048KB(2048로 표시)입니다. 256으로 나눌 수 있는 모든 정수 값을 입력할 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 MAXBUFFERSIZE 키워드를 사용합니다.|  
|데이터 원본 이름|급여 또는 인력과 같은 데이터 원본을 식별하는 이름입니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **DSN** 키워드를 사용합니다.|  
|데이터베이스|Microsoft Access 데이터 원본은 데이터베이스를 선택하거나 만들지 않고도 설정할 수 있습니다. 설정 시 데이터베이스가 제공되지 않으면 데이터 원본에 연결할 때 데이터베이스 파일을 선택하라는 메시지가 표시됩니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **DBQ** 키워드를 사용합니다.|  
|설명|데이터 소스내의 데이터에 대한 선택적 설명; 예를 들어 "고용 일자, 급여 이력 및 모든 직원의 현재 검토"를 예로 들 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **DESCRIPTION** 키워드를 사용합니다.|  
|단독|**배타적** 상자를 선택하면 데이터베이스가 단독 모드에서 열리며 한 번에 한 명의 사용자만 액세스할 수 있습니다. 배타적 모드에서 실행할 때 성능이 향상됩니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **EXCLUSIVE** 키워드를 사용합니다.|  
|암시적 커밋싱크|트랜잭션 외부에서 변경한 내용이 데이터베이스에 기록되는 방법을 결정합니다. 이 값은 처음에 "예"로 설정되어 있으며, 이는 Microsoft Access 드라이버가 내부/암시적 트랜잭션의 커밋이 완료될 때까지 기다립니다.|이 옵션은 Microsoft Access 드라이버의 **고급 옵션 설정** 대화 상자에 포함되어 있습니다.|  
|페이지 시간 시간|페이지(사용하지 않은 경우)가 제거되기 전에 버퍼에 남아 있는 기간을 밀리초 단위로 지정합니다. Microsoft Access 드라이버의 경우 기본값은 500밀리초(0.5초)입니다. 이 옵션은 ODBC 드라이버를 사용하는 모든 데이터 원본에 적용됩니다.<br /><br /> 고유한 지연으로 인해 페이지 시간 시간이 0이 될 수 없습니다. 페이지 시간 초과 옵션이 해당 값 아래로 설정되어 있더라도 페이지 시간 초과가 내재지연보다 적을 수 없습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **PAGETIMEOUT** 키워드를 사용합니다.|  
|읽기 전용|데이터베이스를 읽기 전용으로 지정합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **READONLY** 키워드를 사용합니다.|  
|시스템 데이터베이스|액세스하려는 Microsoft Access 데이터베이스와 함께 사용할 Microsoft Access 시스템 데이터베이스의 전체 경로입니다.<br /><br /> 시스템 **데이터베이스** 버튼을 클릭하여 사용할 시스템 데이터베이스를 선택합니다. ODBC Microsoft Access 드라이버는 사용자에게 이름과 암호를 묻는 메시지를 표시합니다. 기본 이름은 관리자이며 관리자 사용자에 대한 Microsoft Access의 기본 암호는 빈 문자열입니다.<br /><br /> Microsoft Access 데이터베이스의 보안을 강화하려면 새 사용자를 만들어 관리자 사용자를 대체하고 관리자 사용자를 삭제하거나 관리자 사용자가 액세스할 수 있는 개체를 변경합니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **SYSTEMDB** 키워드를 사용합니다.|  
|스레드|사용할 엔진의 배경 스레드 수입니다. Microsoft Access 드라이버의 경우 이 값은 기본값3이지만 변경할 수 있습니다. 데이터베이스에 많은 양의 작업이 있는 경우 스레드 수를 늘릴 수 있습니다.<br /><br /> 이 옵션은 Microsoft Access 드라이버의 **고급 옵션 설정** 대화 상자에 포함되어 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **THREADS** 키워드를 사용합니다.|  
|사용자 커밋싱크|Microsoft Access 드라이버가 명시적 사용자 정의 트랜잭션을 비동기적으로 수행할지 여부를 결정합니다. 이 값은 처음에 "예"로 설정되어 있으며, 이는 Microsoft Access 드라이버가 사용자 정의 트랜잭션의 커밋이 완료될 때까지 기다립니다.<br /><br /> 이 옵션을 False로 설정하면 다중 사용자 환경에서 예기치 않은 결과가 발생할 수 있습니다.|이 옵션을 동적으로 설정하려면 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)에 대한 호출에서 **USERCOMMITSYNC** 키워드를 사용합니다.|
