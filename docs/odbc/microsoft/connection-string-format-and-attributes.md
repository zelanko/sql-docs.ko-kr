---
title: 연결 문자열 형식 및 특성 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a28c3f7128d05307afba95d288f6a20afd75aeea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652471"
---
# <a name="connection-string-format-and-attributes"></a>연결 문자열 형식 및 특성
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 대화 상자를 사용 하는 대신 일부 응용 프로그램 데이터 원본 연결 정보를 지정 하는 연결 문자열을 필요할 수 있습니다. 연결 문자열 드라이버를 데이터 원본에 연결 하는 방법을 지정 하는 특성의 숫자로 구성 됩니다. 특정 드라이버를 알고 있어야 적절 한 데이터 원본 연결 수 있도록 하는 정보를 식별 하는 특성입니다. 각 드라이버 다른 특성 집합이 있을 수 있지만 연결 문자열 형식은 항상 동일 합니다. 연결 문자열에 다음과 같은 형식:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Oracle 용 Microsoft ODBC 드라이버는 드라이버의 첫 번째 버전의 연결 문자열 형식을 지원 `CONNECTSTRING`대신 = `SERVER=`합니다.  
  
 지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, `Trusted_Connection=yes` 연결 문자열에 사용자 ID와 암호 정보 대신 합니다.  
  
 데이터 소스를 지정 해야 합니다는 UID, PWD, 서버 (또는 CONNECTSTRING)을 지정 하지 않으면 하는 경우 이름 및 드라이버 특성입니다. 그러나 다른 모든 특성은 선택 사항입니다. 해당 특성의 관련 DSN 탭에 지정 된 기본값은 특성을 지정 하지 않으면 경우는 **ODBC 데이터 원본 관리자** 대화 상자. 특성 값은 대/소문자 구분 수 있습니다.  
  
 연결 문자열에 대 한 특성은 다음과 같습니다.  
  
|attribute|Description|기본값|  
|---------------|-----------------|-------------------|  
|DSN|드라이버 탭에서 데이터 원본 이름을 나열 합니다 **ODBC 데이터 원본 관리자** 대화 상자.|""|  
|PWD|액세스 하려면 Oracle 서버에 대 한 암호입니다. 이 드라이버는 Oracle 암호를 배치 하는 제한 사항을 지원 합니다.|""|  
|SERVER|액세스 하려면 Oracle 서버에 대 한 연결 문자열입니다.|""|  
|UID|Oracle 서버 사용자 이름입니다. 시스템에 따라이 특성 되지 않을 수 있습니다 (옵션)-즉, 특정 데이터베이스 및 테이블 필요할 수 있습니다이 특성 보안상의 이유로 합니다.<br /><br /> 사용 하 여 "/" Oracle을 사용 하도록 운영 체제 인증 합니다.|""|  
|BUFFERSIZE|열을 가져올 때 사용 되는 최적의 버퍼 크기입니다.<br /><br /> 드라이버 페치 Oracle 서버 로부터의 페치에서 하나의이 크기의 버퍼에 맞게 충분 한 행 반환 되도록 최적화 합니다. 더 큰 값을 많은 양의 데이터를 인출 하는 경우 성능을 향상 시키기 위해는 경향이 있습니다.|65535|  
|SYNONYMCOLUMNS|이 값이 true (1), SQLColumn () API 호출을 열 정보를 반환 합니다. SQLColumn (), 테이블 및 뷰에 대 한 열만 반환합니다. Oracle 용 ODBC 드라이버는이 값이 설정 되지 않은 빠른 액세스를 제공 합니다.|1|  
|REMARKS|이 값이 true (1), 드라이버에 대 한 설명 열을 반환 합니다는 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 결과 집합입니다. Oracle 용 ODBC 드라이버는이 값이 설정 되지 않은 빠른 액세스를 제공 합니다.|0|  
|StdDayOfWeek|ODBC 표준 DAYOFWEEK 스칼라를 적용합니다. 기본적으로이 켜져 있지만 지역화 해야 하는 사용자는 Oracle 무엇이 든 반환 하는 데 동작을 변경할 수 있습니다.|1|  
|GuessTheColDef|드라이버에 대 한 0이 아닌 값을 반환할지 여부를 지정 합니다 *cbColDef* 인수의 **SQLDescribeCol**합니다. 여기서가 Oracle 정의한 확장 안 함 같은 계산 된 숫자 열에만 적용 됩니다. 열과 열 전체 자릿수 또는 확장 없이 수로 정의 합니다. A **SQLDescribeCol** Oracle 해당 정보를 제공 하지 않는 경우 전체 자릿수에 대 한 호출이 반환 130입니다.|0|  
  
 예를 들어 MyOracleServerOracle Server 및 Oracle 사용자 MyUserID를 사용 하 여 MyDataSource 데이터 원본에 연결 하는 연결 문자열을 다음과 같습니다.  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 운영 체제 인증 및 MyOtherOracleServerOracle 서버를 사용 하 여 MyOtherDataSource 데이터 원본에 연결 하는 연결 문자열을 다음과 같습니다.  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
