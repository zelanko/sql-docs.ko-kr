---
title: SQL Server 2019-SQL Server 언어 확장에에서 Java 언어 확장
description: 설치, 구성 및 Linux와 Windows 시스템에 대 한 SQL Server 2019에 Java 언어 확장의 유효성을 검사 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: db57689227445b0f50d6ff59fbf81e1d84ecacdb
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775495"
---
# <a name="java-language-extension-in-sql-server-2019"></a>SQL Server 2019에 Java 언어 확장 

Windows와 Linux 모두에서 SQL Server 2019 preview부터 실행할 수 있습니다 사용 하 여 사용자 지정 Java 코드를 [확장성 프레임 워크](../concepts/extensibility-framework.md) 데이터베이스 엔진 인스턴스를 추가 합니다.

확장성 프레임 워크는 외부 코드를 실행 하는 것에 대 한 아키텍처: Java (SQL Server 2019에서 시작) [Python (SQL Server 2017부터)](../concepts/extension-python.md), 및 [(SQL Server 2016부터) R](../concepts/extension-r.md)합니다. 코드 실행 핵심 엔진 프로세스에서 분리 되었지만 SQL Server 쿼리 실행을 사용 하 여 완벽 하 게 통합 됩니다. 이 의미는 외부 런타임 (Java)를 모든 SQL Server 쿼리에서 데이터를 푸시 및 사용 하거나 SQL Server에 다시 결과 유지 합니다.

모든 프로그래밍 언어 확장을 마찬가지로 시스템 저장 프로시저 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 미리 컴파일된 Java 코드를 실행 하기 위한 인터페이스입니다.

<a name="prerequisites"></a>

## <a name="prerequisites"></a>사전 요구 사항

SQL Server 2019 미리 보기 인스턴스가 필요한 경우 이전 버전의 Java 통합이 필요는 없습니다.

Java 8이 현재 지원 되는 버전입니다. 11, Java 등의 최신 버전에서 언어 확장을 사용 하 여 되어야 하지만 현재 지원 되지 않습니다. Java Runtime Environment (JRE)의 최소 요구 사항 이지만 JDK는 Java 컴파일러 및 개발 패키지 해야 하는 경우에 유용 합니다. JDK 포괄적 이며 JDK를 설치 하는 경우 이므로 JRE 필요 하지 않습니다.

기본 Java 8 배포를 사용할 수 있습니다. 두 개의 제안 된 배포는 다음과 같습니다.

| 배포 | Java 버전 | 운영 체제 | JDK | JRE |
|-|-|-|-|-|
| [Oracle Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) | 8 | Windows 및 Linux | 사용자 계정 컨트롤 | 사용자 계정 컨트롤 |
| [Zulu OpenJDK](https://www.azul.com/downloads/zulu/) | 8 | Windows 및 Linux | 사용자 계정 컨트롤 | 아니요 |

Linux에서 현재 합니다 **mssql server-확장성 java** 이미 설치 되어 있지 않으면 패키지 JRE 8을 자동으로 설치 합니다. 설치 스크립트는 또한 JRE_HOME 이라는 환경 변수를 JVM 경로 추가 합니다.

Windows, 좋습니다 기본 JDK 설치 `/Program Files/` 폴더 가능한 경우. 그렇지 않은 경우 실행 파일에 권한을 부여 하려면 추가 구성 필요 합니다. 자세한 내용은 참조는 [(Windows) 권한을 부여](#perms-nonwindows) 이 문서의 섹션입니다.

> [!Note]
> Java 이전 버전과 호환 되는 이전 버전에서 작동 하지만이 초기 CTP 릴리스에 지원 되는 테스트를 거친 버전은 Java 8을 지정 합니다. 

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>Linux에 설치

설치할 수는 [함께 데이터베이스 엔진 및 Java 확장](../../linux/sql-server-linux-setup-machine-learning.md#install-all), 또는 Java 지원 기존 인스턴스에 추가 합니다. 다음 예제에서는 기존 설치에 Java 확장을 추가합니다.  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# SUSE install commands
sudo zypper install mssql-server-extensibility-java
```

설치 하는 경우 **mssql server-확장성 java**를 이미 설치 되어 있지 않으면 패키지가 JRE 8을 자동으로 설치 합니다. 또한 JVM 경로 JRE_HOME 라는 환경 변수에 추가 됩니다.

설치를 완료 한 후에 다음 단계로 [외부 스크립트 실행 구성](#configure-script-execution)합니다.

> [!Note]
> 인터넷에 연결 된 장치에서 패키지 종속성 다운로드 되 고 주 패키지 설치의 일부로 설치 합니다. 오프 라인 설치를 비롯 한 자세한 정보를 참조 하세요 [Linux에서 SQL Server Machine Learning 설치](../../linux/sql-server-linux-setup-machine-learning.md)합니다.

### <a name="grant-permissions-on-linux"></a>Linux에 대 한 권한 부여

외부 라이브러리를 사용 하는 경우이 단계를 수행할 필요가 없습니다. 작업 하는 권장된 방법을 외부 라이브러리를 사용 합니다. Jar 파일에서 외부 라이브러리를 만드는 데 도움이 필요한 경우 참조 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

외부 라이브러리를 사용 하지 않는 경우에 jar에서 Java 클래스를 실행 하는 권한이 있는 SQL Server를 제공 해야 합니다.

읽기 권한을 부여 하 고 jar 파일에 대 한 액세스를 실행 하려면 다음을 실행 **chmod** jar 파일에서 명령을 합니다. 항상 SQL Server를 사용 하 여 작업할 때 jar의 클래스 파일을 배치 하는 것이 좋습니다. Jar 만들기 도움말을 참조 하세요 [jar 파일을 만드는 방법](#create-jar)합니다.

```cmd
chmod ug+rx <MyJarFile.jar>
```

Jar 파일을 읽기/실행 mssql_satellite 권한을 부여 해야 합니다.

```cmd
chown mssql_satellite:mssql_satellite <MyJarFile.jar>
```

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>Windows에 설치

1. 지원 되는 Java 버전이 설치 되어 있는지 확인 합니다. 자세한 내용은 참조는 [필수 구성 요소](#prerequisites)합니다.

2. [설치 프로그램을 실행](../install/sql-machine-learning-services-windows-install.md) SQL Server 2019를 설치 합니다.

3. 기능 선택에 도달 하면 선택할 **Machine Learning 서비스 (데이터베이스 내)** 합니다. 

   Java 통합 기계 학습 라이브러리가 함께 제공 되지 않습니다, 하지만 확장성 프레임 워크를 제공 하는 설치 옵션입니다. 원하는 경우 R 및 Python을 생략할 수 있습니다.

4. 설치 마법사를 완료 하 고 후 다음 두 태스크를 계속 합니다.

### <a name="add-the-jrehome-variable"></a>JRE_HOME 변수 추가

JRE_HOME는 Java 인터프리터의 위치를 지정 하는 시스템 환경 변수입니다. 이 단계에서는 Windows에서에 대 한 시스템 환경 변수를 만듭니다.

1. 찾기 및 JRE 홈 경로 복사 (예를 들어 `C:\Program Files\Zulu\zulu-8\jre\`).

    기본 Java 배포에 따라 JDK를 JRE의 위치는 위의 예를 들어 경로 보다 달라질 수 있습니다.
    설치 된 JDK가 있는 경우에 종종 시간 JRE 하위 폴더는 설치의 일부로 받은 하는 경우 jre 폴더를 가리키고 있으므로.
    Java 확장 된 jvm.dll JRE_HOME%\bin\server % 경로에서 로드 하려고 합니다.

2. 제어판에서 엽니다 **시스템 및 보안**오픈 **시스템**, 클릭 **고급 시스템 속성**합니다.

3. 클릭 **환경 변수**합니다.

4. 새 시스템 변수를 만들어야 `JRE_HOME` (1 단계에서 찾은) JDK/JRE 경로 값을 사용 하 여 합니다.

5. 다시 시작 [실행 패드](../concepts/extensibility-framework.md#launchpad)합니다.

    1. [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 엽니다.

    2. SQL Server 서비스에서 SQL Server 실행 패드를 마우스 오른쪽 단추로 클릭 하 고 선택 **다시 시작**합니다.

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jre-folder-windows-only"></a>기본이 아닌 JRE 폴더 (Windows만 해당)에 액세스 권한 부여

Program files 아래 JDK를 JRE를 설치 하지 않은 경우 다음 단계를 수행 해야 합니다. 실행 합니다 **icacls** 에서 명령을 *관리자 권한* 액세스 권한을 부여 하는 줄을 **SQLRUsergroup** 및 SQL Server 서비스 계정 (에서 **ALL_APPLICATION_ 패키지**) JRE에 액세스 합니다. 명령에는 모든 파일 및 지정 된 디렉터리 경로 아래에 폴더를 재귀적으로 액세스를 하는 권한 부여 됩니다.

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup 권한

명명 된 인스턴스의 경우 인스턴스 이름을 SQLRUsergroup에 추가 합니다 (예를 들어 `SQLRUsergroupINSTANCENAME`).

```cmd
icacls "<PATH to JRE>" /grant "SQLRUsergroup":(OI)(CI)RX /T
```

Windows에서 program files 아래 기본 폴더에 JDK/JRE를 설치 하는 경우이 단계를 건너뛸 수 있습니다.

#### <a name="appcontainer-permissions"></a>AppContainer 권한

```cmd
icacls "PATH to JRE" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
```

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>스크립트 실행 구성

이 시점에서 거의 Linux 또는 Windows에서 Java 코드를 실행할 수 있습니다. 마지막 단계에서는 SQL Server Management Studio, Azure data studio, SQL CMD 또는 외부 스크립트 실행을 사용 하도록 설정 하는 TRANSACT-SQL 스크립트를 실행할 수 있는 다른 도구를 전환 합니다.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>설치 확인

설치가 작동 확인, 만들기 및 실행을 [샘플 응용 프로그램](java-first-sample.md) 방금 설치 및 JRE_HOME 추가할 Java 런타임 사용 합니다.

## <a name="differences-in-ctp-25"></a>CTP 2.5의 차이점

Machine Learning Services에 익숙한 경우 확장에 대 한 권한 부여 및 격리 모델은이 릴리스에서 변경 되었습니다. 자세한 내용은 [SQL Server Machine Learning Services 2019 설치에서 차이점](../install/sql-machine-learning-services-ver15.md)합니다.

## <a name="limitations-in-ctp-25"></a>CTP 2.5의에서 제한 사항

* 입력 및 출력 버퍼에 있는 값의 수를 초과할 수 없습니다 `MAX_INT (2^31-1)` Java 배열에서 할당 될 수 있는 요소의 최대 개수 이기 때문입니다.

* 출력에서 매개 변수 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 이 버전에서 지원 되지 않습니다.

* Sp_execute_external_script 매개 변수를 사용 하 여 스트리밍 @r_rowsPerRead 이 CTP에서 지원 되지 않습니다.

* Sp_execute_external_script 매개 변수를 사용 하 여 분할 @input_data_1_partition_by_columns 이 CTP에서 지원 되지 않습니다.

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>클래스 파일에서 jar 파일을 만드는 방법

SQL Server에서 실행할 때 jar에 클래스 파일을 항상 패키징 하는 것이 좋습니다.
Jar에서 클래스 파일을 만들려면 클래스 파일을 포함 하는 폴더를 찾아이 명령을 실행 합니다.

```cmd
jar -cf <MyJar.jar> *.class
```

에 대 한 경로 확인 **jar.exe** 시스템 경로 변수에의 일부입니다. 또는 /bin JDK 폴더에서에서 찾을 수 있는 jar에 대 한 전체 경로 지정 합니다. `C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java를 호출 하는 방법](howto-call-java-from-sql.md)
+ [SQL Server에서 Java 샘플](java-first-sample.md)
+ [Microsoft 확장성 Microsoft SQL Server에 대 한 Java 용 SDK](java-sdk.md)
+ [Java와 SQL Server 데이터 형식](java-sql-datatypes.md)
