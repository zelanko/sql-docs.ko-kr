---
title: Machine learning에 대 한 데이터 수집 문제 해결
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f7d5e39d0ca0a89312a6fefd261eff950859d0a2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343391"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Machine learning에 대 한 데이터 수집 문제 해결

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 문제를 해결 하려고 하거나 Microsoft 고객 지원의 도움을 받을 때 사용 해야 하는 데이터 수집 방법을 설명 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (R 및 Python)

## <a name="sql-server-version-and-edition"></a>SQL Server 버전 및 에디션

SQL Server 2016 R Services는 통합 R 지원을 포함 하는 SQL Server의 첫 번째 릴리스입니다. SQL Server 2016 SP1 (서비스 팩 1)에는 외부 스크립트를 실행 하는 기능을 비롯 하 여 몇 가지 주요 개선 사항이 포함 되어 있습니다. SQL Server 2016 고객 인 경우 SP1 이상을 설치 하는 것을 고려해 야 합니다.

SQL Server 2017는 Python 언어 통합을 추가 했습니다. 이전 릴리스에서는 Python 기능 통합을 가져올 수 없습니다.

버전 및 버전을 가져오는 방법에 대 한 자세한 내용은이 문서를 참조 하세요 .이 문서는 각 [SQL Server 버전](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)의 빌드 번호를 나열 합니다.

사용 중인 SQL Server 버전에 따라 일부 기계 학습 기능을 사용할 수 없거나 제한 될 수 있습니다. 다음 문서는 Enterprise, Developer, Standard 및 Express edition의 기계 학습 기능 목록입니다.

* [SQL Server의 버전 및 지원 되는 기능](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [SQL Server 버전별 R 및 Python 기능](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>R 언어 및 도구 버전

일반적으로 R Services 기능 또는 Machine Learning Services 기능을 선택할 때 설치 되는 Microsoft R 버전은 SQL Server 빌드 번호에 따라 결정 됩니다. SQL Server 업그레이드 하거나 패치 하는 경우 R 구성 요소를 업그레이드 하거나 패치 해야 합니다.

릴리스 목록과 R 구성 요소 다운로드에 대 한 링크는 인터넷에 [액세스 하지 않고 machine learning 구성 요소 설치](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)를 참조 하세요. 인터넷에 액세스할 수 있는 컴퓨터에서는 필요한 R 버전이 자동으로 식별 되 고 설치 됩니다.

바인딩 이라는 프로세스에서 SQL Server 데이터베이스 엔진과 별도로 R 서버 구성 요소를 업그레이드할 수 있습니다. 따라서 SQL Server에서 R 코드를 실행할 때 사용 하는 R 버전은 설치 된 SQL Server 버전 및 서버를 최신 R 버전으로 마이그레이션 했는지 여부에 따라 다를 수 있습니다.

### <a name="determine-the-r-version"></a>R 버전 확인

R 버전을 확인 하는 가장 쉬운 방법은 다음과 같은 문을 실행 하 여 런타임 속성을 가져오는 것입니다.

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

마지막 수단으로 서버에서 파일을 열어 설치 된 버전을 확인할 수 있습니다. 이렇게 하려면 rlauncher .config 파일을 찾아 R 런타임 및 현재 작업 디렉터리의 위치를 가져옵니다. 실수로 속성을 변경 하지 않도록 파일의 복사본을 만들고 여는 것이 좋습니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

R 버전 및 RevoScaleR 버전을 가져오려면 R 명령 프롬프트를 열거나 인스턴스와 연결 된 RGui를 엽니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

R 콘솔은 시작 시 버전 정보를 표시 합니다. 예를 들어 다음 버전은 SQL Server 2017에 대 한 기본 구성을 나타냅니다.

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Python 버전

Python 버전을 가져오는 방법에는 여러 가지가 있습니다. 가장 쉬운 방법은 Management Studio 또는 다른 SQL 쿼리 도구에서이 문을 실행 하는 것입니다.

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

Machine Learning Services 실행 되 고 있지 않은 경우 pythonlauncher 파일을 확인 하 여 설치 된 Python 버전을 확인할 수 있습니다. 실수로 속성을 변경 하지 않도록 파일의 복사본을 만들고 여는 것이 좋습니다.

1. SQL Server 2017에만 해당:`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. **PYTHONHOME**에 대 한 값을 가져옵니다.
3. 현재 작업 디렉터리의 값을 가져옵니다.

> [!NOTE]
> SQL Server 2017에 Python과 R을 모두 설치한 경우 작업 디렉터리와 작업자 계정의 풀이 R 및 Python 언어에 대해 공유 됩니다.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>R 또는 Python의 여러 인스턴스가 설치 되어 있나요?

컴퓨터에 R 라이브러리 복사본이 둘 이상 설치 되어 있는지 확인 하십시오. 이 중복은 다음과 같은 경우에 발생할 수 있습니다.

* 설치 하는 동안 R Services (데이터베이스 내)와 R 서버 (독립 실행형)를 둘 다 선택 합니다.
* SQL Server 외에도 Microsoft R Client를 설치 합니다.
* Visual Studio용 R 도구, R Studio, Microsoft R Client 또는 다른 R IDE를 사용 하 여 다른 R 라이브러리 집합이 설치 되었습니다.
* 컴퓨터가 SQL Server의 여러 인스턴스를 호스트 하 고 둘 이상의 인스턴스가 기계 학습을 사용 합니다.

Python에도 동일한 조건이 적용 됩니다.

여러 라이브러리나 런타임이 설치 된 경우 SQL Server 인스턴스에서 사용 되는 Python 또는 R 런타임과 관련 된 오류만 표시 되는지 확인 합니다.

## <a name="origin-of-errors"></a>오류의 출처

R 코드를 실행 하려고 할 때 표시 되는 오류는 다음 원본에서 비롯 될 수 있습니다.

* 저장 프로시저 sp_execute_external_script를 포함 하는 SQL Server 데이터베이스 엔진
* SQL Server 신뢰할 수 있는 실행 패드
* R 및 Python 발사기 및 위성 프로세스를 비롯 한 확장성 프레임 워크의 기타 구성 요소
* Microsoft ODBC (Open Database Connectivity)와 같은 공급자
* R 언어

처음으로 서비스를 사용 하 여 작업 하는 경우 어떤 서비스가 어떤 서비스에서 발생 했는지를 확인 하기가 어려울 수 있습니다. 정확한 메시지 텍스트 뿐만 아니라 메시지를 확인 한 컨텍스트를 캡처하는 것이 좋습니다. Machine learning 코드를 실행 하는 데 사용 하는 클라이언트 소프트웨어에 유의 하세요.

* Management Studio를 사용 하 고 있습니까? 외부 응용 프로그램 인가요?
* 원격 클라이언트에서 R 코드를 실행 하 고 있습니까? 아니면 저장 프로시저에서 직접 실행 합니까?

## <a name="sql-server-log-files"></a>로그 파일 SQL Server

최신 SQL Server 오류 로그를 가져옵니다. 오류 로그의 전체 집합은 다음 기본 로그 디렉터리의 파일로 구성 됩니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 정확한 폴더 이름은 인스턴스 이름에 따라 달라 집니다.

## <a name="errors-returned-by-spexecuteexternalscript"></a>Sp_execute_external_script에서 반환 된 오류

Sp_execute_external_script 명령을 실행할 때 반환 되는 오류의 전체 텍스트를 가져옵니다 (있는 경우).

R 또는 Python 문제를 고려 하 여 제거 하는 경우이 스크립트를 실행할 수 있습니다 .이 스크립트는 R 또는 Python 런타임을 시작 하 고 데이터를 앞뒤로 전달 합니다.

**R의 경우**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Python의 경우**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>확장성 프레임 워크에서 생성 된 오류

SQL Server는 외부 스크립트 언어 런타임에 대 한 별도의 로그를 생성 합니다. 이러한 오류는 Python 또는 R 언어에서 생성 되지 않습니다. 이러한 구성 요소는 언어별 시작 관리자와 해당 위성 프로세스를 포함 하 여 SQL Server의 확장성 구성 요소에서 생성 됩니다.

이러한 로그는 다음과 같은 기본 위치에서 가져올 수 있습니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 정확한 폴더 이름은 인스턴스 이름에 따라 다릅니다. 구성에 따라 폴더가 다른 드라이브에 있을 수 있습니다.

예를 들어 다음 로그 메시지는 확장성 프레임 워크와 관련 되어 있습니다.

* *사용자 MSSQLSERVER01 LogonUser가 실패 했습니다.*
  
  이는 외부 스크립트를 실행 하는 작업자 계정이 인스턴스에 액세스할 수 없음을 나타낼 수 있습니다.

* *InitializePhysicalUsersPool 실패*
  
  이 메시지는 보안 설정에 따라 외부 스크립트를 실행 하는 데 필요한 작업자 계정 풀이 생성 되지 않도록 하는 것을 의미할 수 있습니다.

* *보안 컨텍스트 관리자를 초기화 하지 못했습니다.*

* *위성 세션 관리자를 초기화 하지 못했습니다.*

## <a name="system-events"></a>시스템 이벤트

1. Windows 이벤트 뷰어를 열고 **시스템 이벤트** 로그에서 문자열 실행 *패드*를 포함 하는 메시지를 검색 합니다.
2. ExtLaunchErrorlog 로그 파일을 열고 문자열 *ErrorCode*를 찾습니다. ErrorCode와 연결 된 메시지를 검토 합니다.

예를 들어 다음 메시지는 SQL Server 확장성 프레임 워크와 관련 된 일반적인 시스템 오류입니다.

* *다음 오류 때문에 SQL Server 실행 패드 (MSSQLSERVER) 서비스를 시작 하지 못했습니다.<text>*

* *서비스가 시작 또는 제어 요청에 시기 적절 하 게 응답 하지 않았습니다.*

* *SQL Server 실행 패드 (MSSQLSERVER) 서비스가 연결 되기를 기다리는 동안 제한 시간 (12만 밀리초)에 도달 했습니다.*

## <a name="dump-files"></a>덤프 파일

디버깅에 대해 잘 알고 있는 경우 덤프 파일을 사용 하 여 실행 패드에서 오류를 분석할 수 있습니다.

1. SQL Server에 대 한 설치 부트스트랩 로그가 포함 된 폴더를 찾습니다. 예를 들어 SQL Server 2016에서 기본 경로는 C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\log의 summary.txt입니다.
2. 확장성과 관련 된 부트스트랩 로그 하위 폴더를 엽니다.
3. 지원 요청을 제출 해야 하는 경우이 폴더의 전체 내용을 zip 파일에 추가 합니다. 예: C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
정확한 위치는 사용자의 시스템에서 다를 수 있으며, C 드라이브가 아닌 다른 드라이브에 있을 수 있습니다. Machine learning이 설치 된 인스턴스에 대 한 로그를 가져와야 합니다.

## <a name="configuration-settings"></a>구성 설정

이 섹션에는 R 또는 Python 스크립트를 실행할 때 오류의 원인이 될 수 있는 추가 구성 요소 또는 공급자가 나열 되어 있습니다.

### <a name="what-network-protocols-are-available"></a>사용할 수 있는 네트워크 프로토콜은 무엇 인가요?

Machine Learning Services 확장성 구성 요소 간의 내부 통신 및 외부 R 또는 Python 클라이언트와의 통신을 위해 다음과 같은 네트워크 프로토콜이 필요 합니다.

* 명명된 파이프
* TCP/IP

SQL Server 구성 관리자를 열어 프로토콜이 설치 되어 있는지 여부를 확인 하 고 설치 된 경우 사용 여부를 확인 합니다.

### <a name="security-configuration-and-permissions"></a>보안 구성 및 사용 권한

작업자 계정:

1. 제어판에서 **사용자 및 그룹**을 열고 외부 스크립트 작업을 실행 하는 데 사용 되는 그룹을 찾습니다. 기본적으로 그룹은 **SQLRUserGroup**입니다.
2. 그룹이 있고 하나 이상의 작업자 계정을 포함 하 고 있는지 확인 하십시오.
3. SQL Server Management Studio에서 R 또는 Python 작업이 실행 될 인스턴스를 선택 하 고 **보안**을 선택한 다음 SQLRUserGroup에 대 한 로그온이 있는지 여부를 확인 합니다.
4. 사용자 그룹에 대 한 사용 권한을 검토 합니다.

개별 사용자 계정:

1. 인스턴스가 혼합 모드 인증, SQL 로그인만 또는 Windows 인증만 지원 하는지 여부를 확인 합니다. 이 설정은 R 또는 Python 코드 요구 사항에 영향을 줍니다.
2. R 코드를 실행 해야 하는 각 사용자에 대해 R에서 개체가 기록 될 각 데이터베이스에 대해 필요한 권한 수준을 결정 하거나, 데이터에 액세스 하거나, 개체가 생성 됩니다.
3. 스크립트 실행을 사용 하도록 설정 하려면 역할을 만들거나 필요에 따라 다음 역할에 사용자를 추가 합니다.

   - *Db_owner*: 모든 외부 스크립트를 실행 해야 합니다.
   - *db_datawriter*: R 또는 Python에서 결과를 작성 합니다.
   - *db_ddladmin*: 새 개체를 만듭니다.
   - *db_datareader*: R 또는 Python 코드에서 사용 하는 데이터를 읽을 수 있습니다.
4. SQL Server 2016를 설치할 때 기본 시작 계정을 변경 했는지 여부를 확인 합니다.
5. 사용자가 새 R 패키지를 설치 하거나 다른 사용자가 설치한 R 패키지를 사용 해야 하는 경우 인스턴스에서 패키지 관리를 사용 하도록 설정한 다음 추가 권한을 할당 해야 할 수 있습니다. 자세한 내용은 [R 패키지 관리 사용 또는 사용 안 함](r/r-package-how-to-enable-or-disable.md)을 참조 하세요.

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>어떤 폴더에 바이러스 백신 소프트웨어가 잠금 됩니까?

바이러스 백신 소프트웨어는 폴더를 잠글 수 있으며,이로 인해 machine learning 기능의 설정과 성공적인 스크립트 실행이 모두 방지 됩니다. SQL Server 트리에 있는 모든 폴더에 바이러스 검사가 적용 되는지 여부를 확인 합니다.

그러나 여러 서비스 또는 기능이 인스턴스에 설치 된 경우 인스턴스에서 사용 하는 모든 가능한 폴더를 열거 하기 어려울 수 있습니다. 예를 들어 새 기능을 추가 하는 경우 새 폴더를 식별 하 고 제외 해야 합니다.

또한 일부 기능은 런타임에 동적으로 새 폴더를 만듭니다. 예를 들어 메모리 내 OLTP 테이블, 저장 프로시저 및 함수는 모두 런타임에 새 디렉터리를 만듭니다. 이러한 폴더 이름에는 종종 Guid가 포함 되어 있어 예측할 수 없습니다. SQL Server 신뢰할 수 있는 실행 패드는 R 및 Python 스크립트 작업에 대 한 새 작업 디렉터리를 만듭니다.

SQL Server 프로세스 및 해당 기능에 필요한 모든 폴더를 제외 하는 것은 불가능할 수 있으므로 전체 SQL Server 인스턴스 디렉터리 트리를 제외 하는 것이 좋습니다.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>방화벽이 SQL Server에 대해 열려 있나요? 인스턴스가 원격 연결을 지원 하나요?

1. SQL Server 원격 연결을 지원 하는지 여부를 확인 하려면 [원격 서버 연결 구성](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)을 참조 하세요.

2. SQL Server에 대 한 방화벽 규칙이 생성 되었는지 여부를 확인 합니다. 보안상의 이유로 기본 설치에서는 원격 R 또는 Python 클라이언트가 인스턴스에 연결 하는 것이 불가능할 수 있습니다. 자세한 내용은 [SQL Server에 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)을 참조 하세요.

## <a name="see-also"></a>참조

[SQL Server에서 기계 학습 문제 해결](machine-learning-troubleshooting-faq.md)
