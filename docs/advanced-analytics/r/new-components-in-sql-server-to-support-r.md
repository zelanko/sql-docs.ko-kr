---
title: "R 지원 하도록 SQL Server의 구성 요소 | Microsoft Docs"
ms.custom: 
ms.date: 04/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2bff53d3e324999c7cdca743d6e7b2ff9f85780
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="components-in-sql-server-to-support-r"></a>R 지원 하도록 SQL Server의 구성 요소

SQL Server 2016 및 2017에서 데이터베이스 엔진 확장성을 지 원하는 R 및 Python 등의 외부 스크립트 언어에 대 한 선택적 구성 요소를 포함 합니다. SQL Server 2016;에서 R 언어에 대 한 지원이 추가 되었습니다. SQL Server 2017 컴퓨터 학습 서비스에서 추가 된 Python을 지원 합니다.

이 항목에서는 R 언어와 특별히 작동 하는 새 구성 요소를 설명 합니다. 이러한 구성 요소와 오픈 소스 R 어떻게 작동 하는지에 대 한 논의 알려면 [R 상호 운용성](r-interoperability-in-sql-server.md)

## <a name="components-and-providers"></a>구성 요소 및 공급자

아키텍처 개요에서 설명한 대로 R을 로드하고 R 코드를 실행하는 셸 외에도 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에는 다음과 같은 추가 구성 요소가 포함됩니다.

### <a name="launchpad"></a>실행 패드 

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 는에서 제공 하는 서비스 [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] 전체 텍스트 인덱싱 및 쿼리 서비스가 전체 텍스트 쿼리를 처리 하기 위한 별도 호스트를 실행 하는 방식과 유사 하 게 외부 스크립트의 실행을 지원 합니다.

실행 패드 서비스는 Microsoft에서 게시하거나 성능 및 리소스 관리 요구 사항을 충족시키는 것으로 Microsoft에서 인증한 신뢰할 수 있는 시작 관리자만 시작합니다. 언어별 아이콘에 대 한 이름을 지정 하는 간단 합니다.

  + R-RLauncher.dll
  + Python-PythonLauncher.dll

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 자체 사용자 계정으로 실행됩니다. 특정 언어 런타임에 대한 각 위성 프로세스는 실행 패드의 사용자 계정을 상속받습니다. 구성 및 실행 패드의 보안 컨텍스트에 대 한 자세한 내용은 참조 하십시오. [보안 개요](../../advanced-analytics/r/security-overview-sql-server-r.md)합니다.

### <a name="bxlserver-and-sql-satellite"></a>BxlServer 및 SQL 위성

BxlServer 간의 통신을 관리 하는 Microsoft에서 제공 하는 실행 파일은 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R 런타임 및 또한 RevoScaleR 함수를 구현 합니다. R 세션을 포함하는 데 사용되는 Windows 작업 개체를 만들고 각 R 작업의 보안 작업 폴더를 프로비전하며 SQL Satellite를 사용하여 R과 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 사이의 데이터 전송을 관리합니다.

실제로 BxlServer는 R과 SQL Server의 통합을 지원하기 위해 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]와 함께 사용되는 R의 컴패니언입니다. BXL 이진 Exchange 언어에 대 한 의미 하 고 Microsoft R Client 또는 Microsoft R Server를 설치할 때에 오른쪽 BxlServer.dll 설치가 같은 SQL Server와 외부 프로세스 간에 데이터를 효율적으로 이동 하는 데 데이터 형식을 참조 합니다.

SQL Satellite는 외부 코드나 C 또는 C++를 사용하여 구현된 외부 런타임을 지원하기 위해 데이터베이스 엔진에서 제공하는 SQL Server 2016의 새로운 확장성 API입니다. BxlServer는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]와 통신하기 위해 SQL Satellite를 사용합니다.

SQL Satellite는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]와 외부 스크립트 언어 간의 빠른 데이터 전송을 위해 최적화된 사용자 지정 데이터 형식을 사용합니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]와 R 간의 통신 중에 형식 변환을 수행하고 입력 및 출력 데이터세트의 스키마를 정의합니다.

BxlServer는 SQL Satellite를 사용하여 다음 작업을 수행합니다.

  + 입력 데이터 읽기
  + 출력 데이터 쓰기
  + 입력 인수 가져오기
  + 출력 인수 쓰기
  + 오류 처리
  + 클라이언트에 표준 출력 및 오류를 다시 작성

SQL Satellite는 확장 이벤트를 사용하여 모니터링할 수 있습니다. 자세한 내용은 [SQL Server R Services의 확장 이벤트](extended-events-for-sql-server-r-services.md)를 참조하세요.

## <a name="communication-channels-between-components"></a>구성 요소 간에 통신 채널

+ **TCP/IP**

    기본적으로 간의 내부 통신 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] SQL 위성 TCP/IP를 사용 하 고 있습니다.

+ **명명된 파이프**

    BxlServer 간의 내부 데이터 전송 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] SQL 위성을 통해 성능 향상을 위해 소유, 압축 된 데이터 형식을 사용 합니다. R 메모리에서 BxlServer로의 데이터는 BXL 형식의 명명된 파이프를 통해 교환됩니다.

+ **ODBC**

    외부 데이터 과학 클라이언트 간의 통신 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에 ODBC를 사용 합니다. R 작업을 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]로 보내는 계정에는 인스턴스에 연결하고 외부 스크립트를 실행하는 권한이 있어야 합니다. 또한 계정은 작업에서 사용하는 모든 데이터에 액세스하거나, 데이터를 쓰거나(예: 결과를 테이블에 저장하는 경우), 데이터베이스 개체를 작성(예: R 함수가 새 저장 프로시저의 일부로 저장되는 경우)할 수 있는 권한이 있어야 합니다.

    원격 클라이언트에서 보낸 R 작업의 계산 컨텍스트로 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 사용하고 R 명령이 외부 소스에서 데이터를 검색해야 하는 경우 ODBC가 쓰기 저장용으로 사용됩니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 원격 R 명령을 실행하는 사용자의 ID를 현재 인스턴스의 사용자 ID로 매핑하고 해당 사용자의 자격 증명을 사용하여 ODBC 명령을 실행합니다. 이 ODBC 호출을 수행하는 데 필요한 연결 문자열은 클라이언트 코드에서 가져옵니다.

    **RODBC**를 사용하여 스크립트 내에서 추가 ODBC 호출을 수행할 수 있습니다. RODBC는 관계형 데이터베이스의 데이터에 액세스하는 데 자주 사용되는 R 패키지입니다. 그러나 일반적으로 성능은 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 사용되는 비슷한 공급자보다 느립니다. 많은 R 스크립트는 RODBC에 대해 포함된 호출을 사용하여 분석에 사용할 "보조" 데이터 집합을 검색합니다. 예를 들어 모델을 학습시키는 저장 프로시저는 SQL 쿼리를 정의하여 모델 교육을 위한 데이터를 얻지만, 포함된 RODBC 호출을 사용하여 추가 요소를 얻거나 조회를 수행하거나 텍스트 파일 또는 Excel과 같은 외부 소스에서 새 데이터를 가져올 수 있습니다.

    다음 코드는 R 스크립트에 포함된 RODBC 호출을 보여 줍니다.

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **다른 프로토콜**

    "청크"에서 사용 하거나 원격 클라이언트에 다시 데이터를 전송 해야 할 수 있는 프로세스도 사용할 수는 있습니다. XDF Microsoft 오른쪽 실제 데이터 전송에서 지 원하는 형식이 인코딩된 blob를 통해입니다.

## <a name="interaction-of-components"></a>구성 요소와의 상호 작용

방금 설명한 구성 요소 아키텍처는 오픈 소스 R 코드가 "있는 그대로" 작동할 수 있도록 보장하고 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터에서 실행되는 코드의 성능을 크게 향상시킵니다. 구성 요소가 R 런타임 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터베이스 엔진과 상호 작용하는 방식은 R 코드가 시작되는 방식에 따라 약간 달라집니다. 주요 시나리오는 이 섹션에 요약되어 있습니다.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>데이터베이스에서 SQL Server에서 실행 되는 R 스크립트

"내부" [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 실행되는 R 코드는 저장 프로시저를 호출하여 실행됩니다. 따라서 저장 프로시저 호출을 만들 수 있는 모든 응용 프로그램은 R 코드의 실행을 시작할 수 있습니다.  이후 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 다음 다이어그램에 요약된 대로 R 코드의 실행을 관리합니다.

![rsql_indb780-01](media/script_in-db-r.png)

1. R 런타임에 대한 요청은 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 전달된 매개 변수  _@language='R'_에 의해 표시됩니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 실행 패드 서비스에 이 요청을 보냅니다.
2. 실행 패드 서비스가 적절한 시작 관리자(이 경우 RLauncher)를 시작합니다.
3. RLauncher가 외부 R 프로세스를 시작합니다.
4. BxlServer는 R 런타임과 함께 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]과 데이터 교환 및 작업 결과 저장소를 관리합니다.
5. SQL 위성 관련된 작업에 대 한 통신을 관리 하 고와 처리 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.
6. BxlServer는 SQL Satellite를 사용하여 상태 및 결과를 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]로 전달합니다.
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 결과를 얻고 관련 작업과 프로세스를 닫습니다.

### <a name="r-scripts-executed-from-a-remote-client"></a>원격 클라이언트에서 실행되는 R 스크립트

을 지 원하는 Microsoft R 원격 데이터 과학 클라이언트에서 연결할 경우의 컨텍스트에서 R 함수를 실행할 수 있습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] RevoScaleR 함수를 사용 하 여 합니다. 이 워크플로는 이전 워크플로와 다르며 다음 다이어그램에 요약되어 있습니다.

![rsql_fromR2db-01](media/remote-sqlcc-from-r2.png)

1. RevoScaleR 함수는 R 런타임 BxlServer를 호출 하는 연결 함수를 호출 합니다.
2. BxlServer는 Microsoft R과 함께 제공되며 R 런타임과 별도의 프로세스로 실행됩니다.
3. BxlServer가 연결 대상을 결정하고 ODBC를 통해 연결을 시작하여 R 데이터 원본 개체에 연결 문자열의 일부로 제공된 자격 증명을 전달합니다.
4. BxlServer가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 엽니다.
5. R 호출, 서비스가 호출 되는 실행 패드에 대 한 설정 변수인 RLauncher 적절 한 시작 관리자를 시작 합니다. 이후 R 코드의 처리는 T-SQL에서 R 코드를 실행하는 프로세스와 비슷합니다.
6. RLauncher가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터에 설치된 R 런타임의 인스턴스를 호출합니다.
7. 결과가 BxlServer로 반환됩니다.
8. SQL Satellite가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]와의 통신 및 관련 작업 개체의 정리를 관리합니다.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]가 클라이언트에 결과를 다시 전달합니다.

## <a name="next-steps"></a>다음 단계

[아키텍처 개요](architecture-overview-sql-server-r.md)

[보안 개요](security-overview-sql-server-r.md)

[보안 고려 사항](security-considerations-for-the-r-runtime-in-sql-server.md)

