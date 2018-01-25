---
title: "기계 학습-에 대 한 데이터 수집 SQL Server 문제 해결"
ms.custom: 
ms.date: 06/16/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3eec9220734a2e13cb4d355422b5d8c957bf9264
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>기계 학습에 대 한 데이터 수집 문제 해결

이 문서에서는 설치, 구성 또는 SQL Server에서 학습 하는 컴퓨터의 성능 문제를 해결 하려고 할 때 수집 해야 하는 데이터의 종류를 설명 합니다. 이러한 데이터 로그, 오류 메시지 및 시스템 정보를 포함합니다.

문서에서 설명 하는 가장 유용한 정보의 소스 진단 자가 진단 단위로 수행 하는 경우. SQL Server 컴퓨터 학습 기능과 관련 된 문제에 대 한 기술 지원을 요청 하는 경우이 정보를 수집 하는 유용 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스 (예: R 및 Python)

## <a name="sql-server-and-r-versions"></a>R 및 SQL Server 버전

새로 설치 또는 업그레이드 된 버전 인지 note 합니다. 업그레이드 하는 경우 수행 된 방식을 결정 합니다.

- 버전에서 업그레이드 했습니까? 
- 이전 구성 요소를 제거 하면 또는 준비에서를 업그레이드 했습니까?
- 업그레이드 하는 동안 모든 기능 선택을 변경할? 

### <a name="which-edition-of-sql-server-is-installed-and-which-version"></a>어떤 버전의 SQL Server가 설치 되어 있으므로 버전? 

SQL Server R Services는 SQL Server 2016에 도입 되었습니다. 이전 버전에서 기계 학습을 지원 하지 않습니다. 또한 많은 버그 수정 및 개선 2016 릴리스에 대 한 후속 서비스 팩 포함 되어 있습니다. 첫 번째 단계로, 서비스 팩 1 이상을 설치 해야 합니다.

SQL Server 2017는 Python 언어 지원이 확장 됩니다. 이전 릴리스에서 Python에 대 한 지원이 제공 되지 않았습니다.

에디션 및 버전을 확인 하는 데 도움이 필요한 경우 각에 대 한 빌드 번호를 나열 하는이 문서를 참조 하십시오.는 [SQL Server 버전](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)합니다.

사용 중인 SQL Server의 버전에 따라 기능을 익히는 일부 컴퓨터에 사용할 수 없는 경우 또는 제한 된 수 있습니다.

Enterprise, Developer, Standard 및 Express edition 시스템 학습 기능 목록은 다음 항목을 참조 하십시오.

* [버전 및 SQL Server의 지원 되는 기능](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [R 기능에 SQL Server의 버전 차이](https://docs.microsoft.com/sql/advanced-analytics/r/differences-in-r-features-between-editions-of-sql-server)

### <a name="which-version-of-microsoft-r-is-installed"></a>어떤 버전의 Microsoft R 설치 되어 있습니까?

일반적으로 컴퓨터 학습 서비스 기능을 사용 하거나 R 서비스 기능을 선택 하면 설치 된 Microsoft R 버전의 SQL Server 빌드 번호에 의해 결정 됩니다. 업그레이드 하거나 SQL Server 패치를 업그레이드 해야 하거나 그 R 구성 요소를 패치 해야 합니다.

참조를 해제 하 고 R 구성 요소 다운로드 링크입니다. 목록은, [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소를 설치](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)합니다. 인터넷에 연결 된 컴퓨터에서 필요한 버전의 R 파악 하 고 자동으로 설치 합니다.

바인딩 라고 하는 프로세스에서 SQL Server 데이터베이스 엔진에서 R 서버 구성 요소를 개별적으로 업그레이드할 수는 있습니다. 따라서 SQL Server에서 R 코드를 실행할 때 사용 하는 R의 버전 설치 된 버전의 SQL Server 및 최신 R 버전으로 서버를 마이그레이션 되었는지 여부에 따라 다를 수 있습니다.

#### <a name="determine-the-r-version"></a>R 버전 확인

R 버전을 확인 하는 가장 쉬운 방법은 다음과 같은 문을 실행 하 여 런타임 속성을 가져올 수는 있습니다.

```SQL
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
> R Services 작동 하지 않는 경우 관리자 권한에서 R 스크립트 부분을 실행 해 봅니다.

마지막 수단으로 설치 된 버전을 확인 하는 서버에서 파일을 열 수 있습니다. 이 위해 R 런타임 및 현재 작업 디렉터리의 위치를 가져오려면 rlauncher.config 파일을 찾습니다. 확인 파일의 복사본을 열어 속성을 실수로 변경 하지 않으면 되도록 하는 것이 좋습니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

R 버전 및 RevoScaleR 버전을 가져오려면 R 명령 프롬프트를 또는 인스턴스와 연결 된 관리자 권한을 엽니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`


R 콘솔에는 시작 시에 버전 정보가 표시 됩니다. 예를 들어 다음 버전 SQL Server 2017 CTP 2.0에 대 한 기본 구성을 나타냅니다.

    *Microsoft R Open 3.3.3*
    
    *The enhanced R distribution from Microsoft*
    
    *Microsoft packages Copyright (C) 2017 Microsoft*
    
    *Loading Microsoft R Server packages, version 9.1.0.*


### <a name="what-version-of-python-is-installed"></a>Python 버전 설치 되어 있습니까?

Python에 대 한 지원은 SQL Server 2017 Community Technology Preview (CTP) 2.0 에서만 사용할 수 이상 합니다.

여러 가지 방법으로 Python 버전을 가져올 수 있습니다. Management Studio 또는 다른 SQL 쿼리 도구에서이 문을 실행 하는 가장 쉬운 방법은:

```SQL
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

컴퓨터 학습 서비스를 실행 하지 않는 경우 pythonlauncher.config 파일 확인 하 여 설치 된 Python 버전을 확인할 수 있습니다. 확인 파일의 복사본을 열어 속성을 실수로 변경 하지 않으면 되도록 하는 것이 좋습니다.

1. SQL server 2017만:`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config `
2. 값을 가져오려면 **PYTHONHOME**합니다.
3. 현재 작업 디렉터리의 값을 가져옵니다.


> [!NOTE]
> SQL Server 2017에 Python과 R을 모두 설치한 경우 R 및 Python 언어에 대 한 작업 디렉터리와 풀의 작업자 계정 공유 됩니다.

### <a name="are-multiple-instances-of-r-or-python-installed"></a>R의 여러 인스턴스 또는 Python 설치?

R 라이브러리의 복사본을 여러 개 컴퓨터에 설치 되어 있는지를 확인 합니다. 이러한 중복 하는 경우에 발생할 수 있습니다.

* 설치 하는 동안 R Services (In-database)와 R Server (독립 실행형)를 선택합니다. 
* SQL Server 외에도 Microsoft R 클라이언트를 설치 합니다.
* 다양 한 R 라이브러리 Visual Studio, R Studio, Microsoft R 클라이언트 또는 다른 R IDE에 대 한 R 도구를 사용 하 여 설치 되었습니다.
* SQL Server의 여러 인스턴스를 호스팅하는 컴퓨터 및 기계 학습을 사용 하 여 둘 이상의 인스턴스.

Python에는 같은 조건이 적용 됩니다.

여러 라이브러리 또는 런타임을 설치 되어 있는지를 찾을 관련 된 SQL Server 인스턴스에서 사용 되는 Python 또는 R 런타임 오류만 인지 확인 합니다.

## <a name="errors-and-messages"></a>오류 및 메시지

R 코드를 실행 하려고 할 때 표시 되는 오류는 다음 중 하나에서 발생할 수 있습니다.

- 저장된 프로시저 sp_execute_external_script를 포함 하 여 SQL Server 데이터베이스 엔진
- SQL Server 실행 패드를 신뢰할 수 있는 
- R 및 Python 아이콘 등 위성 프로세스는 확장성 프레임 워크의 다른 구성 요소
- Microsoft Open 같은 공급자 데이터베이스 연결이 (ODBC)
- R 언어

처음으로 서비스를 사용 하는 경우에 메시지 서비스에서 시작 하기가 어려울 수 있습니다. 정확한 메시지 텍스트 뿐 아니라를 언급 했 듯이 메시지 컨텍스트를 캡처할 것이 좋습니다. 시스템 학습 코드를 실행 하는 데 사용 하는 클라이언트 소프트웨어를 note:

- Management Studio 사용 중 인가요? 외부 프로그램?
- 저장된 프로시저에서 직접 또는 원격 클라이언트에서 R 코드를 실행 하 시겠습니까?

### <a name="what-errors-has-sql-server-logged"></a>SQL Server에서 오류를 로깅에?

최신 SQL Server 오류 로그를 가져옵니다. 다음 기본 로그 디렉터리에서 파일의 전체 집합의 오류 로그 구성 됩니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE] 
> 정확한 폴더 이름을 인스턴스 이름에 따라 달라 집니다.


### <a name="what-errors-were-returned-by-the-spexecuteexternalscript-command"></a>어떤 오류가 sp_execute_external_script 명령에서 반환 된?

Sp_execute_external_script 명령을 실행할 때 반환 되는 오류의 전체 텍스트를 있는 경우 가져옵니다. 

Python 또는 R 문제를 고려 대상에서 제거 하려면 Python 또는 R 런타임을 시작 하 고 간에 데이터를 전달 하는이 스크립트를 실행할 수 있습니다.

**R에 대 한**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Python에 대 한**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

### <a name="what-errors-are-generated-by-the-extensibility-framework"></a>어떤 오류가 extensibility framework에서 생성 됩니다.

SQL Server 외부 스크립트 언어 런타임에 대 한 별도 로그를 생성합니다. 이러한 오류는 Python 또는 R 언어에서 생성 되지 않습니다. SQL server에서는 언어별로 표시 아이콘 및 해당 위성 프로세스를 포함 하 여 확장성 구성 요소에서 생성 하는 합니다.

다음 기본 사이트에서 이러한 로그를 얻을 수 있습니다.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog `

> [!NOTE] 
> 정확한 폴더 이름을 인스턴스 이름에 따라 다릅니다. 구성에 따라 폴더는 다른 드라이브에 있을 수 있습니다.

예를 들어 다음 로그 메시지에는 확장 프레임 워크를 관련이 있습니다.

* *MSSQLSERVER01 사용자에 대 한 LogonUser가 실패 했습니다*
  
  인스턴스는 외부 스크립트를 실행 하는 작업자 계정에 액세스할 수 있다는 의미일 수 있습니다.

* *InitializePhysicalUsersPool 실패* 
  
  이 메시지는 현재 보안 설정으로 인해 하지 않음을 설치 외부 스크립트를 실행 하는 데 필요한 작업자 계정 풀을 만들지 못하게 될 수도 있습니다.

* *보안 컨텍스트 관리자 초기화 하지 못했습니다.* 

* *위성 세션 관리자가 초기화 하지 못했습니다.*

### <a name="are-there-any-related-system-events"></a>관련된 시스템 이벤트 있습니까?

1. Windows 이벤트 뷰어를 열고 검색는 **시스템 이벤트** 문자열이 포함 된 메시지에 대 한 로그 *실행 패드*합니다. 
2. 문자열에 대해 확인 하 고 ExtLaunchErrorlog 파일을 열고 *ErrorCode*합니다. 오류 코드와 관련 된 메시지를 검토 합니다.

예를 들어 다음 메시지는 SQL Server 확장 프레임 워크 관련 된 일반적인 시스템 오류: 

* *SQL Server 실행 패드 (MSSQLSERVER) 서비스가 다음 오류로 인해 시작 하지 못했습니다.<text>*

* *서비스가 적시에 시작 또는 제어 요청에 응답 하지 않았습니다.* 

* *시간 초과 연결 하려면 SQL Server 실행 패드 (MSSQLSERVER) 서비스에 대 한 대기 하는 동안 (120000 밀리초)에 도달 했습니다.* 

### <a name="did-any-components-start-and-then-crash"></a>모든 구성 요소 시작 하 고 크래시가?

디버깅에 대 한 지식이 인 경우에 실행 패드에서 실패를 분석 하려면 덤프 파일을 사용할 수 있습니다.

1. SQL Server에 대 한 설치 부트스트랩 로그가 들어 있는 폴더를 찾습니다. 예를 들어 SQL Server 2016의 기본 경로 C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log를 했습니다.
2. 확장성에만 적용 되는 부트스트랩 로그 하위 폴더를 엽니다.
3. 지원 요청을 제출 해야 하는 경우이 폴더의 전체 내용을 압축 된 파일에 추가 합니다. 예를 들어, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog 합니다.
  
시스템에서 정확한 위치는 다를 수 있습니다 하 고 C 드라이브 이외의 드라이브에 있을 수 있습니다. 기계 학습이 설치 된 인스턴스에 대 한 로그를 가져올 해야 합니다. 


## <a name="related-tools-and-configuration"></a>관련된 도구 및 구성

이 섹션에는 추가 구성 요소 또는 Python 또는 R 스크립트를 실행할 때 오류 소스 일 수 있는 공급자 나열 합니다.

### <a name="what-network-protocols-are-available"></a>네트워크 프로토콜을 사용할 수 있습니까?

컴퓨터 학습 서비스 확장성 구성 요소 간의 내부 통신에 대 한 및 R 또는 Python에 대 한 외부 클라이언트와의 통신에는 다음 네트워크 프로토콜 필요합니다.

* 명명된 파이프
* TCP/IP

지 확인 하는 프로토콜을 설치, 설치 되어 있는 경우, 사용할 수 있는지 여부를 확인 하려면 SQL Server 구성 관리자를 엽니다.

### <a name="security-configuration-and-permissions"></a>보안 구성 및 사용 권한

작업자 계정:

1. 제어판을 열고 **사용자 및 그룹**, 외부 스크립트 작업을 실행 하는 데 사용 되는 그룹을 찾습니다. 기본적으로 그룹은 **SQLRUserGroup**합니다.
2. 하나 이상의 작업자 계정을 포함 하 고 그룹이 있는지 확인 합니다.
3. SQL Server Management Studio에서 Python 또는 R 작업 실행 될 인스턴스를 선택 합니다. 선택 **보안**, 고 SQLRUserGroup에 대 한 로그온 있는지 여부를 결정 합니다.
4. 사용자 그룹에 대 한 권한을 검토 합니다.

개별 사용자 계정:

1. 인스턴스가 혼합 모드 인증, SQL 로그인만, 또는 Windows 인증만 지원 하는지 여부를 결정 합니다. 이 설정은 적용 R 또는 Python 코드 요구 사항입니다.
2. R 코드를 실행 해야 하는 각 사용자에 대해 필요한 수준의 있는 R에서 개체를 쓸, 데이터가 액세스 되는, 또는 개체가 생성 됩니다. 각 데이터베이스에 대 한 권한 확인 합니다.
3. 스크립트 실행을 사용 하려면 역할을 만들 하거나 필요에 따라 다음 역할에 사용자를 추가 합니다.

   - 제외 하 고 모두 *db_owner*: ANY EXTERNAL SCRIPT를 실행 해야 합니다.
   - *db_datawriter*: R, Python에서 결과 쓸 수 있습니다. 
   - *db_ddladmin*: 새 개체를 만들 수 있습니다. 
   - *db_datareader*: R, Python 코드에서 사용 되는 데이터를 읽을 수 있습니다. 
4. SQL Server 2016을 설치 했을 때 모든 기본 시작 계정에 변경 여부 note 합니다.
5. 사용자를 새 R 패키지를 설치 하거나 다른 사용자가 설치 된 R 패키지를 사용 하는 경우 인스턴스에서 패키지 관리를 사용 하도록 설정 하 고 다음 추가 사용 권한을 할당 하려면 할 수 있습니다. 자세한 내용은 참조 [사용 하거나 R 패키지 관리를 사용 하지 않도록](r\r-package-how-to-enable-or-disable.md)합니다.

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>폴더는 바이러스 백신 소프트웨어로 잠금 영향을 받습니다.

바이러스 백신 소프트웨어에 기계 학습 기능 및 성공적인 스크립트 실행의 설치를 방지 하는 폴더를 잠글 수 있습니다. SQL Server 트리에 있는 모든 폴더 바이러스 검사 적용 되는지 여부를 결정 합니다.

그러나 인스턴스에서 여러 서비스 또는 기능이 설치 되 면 인스턴스가 사용 되는 모든 가능한 폴더를 열거할 어려울 수 있습니다. 예를 들어 새 기능을 추가 하는 경우 새 폴더 여야 식별 하며 제외 합니다.

또한, 일부 기능은 새 폴더를 만들고 동적으로 런타임에 합니다. 예를 들어 메모리 내 OLTP 테이블, 저장된 프로시저 및 함수 모든 런타임 시이 디렉터리를 새로 만듭니다. 이 폴더 이름은 종종 Guid가 포함 하 고 예측할 수 없습니다. SQL Server 신뢰할 수 있는 실행 패드 R에 대 한 새 작업 디렉터리 만들고 Python 스크립트 작업 합니다.

SQL Server 프로세스와 해당 기능에 필요한 모든 폴더를 제외 하려고 하지 못할 수도 있습니다, 때문에 전체 SQL Server 인스턴스 디렉터리 트리를 제외 하는 것이 좋습니다.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>SQL Server에 대 한 열기 방화벽은? 인스턴스가 원격 연결을 지원 합니까?

1. 참조를 SQL Server 원격 연결을 지원 하는지 여부를 확인 하려면 [원격 서버 연결을 구성할](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)합니다.

2. SQL Server에 대 한 방화벽 규칙을 만들어졌는지 여부를 결정 합니다. 보안상의 이유로 기본 설치에 해당 하지 못할 수도 있습니다는 인스턴스에 연결 하려면 원격 R, Python 클라이언트에 대 한 합니다. 자세한 내용은 참조 [SQL Server에 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)합니다.

### <a name="can-you-run-r-script-outside-t-sql"></a>T-SQL 외부 R 스크립트를 실행할 수 있습니까?

기타 R 도구를 사용 하 여 SQL Server 인스턴스와 연결 된 R 런타임 실행을 시도할 수 있습니다. 이런 방식으로 필요한 라이브러리가 설치 되어 있는지 여부를 확인할 수 있습니다.

R의 기본 설치에는 스크립트의 대화형 실행에 대 한 관리자 권한 뿐만 아니라 명령줄에서 R 스크립트를 실행 하는 데 사용할 수 있는 여러 도구가 포함 되어 있습니다.

R 런타임 작동 하는 경우 오류를 반환 하는 스크립트는 전용된 등의 R 개발 환경 R Tools for Visual Studio에서에서 스크립트를 디버깅 하려고 하는 것이 좋습니다.

검토 하 고 약간 R과 데이터베이스 엔진 간에 데이터를 이동할 때 발생할 수 있는 데이터 형식 문제를 해결 하는 스크립트를 다시 작성 하는 것이 좋습니다. 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

또한 R 스크립트를 보다 쉽게 저장 프로시저로 사용 되는 형식으로 번들로 묶는 sqlrutils 패키지를 사용할 수 있습니다. 참조 항목:
* [Sqlrutils 패키지를 사용 하 여 R 코드에 대 한 저장된 프로시저를 생성 합니다.](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [Sqlrutils를 사용 하 여 저장된 프로시저 만들기](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="see-also"></a>참고 항목

[SQL Server의 기계 학습 문제 해결](machine-learning-troubleshooting-faq.md)
