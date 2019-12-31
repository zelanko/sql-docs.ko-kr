---
title: SQL Native Client ODBC 앱 만들기
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, architecture
- SQL Server Native Client ODBC driver, creating applications
- ODBC function calls
- ODBC, header files
- ODBC applications
- ODBC applications, creating
- SQL Server Native Client ODBC driver, extensions
- applications [SQL Server Native Client]
- SQL Server Native Client ODBC driver, ODBC architecture
- extensions [ODBC]
- ODBC, driver extensions
- function calls [ODBC]
ms.assetid: c83c36e2-734e-4960-bc7e-92235910bc6f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cf46cdf2fb658623a549f3eef160ae6293ab9c7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247385"
---
# <a name="creating-a-driver-application"></a>드라이버 애플리케이션 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 아키텍처에는 다음과 같은 기능을 수행하는 네 가지 구성 요소가 있습니다.  
  
|구성 요소|기능|  
|---------------|--------------|  
|애플리케이션|ODBC 데이터 원본과 통신하는 ODBC 함수를 호출하고, SQL 문을 전송하고, 결과 집합을 처리합니다.|  
|드라이버 관리자|애플리케이션과 애플리케이션에서 사용하는 모든 ODBC 드라이버 사이의 통신을 관리합니다.|  
|드라이버|애플리케이션으로부터의 모든 ODBC 호출을 처리하고, 데이터 원본에 연결하고, 애플리케이션에서 데이터 원본으로 SQL 문을 전달하고, 애플리케이션에 결과를 반환합니다. 필요한 경우 드라이버는 애플리케이션에서 전달된 ODBC SQL을 데이터 원본에서 사용하는 기본 SQL로 변환합니다.|  
|데이터 원본|드라이버가 DBMS의 특정 데이터 인스턴스에 액세스하는 데 필요한 모든 정보를 포함합니다.|  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버를 사용 하 여 인스턴스와 통신 하는 응용 프로그램은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다음 작업을 수행 합니다.  
  
-   데이터 원본에 연결  
  
-   데이터 원본에 SQL 문 전송  
  
-   데이터 원본에서 문의 결과 처리  
  
-   오류 및 메시지 처리  
  
-   데이터 원본에 대한 연결 종료  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버에 대해 작성 된 더 복잡 한 응용 프로그램은 다음 작업을 수행할 수도 있습니다.  
  
-   커서를 사용하여 결과 집합에서 위치 제어  
  
-   트랜잭션 컨트롤에 대해 커밋 또는 롤백 작업 요청  
  
-   둘 이상의 서버가 관련된 분산 트랜잭션 수행  
  
-   원격 서버에서 저장 프로시저 실행  
  
-   카탈로그 함수를 호출하여 결과 집합의 특성 조회  
  
-   대량 복사 작업 수행  
  
-   대량 데이터 관리 (**varchar (max)**, **nvarchar (max)** 및 **varbinary (max)** 열) 작업  
  
-   데이터베이스 미러링이 구성되어 있는 경우 다시 연결 논리를 사용하여 효과적인 장애 조치(failover) 수행  
  
-   성능 데이터 및 장기 실행 쿼리 기록  
  
 ODBC 함수를 호출하려면 C 또는 C++ 애플리케이션에 sql.h, sqlext.h 및 sqltypes.h 헤더 파일이 포함되어야 하며 ODBC 설치 관리자 API 함수를 호출하려면 애플리케이션에 odbcinst.h 헤더 파일이 포함되어야 합니다. 유니코드 ODBC 애플리케이션에는 sqlucode.h 헤더 파일이 반드시 포함되어야 합니다. ODBC 애플리케이션은 odbc32.lib 파일에 연결되어야 하고 ODBC 설치 관리자 API 함수를 호출하는 ODBC 애플리케이션은 odbccp32.lib 파일에 연결되어야 합니다. 이러한 파일은 Windows Platform SDK에 포함되어 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client odbc 드라이버를 비롯 한 많은 odbc 드라이버는 드라이버별 ODBC 확장을 제공 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버별 확장을 활용 하려면 응용 프로그램에 sqlncli 헤더 파일이 포함 되어야 합니다. 이 헤더 파일에는 다음과 같은 항목이 들어 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 드라이버별 연결 특성입니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 드라이버별 문 특성  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 드라이버별 열 특성입니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]별 데이터 형식  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]별 사용자 정의 데이터 형식  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 드라이버별 [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) 형식입니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 드라이버 진단 필드입니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]별 진단 동적 함수 코드  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]별 네이티브 C 데이터 형식용 C/C++ 형식 정의(C 데이터 형식 SQL_C_BINARY에 열이 바인딩된 경우 반환됨)  
  
-   SQLPERF 데이터 구조용 형식 정의  
  
-   ODBC 연결을 통한 대량 복사 API 사용을 지원하기 위한 대량 복사 매크로 및 프로토타입  
  
-   연결된 서버와 해당 카탈로그의 목록을 위해 분산 쿼리 메타데이터 API 함수 호출  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버의 대량 복사 기능을 사용 하는 모든 C 또는 c + + odbc 응용 프로그램은 sqlncli11 파일에 연결 되어야 합니다. 또한 분산 쿼리 메타데이터 API 함수를 호출하는 애플리케이션도 sqlncli11.lib 파일에 연결되어야 합니다. Sqlncli 및 sqlncli11 파일은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개발자 도구의 일부로 배포 됩니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Include 및 Lib 디렉터리는 다음과 같이 컴파일러의 INCLUDE 및 LIB 경로에 있습니다.  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 애플리케이션을 빌드할 때는 애플리케이션에서 여러 개의 ODBC 호출을 동시에 유지해야 하는지 여부를 초기 단계에서 결정해야 합니다. 여러 개의 동시 ODBC 호출을 지원하는 방법에는 두 가지가 있으며 이 섹션의 나머지 항목에서 설명합니다. 자세한 내용은 [ODBC 프로그래머 참조](https://go.microsoft.com/fwlink/?LinkId=45250)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [비동기 모드와 SQLCancel](../../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)  
  
-   [다중 스레드 애플리케이션](../../../relational-databases/native-client/odbc/creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
