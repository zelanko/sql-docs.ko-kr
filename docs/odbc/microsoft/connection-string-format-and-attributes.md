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
ms.openlocfilehash: a007f4c7c92bf4254e4d36638cf2d92ba0764be5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68082017"
---
# <a name="connection-string-format-and-attributes"></a>연결 문자열 형식 및 특성
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 일부 응용 프로그램에는 대화 상자를 사용 하는 대신 데이터 원본 연결 정보를 지정 하는 연결 문자열이 필요할 수 있습니다. 연결 문자열은 드라이버가 데이터 원본에 연결 하는 방법을 지정 하는 여러 특성으로 구성 됩니다. 특성은 드라이버에서 적절 한 데이터 원본 연결을 만들기 전에 알아야 할 특정 정보를 식별 합니다. 각 드라이버에는 서로 다른 특성 집합이 있을 수 있지만 연결 문자열 형식은 항상 동일 합니다. 연결 문자열의 형식은 다음과 같습니다.  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Oracle 용 Microsoft ODBC 드라이버는 = 대신를 사용 `CONNECTSTRING`하는 첫 번째 버전의 드라이버에 대 한 연결 문자열 형식을 지원 `SERVER=`합니다.  
  
 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 `Trusted_Connection=yes` ID 및 암호 정보를 지정 하는 대신를 지정 해야 합니다.  
  
 UID, PWD, 서버 (또는 CONNECTSTRING) 및 드라이버 특성을 지정 하지 않으면 데이터 원본 이름을 지정 해야 합니다. 그러나 다른 모든 특성은 선택 사항입니다. 특성을 지정 하지 않으면 해당 특성은 **ODBC 데이터 원본 관리자** 대화 상자의 관련 DSN 탭에 지정 된 특성으로 설정 됩니다. 특성 값은 대/소문자를 구분 합니다.  
  
 연결 문자열의 특성은 다음과 같습니다.  
  
|attribute|Description|기본값|  
|---------------|-----------------|-------------------|  
|DSN|**ODBC 데이터 원본 관리자** 대화 상자의 드라이버 탭에 나열 된 데이터 원본 이름입니다.|""|  
|PWD|액세스 하려는 Oracle 서버의 암호입니다. 이 드라이버는 Oracle에서 암호를 저장 하는 제한 사항을 지원 합니다.|""|  
|SERVER|액세스 하려는 Oracle 서버에 대 한 연결 문자열입니다.|""|  
|UID|Oracle 서버 사용자 이름입니다. 시스템에 따라이 특성은 선택 사항이 아닐 수 있습니다. 즉, 특정 데이터베이스와 테이블에는 보안을 위해이 특성이 필요할 수 있습니다.<br /><br /> "/"를 사용 하 여 Oracle의 운영 체제 인증을 사용 합니다.|""|  
|BUFFERSIZE|열을 페치할 때 사용 되는 최적의 버퍼 크기입니다.<br /><br /> 드라이버는 가져오기를 최적화 하 여 Oracle 서버에서 하나의 반입이이 크기의 버퍼를 채우도록 충분 한 행을 반환 합니다. 값이 클수록 많은 데이터를 인출 하는 경우 성능이 향상 됩니다.|65535|  
|SYNONYMCOLUMNS|이 값이 true (1) 이면 SQLColumn () API 호출에서 열 정보를 반환 합니다. 그렇지 않으면 SQLColumn ()에서 테이블 및 뷰에 대 한 열만 반환 합니다. Oracle 용 ODBC 드라이버는이 값이 설정 되지 않은 경우 더 빠른 액세스를 제공 합니다.|1|  
|REMARKS|이 값이 true (1) 이면 드라이버는 [sqlcolumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 결과 집합에 대 한 설명 열을 반환 합니다. Oracle 용 ODBC 드라이버는이 값이 설정 되지 않은 경우 더 빠른 액세스를 제공 합니다.|0|  
|StdDayOfWeek|DAYOFWEEK 스칼라에 대해 ODBC 표준을 적용 합니다. 기본적으로이 기능은 설정 되어 있지만 지역화 된 버전이 필요한 사용자는 Oracle에서 반환 하는 모든 항목을 사용 하도록 동작을 변경할 수 있습니다.|1|  
|GuessTheColDef|드라이버가 **SQLDescribeCol**의 *cbcoldef* 인수에 대해 0이 아닌 값을 반환 해야 하는지 여부를 지정 합니다. 계산 된 숫자 열과 정밀도 나 소수 자릿수가 없는 숫자로 정의 된 열과 같이 Oracle에서 정의한 소수 자릿수가 없는 열에만 적용 됩니다. **SQLDescribeCol** 호출은 Oracle에서 해당 정보를 제공 하지 않을 때 전체 자릿수에 대해 130을 반환 합니다.|0|  
  
 예를 들어 MyOracleServerOracle 서버 및 Oracle 사용자 Mydatasource를 사용 하 여 MyDataSource 데이터 원본에 연결 하는 연결 문자열은 다음과 같습니다.  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 운영 체제 인증 및 MyOtherOracleServerOracle 서버를 사용 하 여 MyOtherDataSource 데이터 원본에 연결 하는 연결 문자열은 다음과 같습니다.  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
