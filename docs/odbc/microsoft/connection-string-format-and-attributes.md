---
title: "연결 문자열 형식 및 특성 | Microsoft Docs"
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
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79d5cabb884262b052429da53cf19c360048dd21
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connection-string-format-and-attributes"></a>연결 문자열 형식 및 특성
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 대화 상자를 사용 하는 대신 일부 응용 프로그램 데이터 원본 연결 정보를 지정 하는 연결 문자열을 필요할 수 있습니다. 연결 문자열은 다양 한 드라이버를 데이터 원본에 연결 하는 방법을 지정 하는 특성으로 이루어져 있습니다. 특성에서 해당 데이터 원본 연결을 만들 수 전에 알아야 하는 드라이버 정보의 특정 부분을 식별 합니다. 각 드라이버에는 다른 특성 집합이 있을 수 있지만 연결 문자열 형식은 항상 동일 합니다. 연결 문자열의 다음 형식은 같습니다.  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Microsoft ODBC Driver for Oracle 사용 되는 드라이버의 첫 번째 버전의 연결 문자열 형식을 지원 `CONNECTSTRING`대신 = `SERVER=`합니다.  
  
 지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, `Trusted_Connection=yes` 연결 문자열에 사용자 ID와 암호 정보 대신 합니다.  
  
 데이터 원본을 지정 해야 UID, PWD, 서버 (또는 CONNECTSTRING)를 지정 하지 않으면 이름을 지정 하 고 드라이버 특성입니다. 그러나 다른 모든 특성은 선택적입니다. 해당 특성의 관련 DSN 탭에 지정 된 경우 특성을 지정 하지 않으면 기본값으로 **ODBC 데이터 원본 관리자** 대화 상자. 특성 값은 대/소문자 구분 수 있습니다.  
  
 연결 문자열에 대 한 특성은 다음과 같습니다.  
  
|Attribute|Description|기본값|  
|---------------|-----------------|-------------------|  
|DSN|데이터 원본 이름은의 드라이버 탭에 나열 된는 **ODBC 데이터 원본 관리자** 대화 상자.|""|  
|PWD|에 액세스 하려면 Oracle 서버에 대 한 암호입니다. 이 드라이버는 Oracle 암호에 배치 하는 제한 사항을 지원 합니다.|""|  
|SERVER|에 액세스 하려면 Oracle 서버에 대 한 연결 문자열입니다.|""|  
|UID|Oracle 서버 사용자 이름입니다. 시스템에 따라이 특성 하지 못할 선택적-즉, 특정 데이터베이스 및 테이블이이 특성에 필요할 보안상의 이유로 사용 합니다.<br /><br /> 사용 하 여 "/" Oracle을 사용 하도록 운영 체제 인증 합니다.|""|  
|BUFFERSIZE|열을 인출할 때 사용 되는 최적의 버퍼 크기입니다.<br /><br /> 드라이버 인출 Oracle 서버에서 하나의 인출이이 크기의 버퍼에 맞게 충분 한 행이 반환 되도록 최적화 됩니다. 많은 데이터를 인출 하는 경우 성능을 향상 시키기 위해 값이 클수록는 경향이 있습니다.|65535|  
|SYNONYMCOLUMNS|이 값이 true (1), SQLColumn () API 호출 열 정보를 반환 합니다. SQLColumn (), 테이블 및 뷰에 대 한 열만 반환합니다. Oracle에 대 한 ODBC 드라이버는이 값을 설정 하지 않은 경우 더 빠른 액세스를 제공 합니다.|1.|  
|REMARKS|이 값이 true (1), 드라이버에 대 한 설명 열을 반환 된 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 결과 집합입니다. Oracle에 대 한 ODBC 드라이버는이 값을 설정 하지 않은 경우 더 빠른 액세스를 제공 합니다.|0|  
|StdDayOfWeek|DAYOFWEEK 스칼라 ODBC 규칙을 적용 합니다. 기본적으로이 켜져 있지만 지역화 된 버전을 해야 하는 사용자는 Oracle에서 반환 하는 관계 없이 사용 하도록 동작을 변경할 수 있습니다.|1.|  
|GuessTheColDef|드라이버에 대 한 0이 아닌 값을 반환할지 여부를 지정 된 *cbColDef* 의 인수 **SQLDescribeCol**합니다. 될 Oracle 정의 배율 없음 계산와 같은 숫자 열에만 적용 됩니다. 열과 열 또는 소수 자릿수가 없이 수로 정의 합니다. A **SQLDescribeCol** Oracle 해당 정보를 제공 하지 않는 전체 자릿수에 대 한 호출이 반환 130입니다.|0|  
  
 예를 들어 MyOracleServerOracle 서버와 Oracle 사용자 MyUserID를 사용 하 여 MyDataSource 데이터 원본에 연결 하는 연결 문자열 다음과 같습니다.  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 운영 체제 인증 및 MyOtherOracleServerOracle 서버를 사용 하 여 MyOtherDataSource 데이터 원본에 연결 하는 연결 문자열이 합니다.  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```

