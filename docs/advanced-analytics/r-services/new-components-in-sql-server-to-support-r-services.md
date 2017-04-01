---
title: "R 서비스를 지 원하는 SQL Server의 새로운 구성 요소 | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# R 서비스를 지 원하는 SQL Server의 새로운 구성 요소

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 제공 하는 새 구성 요소를 포함 된 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 확장성을 지 원하는 R 언어에 대 한 데이터베이스 엔진입니다. 관리 하는 이러한 구성 요소에 대 한 보안 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 및 나중에 자세히 설명 하겠습니다.

## 새 SQL Server 구성 요소 및 공급자

R을 로드 하 고 아키텍처 개요에 설명 된 대로 R 코드를 실행 하는 셸 외에도 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 이러한 추가 구성 요소도 포함 합니다.

### **실행 패드** 
   [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 는에서 제공 하는 새로운 서비스 [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] 전체 텍스트 인덱싱 및 쿼리 서비스가 전체 텍스트 쿼리를 처리 하기 위한 별도 호스트를 실행 하는 방식과 유사 하 게 외부 스크립트의 실행을 지원 합니다. 
  
  실행 패드 서비스는 Microsoft에서 게시 하는 성능 및 리소스 관리에 대 한 요구 사항을 충족으로 Microsoft에 의해 인증 된 또는 신뢰할 수 있는 아이콘만 시작 됩니다.  [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)], R은 현재 지 원하는 유일한 외부 언어는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]합니다.
  
   [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 자체 사용자 계정으로 실행 합니다. 특정 언어 런타임에 대 한 각 위성 프로세스 실행 패드의 사용자 계정에 상속 됩니다. 구성 및 실행 패드의 보안 컨텍스트 하는 방법에 대 한 자세한 내용은 참조 [보안 개요](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)합니다.

### **BxlServer 및 SQL 위성**
  BxlServer 간의 통신을 관리 하는 Microsoft에서 제공 하는 실행 파일은 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R 런타임 및도 ScaleR 함수를 구현 합니다. R 세션을 프로 비전 각 R 작업에 대 한 보안 작업 폴더를 포함 하는 데 사용 되는 SQL 위성을 사용 하 여 R 사이 데이터 전송을 관리 하는 Windows 작업 개체를 만듭니다 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.  

  실제로 BxlServer 목록은 함께 작동 하는 R과 함께 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R SQL Server와의 통합을 지원 하도록 합니다. BXL 이진 Exchange 언어에 대 한 의미 하 고 SQL Server 및 R.와 같은 외부 프로세스 간에 데이터를 효율적으로 이동 하는 데 사용 하는 데이터 형식을 참조 합니다. 

 SQL 위성 외부 코드 또는 C 또는 c + +를 사용 하 여 구현 하는 외부 런타임 지원 하기 위해 데이터베이스 엔진에 의해 제공 되는 SQL Server 2016에서 새 확장성 API입니다. 현재 R은 지원 되는 유일한 런타임입니다. BxlServer SQL 위성을 사용 하 여와 통신 하기 위한 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.
 
  SQL 위성 간의 빠른 데이터 전송에 대 한 최적화 된 사용자 지정 데이터 형식을 사용 하 여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 및 외부 스크립트 언어입니다. 형식 변환을 수행 하 고 입력 및 출력 데이터 집합의 스키마 간의 통신 하는 동안 정의 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R. 및

  BxlServer 이러한 작업에 대 한 SQL 위성을 사용합니다. 
  - 입력된 데이터 읽기
  - 출력 데이터를 쓰는 중
  - 입력된 인수를 가져오는 중
  - 쓰기 출력 인수입니다.
  - 오류 처리
  - 클라이언트에 STDOUT 및 STDERR를 다시 작성

  확장 이벤트를 사용 하 여 SQL 위성을 모니터링할 수 있습니다. 자세한 내용은 참조 [SQL Server R 서비스에 대 한 확장 이벤트](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)합니다.


## 구성 요소 간의 통신 채널

+ **TCP/IP** 기본적으로 간의 내부 통신 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] SQL 위성 TCP/IP를 사용 하 고 있습니다.

+ **명명된 파이프**

  BxlServer 간의 내부 데이터 전송 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] SQL 위성을 통해 성능 향상을 소유 하 고 압축 된 데이터 형식을 사용 합니다. R 메모리에서 데이터 BxlServer BXL 형식의 명명 된 파이프를 통해 교환 됩니다. 
  
+ **ODBC** 외부 데이터 과학 클라이언트 간의 통신 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 ODBC를 사용 합니다. R을 보내는 계정 작업을 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에 연결 하 고 외부 스크립트를 실행 하려면 두 권한이 있어야 합니다. 또한 계정 (예를 들어 테이블에 결과 저장 하는 경우), 데이터를 작성 하거나 (예를 들어 경우 새 저장된 프로시저의 일부분으로 R 함수를 저장) 데이터베이스 개체를 만들 수는 작업에서 사용 되는 모든 데이터에 액세스할 수 있는 권한이 있어야 합니다.

  때 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 은 R 작업에 대 한 계산 컨텍스트는 원격 클라이언트에서 전송 하 고 R 명령에서는 외부 소스에서 데이터를 검색 해야 하는 대로 사용 ODBC 쓰기 저장에 사용 됩니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 현재 인스턴스에 대 한 사용자의 id로 원격 R 명령을 실행 하는 사용자의 id를 매핑한 해당 사용자의 자격 증명을 사용 하 여 ODBC 명령을 실행 합니다. 이 ODBC 호출을 수행 하는 데 필요한 연결 문자열에서 클라이언트 코드에서 가져옵니다.
  
  추가 ODBC 호출을 수행 스크립트 내를 사용 하 여 **RODBC**합니다. RODBC는 관계형 데이터베이스의 데이터에 액세스 하는 데 사용 하는 인기 있는 R 패키지 그러나 성능이 더 일반적으로에서 사용 하는 비교 가능한 공급자 보다 더 느립니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 여러 R 스크립트는 분석에 사용할 "보조" 데이터 집합을 검색 하는 방법으로 RODBC에 대 한 포함 된 호출을 사용 합니다. 예를 들어 모델을 학습 하는 저장된 프로시저 데이터를 가져올 모델을 학습 하는 것에 대 한 SQL 쿼리를 정의할 수 있지만, 조회를 수행 하거나 텍스트 파일 또는 Excel 등의 외부 원본에서 새 데이터를 가져오는 추가 요소를 가져오려는 경우 포함 된 RODBC 호출을 사용 합니다.

  다음 코드에서는 R 스크립트에 포함 된 RODBC 호출을 보여 줍니다.
   ~~~~
  library(RODBC);
  connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
  dbhandle <- odbcDriverConnect(connStr)
  OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
  ~~~~

+ **다른 프로토콜** "청크"에서 사용 하거나 원격 클라이언트에 다시 데이터를 전송 해야 할 수 있는 프로세스를 사용할 수도 수는 있습니다. XDF Microsoft R. 실제 데이터 전송에서 지 원하는 형식은 인코딩된 blob를 통해입니다.

## 구성 요소 간의 상호 작용

오픈 소스 R 코드를 "있는 그대로" 작업할 수 있다는 보장 하기 위해 제공 된 위에서 설명한 구성 요소 아키텍처에서 실행 되는 코드에 대 한 성능 향상 크게 제공 하는 반면, 한 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터입니다. 구성 요소에서 R 런타임과 상호 작용 하는 방법의 메커니즘 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 R 코드를 시작 하는 방법에 따라 약간 다릅니다. 주요 시나리오는이 섹션에 요약 되어 있습니다. 
 
### SQL Server (데이터베이스)에서 실행 되는 R 스크립트

"내부"에서 실행 되는 R 코드 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 저장된 프로시저를 호출 하 여 실행 됩니다. 따라서 호출 하는 저장된 프로시저를 만들 수 있는 모든 응용 프로그램의 R 코드 실행을 시작할 수 있습니다.  그 이후에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 다음 다이어그램에 요약 된 것 처럼 R 코드의 실행을 관리 합니다.

![rsql_indb780-01](../../advanced-analytics/r-services/media/rsql-indb780-01.png)

1. R 런타임에 대 한 요청은 매개 변수가 가리키는 _@language = 'R'_ 저장된 프로시저에 전달 된 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 실행 패드 서비스에이 요청을 보냅니다.
2. 실행 패드 서비스; 적절 한 시작 관리자를 시작합니다. 이 경우 RLauncher 합니다.
3. RLauncher 외부 R 프로세스를 시작 합니다.
4. R 런타임에 BxlServer 좌표를 사용 하 여 데이터의 교환은 관리를 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 및 작업 결과 저장 합니다.
5. SQL 위성 관련된 작업에 대 한 통신을 관리와 프로세스를 처리량, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.
6. BxlServer SQL 위성을 사용 하 여 상태를 전달 하 고 결과를 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 결과 가져오고 관련된 작업 및 프로세스를 닫습니다. 


### 원격 클라이언트에서 실행 되는 R 스크립트

를 지 원하는 Microsoft R 원격 데이터 과학 클라이언트에서 연결할 때의 컨텍스트에서 R 함수를 실행할 수 있습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ScaleR 함수를 사용 합니다. 이전에서 다른 워크플로 이며 다음 다이어그램에 요약 됩니다.


![rsql_fromR2db-01](../../advanced-analytics/r-services/media/rsql-fromr2db-01.png)

1. ScaleR 함수에 대 한 R 런타임 BxlServer를 호출 하는 연결 함수를 호출 합니다. 
2. BxlServer는 Microsoft R와 함께 제공 되 고 R 런타임에서 별도 프로세스에서 실행 합니다.
3. BxlServer 연결 대상을 확인 하 고 R 데이터 원본 개체에 연결 문자열의 일부로 제공 되는 자격 증명을 전달 하는 ODBC를 사용 하는 연결을 시작 합니다.
4. BxlServer 연결을 열어는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스.
5. R 호출 서비스가 호출 되 면 실행 패드에 턴 변수인 RLauncher 적절 한 시작 관리자를 시작 합니다. 그런 다음 R 코드 처리는 T-SQL에서 R 코드를 실행 하기 위한 프로세스와 유사 합니다.
6. RLauncher에 설치 된 R 런타임의 인스턴스를 호출 하 여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터입니다. 
7. 결과 BxlServer에 반환 됩니다.
8. 과 통신을 관리 하는 SQL 위성 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 와 관련 된 작업 개체의 정리 합니다.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 클라이언트에 결과 전달합니다.

## 참고 항목
[아키텍처 개요](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)
