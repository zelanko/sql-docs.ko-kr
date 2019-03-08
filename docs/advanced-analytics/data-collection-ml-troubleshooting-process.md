---
title: Machine learning-SQL Server Machine Learning 서비스에 대 한 데이터 수집 문제 해결
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a4fdd31cddaba1c46cc14ae6dbdeeb6ad92449da
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579133"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Machine learning 위한 데이터 수집 문제 해결

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

여기에서는 자체의 문제를 해결 하거나 Microsoft 고객을 통해 지원 시도할 때 사용 해야 하는 데이터 수집 방법에 설명 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning 서비스 (R 및 Python)

## <a name="sql-server-version-and-edition"></a>SQL Server 버전

SQL Server 2016 R Services에 통합 된 R 지원을 포함 하도록 SQL Server의 첫 번째 릴리스입니다. SQL Server 2016 서비스 팩 1 (SP1) 외부 스크립트를 실행 하는 기능을 비롯 한 몇 가지 주요 향상을 포함 합니다. SQL Server 2016 고객 인 경우 설치 해야 SP1 이상.

SQL Server 2017에 Python 언어 통합을 추가 합니다. 이전 버전의 Python 기능 통합을 가져올 수 없습니다.

각각에 대 한 빌드 번호를 나열 하는이 문서를 참조 하는 버전 및 버전 지원에 대 한 합니다 [SQL Server 버전](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)합니다.

사용 중인 SQL server 버전에 따라 몇 가지 machine learning 기능을 사용할 수 없거나 제한 수 있습니다. 다음 문서 목록 Enterprise, Developer, Standard 및 Express 버전에서는 machine learning 기능입니다.

* [버전 및 SQL Server의 지원 되는 기능](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [SQL Server 버전에서 R 및 Python 기능](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>R 언어 및 도구 버전

일반적으로 Machine Learning 서비스 기능을 사용 하거나 R Services 기능을 선택 하면 설치 된 Microsoft R 버전을 SQL Server 빌드 수에 따라 결정 됩니다. 를 업그레이드 하거나 SQL Server 패치 하는 경우 업그레이드 해야 하거나 해당 R 구성 요소를 패치 해야 합니다.

릴리스 및 R 구성 요소 다운로드에 대 한 링크의 목록을 참조 하세요 [인터넷에 액세스 하지 않고 기계 학습 구성 요소 설치](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)합니다. 인터넷에 연결 된 컴퓨터에서 R의 필수 버전이 식별 이며 자동으로 설치 합니다.

바인딩으로 알려진 프로세스에서 SQL Server 데이터베이스 엔진에서 R Server 구성 요소를 개별적으로 업그레이드 하는 것이 가능 합니다. 따라서 SQL Server에서 R 코드를 실행할 때 사용 하는 R 버전을 모두 설치 된 SQL Server 버전 및 여부 마이그레이션한 서버를 최신 R 버전에 따라 다를 수 있습니다.

### <a name="determine-the-r-version"></a>R 버전 확인

R 버전을 확인 하는 가장 쉬운 방법은 다음과 같습니다. 다음과 같은 문을 실행 하 여 런타임 속성을 가져오려면

```sql
exec sp_execute_external_script
       @language = N'R'
       , @script = N'
# Transform R version properties to data.frame
OutputDataSet <- data.frame(
  property_name = c("R.version", "Revo.version"),
  property_value = c(R.Version()$version.string, Revo.version$version.string),
  stringsAsFactors = FALSE)
# Retrieve properties like R.home, libPath & default packages
OutputDataSet <- rbind(OutputDataSet, data.frame(
  property_name = c("R.home", "libPaths", "defaultPackages"),
  property_value = c(R.home(), .libPaths(), paste(getOption("defaultPackages"), collapse=", ")),
  stringsAsFactors = FALSE)
)
'
WITH RESULT SETS ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));

```

> [!TIP]
> R Services가 작동 하지 않는 경우 RGui에서 R 스크립트 부분만 실행 해 봅니다.

마지막 수단으로 설치 된 버전을 확인 하는 서버에서 파일을 열 수 있습니다. 이렇게 하려면 R 런타임 및 현재 작업 디렉터리의 위치를 가져오려면 rlauncher.config 파일을 찾습니다. 확인 속성을 실수로 변경 하지 않으면 있도록 파일의 복사본을 열어야 하는 것이 좋습니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

R 버전 및 RevoScaleR 버전을 가져오려면 R 명령 프롬프트를 또는 인스턴스와 연결 된 RGui를 엽니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

R 콘솔을 시작할 때 버전 정보를 표시합니다. 예를 들어, 다음 버전 SQL Server 2017에 대 한 기본 구성을 나타냅니다.

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Python 버전

Python 버전을 가져오도록 하는 방법은 여러 가지가 있습니다. Management Studio 또는 다른 SQL 쿼리 도구에서이 문을 실행 하는 가장 쉬운 방법은:

```sql
-- Get Python runtime properties:
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import sys
import pkg_resources
OutputDataSet = pandas.DataFrame(
                    {"property_name": ["Python.home", "Python.version", "Revo.version", "libpaths"],
                    "property_value": [sys.executable[:-10], sys.version, pkg_resources.get_distribution("revoscalepy").version, str(sys.path)]}
)
'
with WITH RESULT SETS (SQL keywords) ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));
```

Machine Learning 서비스를 실행 하지 않는 경우 pythonlauncher.config 파일을 확인 하 여 설치 된 Python 버전을 확인할 수 있습니다. 확인 속성을 실수로 변경 하지 않으면 있도록 파일의 복사본을 열어야 하는 것이 좋습니다.

1. SQL server 2017만: `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. 에 대 한 값을 얻으려면 **PYTHONHOME**합니다.
3. 현재 작업 디렉터리의 값을 가져옵니다.

> [!NOTE]
> SQL Server 2017에 Python 및 R을 설치 하는 경우 R 및 Python 언어에 대 한 작업 디렉터리 및 작업자 계정 풀이 공유 됩니다.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>여러 인스턴스의 R 또는 Python 설치?

R 라이브러리의 사본을 하나 이상 컴퓨터에 설치 되어 있는지 확인 합니다. 이 복제는 다음과 같은 경우에 발생할 수 있습니다.

* 설치 하는 동안 R Services (In-database)와 R Server (독립 실행형)를 선택합니다.
* SQL Server 이외에 Microsoft R 클라이언트를 설치 합니다.
* Visual Studio, R Studio, Microsoft R Client 또는 다른 R IDE 용 R 도구를 사용 하 여 다양 한 R 라이브러리 설치 되었습니다.
* SQL Server의 여러 인스턴스를 호스트 하는 컴퓨터 및 machine learning을 사용 하 여 둘 이상의 인스턴스.

Python에는 동일한 조건이 적용 됩니다.

여러 라이브러리 또는 런타임이 설치 되어 있는지, 있다면 SQL Server 인스턴스에서 사용 되는 Python 또는 R 런타임과 사용 하 여 연결 된 오류만을 얻을 수 있는지 확인 합니다.

## <a name="origin-of-errors"></a>오류 원본

R 코드를 실행 하려고 할 때 표시 되는 오류는 다음 원본 중 하나에서 발생할 수 있습니다.

* 저장된 프로시저 sp_execute_external_script를 포함 하 여 SQL Server 데이터베이스 엔진
* SQL Server 실행 패드를 신뢰할 수 있는
* R 및 Python 시작 관리자 및 위성 프로세스를 포함 하 여 확장성 프레임 워크의 다른 구성 요소
* Microsoft 오픈 같은 공급자 데이터베이스 연결 (ODBC)
* R 언어

처음으로 서비스를 사용 하 여 작업할 때 서비스에서 생성 되는 메시지를 확인 하기 어려울 수 있습니다. 정확한 메시지 텍스트 뿐만 아니라 메시지 살펴보았습니다 컨텍스트 캡처하는 것이 좋습니다. Machine learning 코드를 실행 하는 데 사용 하는 클라이언트 소프트웨어를 note:

* Management Studio를 사용 중 입니까? 외부 응용 프로그램이 있나요?
* 저장된 프로시저를 직접 또는 원격 클라이언트에서 R 코드를 실행 하 시겠습니까?

## <a name="sql-server-log-files"></a>SQL Server 로그 파일

최신 SQL Server 오류 로그를 가져옵니다. 다음 기본 로그 디렉터리에서 파일의 전체 집합이 오류 로그 구성 됩니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 정확한 폴더 이름을 인스턴스 이름에 따라 다릅니다.

## <a name="errors-returned-by-spexecuteexternalscript"></a>Sp_execute_external_script에서 반환한 오류

Sp_execute_external_script 명령을 실행할 때 반환 되는 오류의 전체 텍스트를 있는 경우 가져옵니다.

R 또는 Python 문제를 고려 대상에서 제거 하려면 R 또는 Python 런타임을 시작 하 고 데이터를 앞뒤로 전달이 스크립트를 실행할 수 있습니다.

**R에 대 한**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Python 용**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>확장성 프레임 워크에 의해 생성 된 오류

SQL Server 외부 스크립트 언어 런타임에 대 한 별도 로그를 생성합니다. 이러한 오류는 Python 또는 R 언어에서 생성 되지 않습니다. 해당 하는 언어별 시작 관리자 및 위성 프로세스를 포함 하 여 SQL Server의 확장성 구성 요소에서 생성 됩니다.

다음 기본 위치에서 이러한 로그를 가져올 수 있습니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 정확한 폴더 이름을 인스턴스 이름에 따라 다릅니다. 구성에 따라 폴더는 다른 드라이브에 있을 수 있습니다.

예를 들어, 다음 로그 메시지는 확장성 프레임 워크를 관련이 있습니다.

* *MSSQLSERVER01 사용자에 대 한 logonuser가 실패 했습니다.*
  
  인스턴스는 외부 스크립트를 실행 하는 작업자 계정에 액세스할 수 있다는 의미일 수 있습니다.

* *InitializePhysicalUsersPool 실패*
  
  이 메시지 보안 설정을 설치에서 외부 스크립트를 실행 하는 데 필요한 작업자 계정의 풀을 만들 수 없게 되는 것일 수 있습니다.

* *보안 컨텍스트 관리자 초기화 하지 못했습니다.*

* *위성 세션 관리자 초기화 하지 못했습니다.*

## <a name="system-events"></a>시스템 이벤트

1. Windows 이벤트 뷰어를 열고 검색 합니다 **시스템 이벤트** 문자열이 포함 된 메시지에 대 한 로그 *실행 패드*합니다.
2. ExtLaunchErrorlog 파일을 열고 문자열을 찾습니다 *ErrorCode*합니다. 오류 코드와 관련 된 메시지를 검토 합니다.

예를 들어 다음 메시지는 SQL Server 확장성 프레임 워크와 관련 된 일반적인 시스템 오류:

* *SQL Server 실행 패드 (MSSQLSERVER) 서비스가 다음 오류로 인해 시작 하지 못했습니다.  <text>*

* *서비스가 적시에 시작 또는 제어 요청에 응답 하지 않았습니다.*

* *제한 시간을 연결 하려면 SQL Server 실행 패드 (MSSQLSERVER) 서비스를 기다리는 동안 (120000 밀리초)에 도달 했습니다.*

## <a name="dump-files"></a>덤프 파일

디버깅에 대 한 지식이 인 경우 실행 패드에서 실패를 분석 하는 덤프 파일을 사용할 수 있습니다.

1. SQL Server에 대 한 설치 부트스트랩 로그가 들어 있는 폴더를 찾습니다. 예를 들어, SQL Server 2016에서 기본 경로 C:\Program Files\Microsoft SQL Server\130\Setup bootstrap\log\를 했습니다.
2. 확장성 관련 된 부트스트랩 로그 하위 폴더를 엽니다.
3. 지원 요청을 제출 해야 할 경우이 폴더의 전체 내용을 압축 된 파일에 추가 합니다. 예를 들어, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog 합니다.
  
정확한 위치는 시스템에서 다를 수 있습니다 하 고 C 드라이브가 아닌 다른 드라이브에 있을 수 있습니다. 기계를 설치한 인스턴스에 대 한 로그를 다운로드 해야 합니다.

## <a name="configuration-settings"></a>구성 설정

이 섹션에서는 추가 구성 요소 또는 R 또는 Python 스크립트를 실행 하는 경우 오류의 원인이 될 수 있는 공급자를 나열 합니다.

### <a name="what-network-protocols-are-available"></a>네트워크 프로토콜을 사용할 수 있습니까?

Machine Learning 서비스 및 외부 R 또는 Python 클라이언트를 사용 하 여 통신을 확장성 구성 요소 간의 내부 통신에 대 한 다음 네트워크 프로토콜을 필요합니다.

* 명명된 파이프
* TCP/IP

프로토콜을 설치 및 설치 된 경우 확인에 사용 되는지 여부를 확인 하려면 SQL Server 구성 관리자를 엽니다.

### <a name="security-configuration-and-permissions"></a>보안 구성 및 사용 권한

작업자 계정의 경우:

1. 제어판에서 엽니다 **사용자 및 그룹**, 외부 스크립트 작업을 실행 하는 데 사용 하 여 그룹을 찾습니다. 기본적으로 그룹은 **SQLRUserGroup**합니다.
2. 그룹이 있고 하나 이상의 작업자 계정에 포함 되어 있는지 확인 합니다.
3. SQL Server Management studio에서 R 또는 Python 작업이 실행 될 위치 인스턴스를 선택 합니다. 선택 **보안**, 고 SQLRUserGroup에 대 한 로그온이 있는지 여부를 결정 합니다.
4. 사용자 그룹에 대 한 권한을 검토 합니다.

개별 사용자 계정의 경우:

1. 인스턴스가 혼합 모드 인증만 SQL 로그인 또는 Windows 인증만 지원 하는지 여부를 결정 합니다. 이 설정은 R 또는 Python 코드 요구 사항입니다.
2. R 코드를 실행 해야 하는 각 사용자에 대해 필요한 위치에서 R 개체를 쓸, 데이터에 액세스할 수는 또는 개체를 만들 수는 각 데이터베이스에 대 한 권한 수준을 결정 합니다.
3. 스크립트 실행을 사용 하려면 역할 만들거나 필요에 따라 다음 역할에 사용자를 추가 합니다.

   - 군더더기 *db_owner*: 필요한 모든 외부 스크립트를 실행 합니다.
   - *db_datawriter*: R 또는 Python에서 결과 작성 합니다.
   - *db_ddladmin*: 새 개체를 만듭니다.
   - *db_datareader*: 에 R 또는 Python 코드에서 사용 되는 데이터를 읽습니다.
4. SQL Server 2016을 설치할 때 모든 기본 시작 계정 변경 여부를 note 합니다.
5. 사용자에 게 새 R 패키지를 설치 하거나 다른 사용자가 설치 된 R 패키지를 사용 하 여 필요한 경우 인스턴스에서 패키지 관리를 사용 하도록 설정 하 여 다음 추가 사용 권한을 할당 해야 합니다. 자세한 내용은 [사용 하거나 R 패키지 관리를 사용 하지 않도록](r/r-package-how-to-enable-or-disable.md)합니다.

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>폴더는 바이러스 백신 소프트웨어로 잠금 사항이 있습니까?

바이러스 백신 소프트웨어에 모두 설치 기계 학습 기능 및 성공적인 스크립트 실행을 방지 하는 폴더를 잠글 수 있습니다. SQL Server 트리의 모든 폴더 바이러스 검사 적용 되는지 여부를 결정 합니다.

그러나 인스턴스에서 여러 서비스 또는 기능이 설치 되 면 인스턴스에서 사용 되는 모든 가능한 폴더를 열거 하려면 어려울 수 있습니다. 예를 들어, 새 기능을 추가 하는 경우 새 폴더 여야 식별 하며 제외 합니다.

또한 일부 기능은 새 폴더를 만들거나 동적으로 런타임 시. 예를 들어 메모리 내 OLTP 테이블, 저장된 프로시저 및 함수 모두 런타임에 새 디렉터리를 만듭니다. 이러한 폴더 이름은 대개 guid가 포함 되어 및 예측할 수 없습니다. SQL Server 신뢰할 수 있는 실행 패드는 R에 대 한 새 작업 디렉터리를 만듭니다 및 Python 스크립트 작업.

SQL Server 프로세스 및 해당 기능에 필요한 모든 폴더를 제외할 수 수 없을 수 있으므로, 전체 SQL Server 인스턴스 디렉터리 트리를 제외 하는 것이 좋습니다.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>SQL Server 용 방화벽 열기을입니다. 인스턴스가 원격 연결을 지원 하나요?

1. 확인 하려면 SQL Server 원격 연결을 지원 하는지 여부를 참조 하세요 [원격 서버 연결 구성](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)합니다.

2. SQL Server에 대 한 방화벽 규칙을 만들어졌는지 여부를 결정 합니다. 기본 설치의 경우 보안상의 이유로 하지 못할 수도 있습니다는 인스턴스에 연결 하려면 원격 R 또는 Python 클라이언트에 대 한 합니다. 자세한 내용은 [SQL Server에 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)합니다.

## <a name="see-also"></a>참고자료

[SQL Server에서 기계 학습 문제 해결](machine-learning-troubleshooting-faq.md)
