---
title: "Python SQL Server와의 통합에 대 한 구성 요소 | Microsoft Docs"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 07f8e18b4481b2773f3ac16cdea08c27feff1ba3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="components-in-sql-server-to-support-python-integration"></a>Python 통합을 지원 하도록 SQL Server의 구성 요소

SQL Server 2017 년 부터는 컴퓨터 학습 서비스 T-SQL에서 실행할 수 또는 원격으로 SQL Server를 사용 하 여 계산 컨텍스트로 써 실행 하는 외부 언어도 Python을 지원 합니다.

이 항목에서는 확장성을 지 원하는 일반적 SQL Server 2017 및 Python 언어 구성 요소를 구체적으로 설명 합니다.

## <a name="sql-server-components-and-providers"></a>SQL Server 구성 요소 및 공급자

SQL Server 2017 Python 스크립트 실행을 허용 하도록 구성 하려면 여러 단계 프로세스입니다.

1. 확장성 기능을 설치 합니다.
2. 외부 스크립트 실행 기능을 사용 하도록 설정 합니다.
3. 데이터베이스 엔진 서비스를 다시 시작 합니다.

원격 스크립트 실행을 지원 하려면 추가 단계를 수행 해야 할 수 있습니다.

자세한 내용은 참조 [컴퓨터 학습 서비스 설정](setup-python-machine-learning-services.md)

### <a name="launchpad"></a>실행 패드

SQL Server 신뢰할 수 있는 실행 패드에 관리 하 고 전체 텍스트 인덱싱 및 쿼리 서비스가 전체 텍스트 쿼리를 처리 하기 위한 별도 호스트를 실행 하는 방식과 유사 하 게 외부 스크립트를 실행 하는 SQL Server 2016에 도입 된 서비스입니다.

실행 패드 서비스는 Microsoft에서 게시 하는 성능 및 리소스 관리에 대 한 요구 사항을 충족으로 Microsoft에 의해 인증 된 또는 신뢰할 수 있는 아이콘을 시작할 수 있습니다.

+ SQL Server 2017 R 및 Python 3.5를 지원합니다.
+ SQL Server 2016 R을 지원

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 자체 사용자 계정으로 실행됩니다.

> [!TIP]
> 실행 패드를 실행 하는 계정을 변경 하면 관련 파일에 변경 내용이 기록 되도록 하려면 SQL Server 구성 관리자를 사용 하 여 그렇게 해야 합니다.

지원 되는 특정 언어에서 작업을 실행 하려면 실행 패드에서 풀의 보안된 작업자 계정을 가져오고 외부 런타임을 관리 하는 위성 프로세스를 시작:

+ R 언어에 대 한 RLauncher.dll
+ Python 3.5에 대 한 Pythonlauncher.dll

각 위성 프로세스는 실행 패드의 사용자 계정을 상속 하 고 스크립트 실행의 기간에 대 한 해당 작업자 계정을 사용 합니다. Python 스크립트 병렬 프로세스를 사용 하는 경우 동일 하 고 단일 작업자 계정에서 생성 됩니다.

실행 패드의 보안 컨텍스트에 대 한 자세한 내용은 참조 [보안](security-overview-sql-server-python-services.md)합니다.

### <a name="bxlserver-and-sql-satellite"></a>BxlServer 및 SQL 위성

실행 하는 경우 [프로세스 탐색기](https://technet.microsoft.com/sysinternals/processexplorer.aspx) Python 작업이 실행 되는 동안 BxlServer의 하나 또는 여러 인스턴스가 표시 될 수 있습니다.

**BxlServer** 간의 통신을 관리 하는 Microsoft에서 제공 하는 실행 파일은 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 및 Python (또는 R). 외부 스크립트 세션을 각 외부 스크립트 작업에 대 한 프로 비전 보안 작업 폴더를 포함 하는 데 사용 되는 SQL 위성을 사용 하 여 외부 런타임 간의 데이터 전송 관리 하는 Windows 작업 개체를 생성 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.

BxlServer 목록은 사용 하는 Python과 함께 실제로 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 작업을 데이터를 전송 하 고 관리 합니다. BXL 이진 Exchange 언어에 대 한 의미 하 고은 SQL Server와 외부 프로세스 간에 데이터를 효율적으로 이동 하는 데 데이터 형식을 나타냅니다. BxlServer는 Microsoft R Client 및 Microsoft R Server의 중요 한 부분이 이기도합니다.

**SQL 위성** 외부 코드를 지 원하는 SQL Server 2016으로 시작 하는 데이터베이스 엔진에 포함 되는 확장성 API 또는 외부 런타임 C 또는 c + +를 사용 하 여 구현 합니다.

BxlServer는 SQL Satellite를 사용하여 다음 작업을 수행합니다.

+ 입력 데이터 읽기
+ 출력 데이터 쓰기
+ 입력 인수 가져오기
+ 출력 인수 쓰기
+ 오류 처리
+ STDOUT 및 STDERR을 클라이언트에 다시 쓰기

SQL 위성 사이의 고속 데이터 전송을 최적화 되는 사용자 지정 데이터 형식을 사용 하 여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 및 외부 스크립트 언어입니다. 유형 변환을 수행 하 고 입력 및 출력 데이터 집합의 스키마 간의 통신 하는 동안 정의 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 및 외부 스크립트 런타임.

SQL 위성 windows 확장 이벤트 (Xevent)를 사용 하 여 모니터링할 수 있습니다. 자세한 내용은 참조 [R에 대 한 확장 이벤트](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)합니다.

## <a name="communication-channels-between-components"></a>구성 요소 간에 통신 채널

+ **TCP/IP**

  기본적으로 간의 내부 통신 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] SQL 위성 TCP/IP를 사용 하 고 있습니다.

+ **명명된 파이프**

  SQL Satellite를 통한 BxlServer와 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 간의 내부 데이터 전송은 독점적인 압축 데이터 형식을 사용하여 성능을 향상시킵니다. 데이터는 BXL 형식으로 명명 된 파이프를 사용 하 여 Python 및 BxlServer 간에 교환 됩니다.

+ **ODBC**

  외부 데이터 과학 클라이언트 간의 통신 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에 ODBC를 사용 합니다. 스크립트가 전송 하는 계정에 작업 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에 연결 하 고 외부 스크립트 실행 권한을 모두 있어야 합니다.

  또한 태스크에 따라 계정이 이러한 권한을 해야 합니다.

  + 작업에서 사용 하는 데이터 읽기
  + 테이블에 데이터를 쓸: 예를 들어 때 저장 결과 테이블
  + 데이터베이스 개체 만들기: 새 저장된 프로시저의 일환으로 외부 스크립트를 저장 하는 경우 등입니다.

  때 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 원격 클라이언트에서 Python 스크립트 실행 하 고 외부 원본에서 데이터를 검색 해야 Python 실행 파일에 대 한 계산 컨텍스트 기호로 사용 하 고, ODBC는 쓰기 저장에 사용 됩니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]현재 인스턴스에 대 한 사용자의 id로 원격 명령을 실행 하는 사용자의 id를 매핑한 해당 사용자의 자격 증명을 사용 하 여 ODBC 명령을 실행 합니다. 이 ODBC 호출을 수행하는 데 필요한 연결 문자열은 클라이언트 코드에서 가져옵니다.

## <a name="interaction-of-components"></a>구성 요소와의 상호 작용

다음 다이어그램은 각 지원 되는 시나리오에는 Python 런타임의와 상호 작용의 SQL Server 구성 요소를 보여 주는: SQL Server 계산 컨텍스트를 사용 하 여 Python 터미널에서는 스크립트에서 데이터베이스 및 원격 실행을 실행 합니다.

### <a name="python-scripts-executed-in-database"></a>데이터베이스에서 Python 스크립트 실행

Python "내부"를 실행 하는 경우 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 특별 한 저장된 프로시저 내에서 Python 스크립트 캡슐화 해야 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

스크립트 저장된 프로시저에 포함 되었으면, 후 저장된 프로시저 호출을 만들 수 있는 모든 응용 프로그램 Python 코드의 실행을 시작할 수 있습니다.  그 후 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 다음 다이어그램에 요약 된 것 처럼 코드 실행을 관리 합니다.

![스크립트에서 db python](../../advanced-analytics/python/media/script-in-db-python.png)

1. Python 런타임의 대 한 요청은 매개 변수가 가리키는  _@language'Python' =_ 저장된 프로시저에 전달 합니다. SQL Server 실행 패드 서비스에이 요청을 보냅니다.
2. 실행 패드 서비스 시작 적절 한 실행 프로그램입니다. 이 경우 PythonLauncher입니다.
3. PythonLauncher 외부 Python35 프로세스를 시작합니다.
4. BxlServer 데이터 교환 및 작업 결과의 저장소를 관리 하는 Python 런타임의 협력 합니다.
5. SQL 위성 관련된 작업에 대 한 통신을 관리 하 고와 처리 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.
6. BxlServer는 SQL Satellite를 사용하여 상태 및 결과를 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]로 전달합니다.
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 결과를 얻고 관련 작업과 프로세스를 닫습니다.

### <a name="python-scripts-executed-from-a-remote-client"></a>원격 클라이언트에서 실행 하는 Python 스크립트

랩톱 등의 원격 컴퓨터에서 Python 스크립트를 실행 하 고 이러한 조건이 충족 될 경우 SQl Server 컴퓨터의 컨텍스트 내에서 실행 되도록 할 수 있습니다.

+ 스크립트를 적절 하 게 디자인
+ 원격 컴퓨터가 컴퓨터 학습 서비스에서 사용 되는 확장성 라이브러리 설치

다음 다이어그램은 원격 컴퓨터에서 스크립트를 보낼 경우 전체 워크플로 요약 합니다.

![python에서 원격 sqlcc](../../advanced-analytics/python/media/remote-sqlcc-from-python2.png)

1. 지원 되는 함수에 대 한 **revoscalepy**는 Python 런타임의 BxlServer를 호출 하는 연결 함수를 호출 합니다.
2. BxlServer는 컴퓨터 학습 services (In-database) 포함 되어 있으며는 Python 런타임의에서 별도 프로세스로 실행 됩니다.
3. BxlServer 연결 대상을 확인 하 고 Python 스크립트에서 연결 문자열의 일부로 제공 되는 자격 증명을 전달 하는 ODBC를 사용 하는 연결을 시작 합니다.
4. BxlServer가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 엽니다.
5. 외부 스크립트 런타임 호출 되 면 실행 패드 서비스를 호출할 적절 한 시작 관리자를 다시 시작 되는:이 경우 PythonLauncher.dll 합니다. 그 후 t-sql에서 저장된 프로시저에서 Python 코드를 호출 하면 Python 코드의 처리는 비슷합니다는 워크플로에서 처리 됩니다.
6. PythonLauncher Python에 설치 된 인스턴스에 대 한 호출에서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터입니다.
7. 결과가 BxlServer로 반환됩니다.
8. SQL Satellite가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]와의 통신 및 관련 작업 개체의 정리를 관리합니다.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]가 클라이언트에 결과를 다시 전달합니다.

## <a name="next-steps"></a>다음 단계

[SQL Server에서 Python에 대 한 아키텍처 개요](architecture-overview-sql-server-python.md)

