---
title: 연결 문자열 형식 및 특성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d95866976d2e83c058f83b3a0ae5e9a4e8888ed1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281153"
---
# <a name="connection-string-format-and-attributes"></a>연결 문자열 형식 및 특성
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 일부 응용 프로그램에는 대화 상자를 사용하는 대신 데이터 원본 연결 정보를 지정하는 연결 문자열이 필요할 수 있습니다. 연결 문자열은 드라이버가 데이터 원본에 연결하는 방법을 지정하는 여러 특성으로 구성됩니다. 특성은 적절한 데이터 원본 연결을 만들기 전에 드라이버가 알아야 할 특정 정보를 식별합니다. 각 드라이버마다 다른 특성 집합이 있을 수 있지만 연결 문자열 형식은 항상 동일합니다. 연결 문자열에는 다음과 같은 형식이 있습니다.  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  오라클용 Microsoft ODBC 드라이버는 `CONNECTSTRING` `SERVER=`.  
  
 Windows 인증을 지원하는 데이터 원본 공급자에 연결하는 경우 `Trusted_Connection=yes` 연결 문자열에서 사용자 ID 및 암호 정보 대신 지정해야 합니다.  
  
 UID, PWD, 서버(또는 CONNECTSTRING) 및 드라이버 특성을 지정하지 않으면 데이터 원본 이름을 지정해야 합니다. 그러나 다른 모든 특성은 선택 사항입니다. 특성을 지정하지 않으면 해당 특성은 **ODBC 데이터 원본 관리자** 대화 상자의 관련 DSN 탭에 지정된 특성으로 기본설정됩니다. 특성 값은 대/소문자를 구분할 수 있습니다.  
  
 연결 문자열의 특성은 다음과 같습니다.  
  
|attribute|Description|기본값|  
|---------------|-----------------|-------------------|  
|DSN|**ODBC** 데이터 원본 관리자 대화 상자의 드라이버 탭에 나열된 데이터 원본 이름입니다.|""|  
|PWD|액세스하려는 Oracle Server의 암호입니다. 이 드라이버는 오라클이 암호에 배치하는 제한을 지원합니다.|""|  
|SERVER|액세스하려는 Oracle Server의 연결 문자열입니다.|""|  
|UID|Oracle 서버 사용자 이름입니다. 시스템에 따라 이 특성은 선택 사항이 아닐 수 있습니다.<br /><br /> "/"를 사용하여 오라클의 운영 체제 인증을 사용합니다.|""|  
|버퍼 크기|열을 가져올 때 사용되는 최적의 버퍼 크기입니다.<br /><br /> 드라이버는 오라클 서버에서 가져온 하나의 가져오기가 이 크기의 버퍼를 채울 만큼 충분한 행을 반환하도록 페칭을 최적화합니다. 값이 클수록 많은 데이터를 가져오는 경우 성능이 향상되는 경향이 있습니다.|65535|  
|시니엠칼럼|이 값이 true(1)이면 SQLColumn() API 호출이 열 정보를 반환합니다. 그렇지 않으면 SQLColumn() 테이블 및 뷰에 대한 열만 반환합니다. 오라클의 ODBC 드라이버는 이 값을 설정하지 않을 때 더 빠른 액세스를 제공합니다.|1|  
|REMARKS|이 값이 true(1)이면 드라이버는 SQLColumns 결과 집합에 대한 비고 열을 [반환합니다.](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 오라클의 ODBC 드라이버는 이 값을 설정하지 않을 때 더 빠른 액세스를 제공합니다.|0|  
|세인트데이오브위크|DAYOFWEEK 스칼라에 대한 ODBC 표준을 적용합니다. 기본적으로 이 설정은 켜져 있지만 지역화된 버전이 필요한 사용자는 오라클이 반환하는 모든 것을 사용하도록 동작을 변경할 수 있습니다.|1|  
|추측더콜데프|**SQLDescribeCol의** *cbColDef* 인수에 대해 드라이버가 0이 아닌 값을 반환할지 여부를 지정합니다. 정밀도 또는 축척없이 NUMBER로 정의된 계산된 숫자 열 및 열과 같이 Oracle 정의 배율이 없는 열에만 적용됩니다. **SQLDescribeCol** 호출은 Oracle에서 해당 정보를 제공하지 않을 때 정밀도에 대해 130을 반환합니다.|0|  
  
 예를 들어 MyOracleServerOracle 서버와 Oracle 사용자 MyUserID를 사용하여 MyDataSource 데이터 원본에 연결하는 연결 문자열은 다음과 같은 것입니다.  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 운영 체제 인증 및 MyOtherOracleServerOracle 서버를 사용하여 MyOtherDataSource 데이터 원본에 연결하는 연결 문자열은 다음과 같은 것입니다.  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
