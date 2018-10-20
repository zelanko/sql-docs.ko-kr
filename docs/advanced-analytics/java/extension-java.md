---
title: SQL Server 2019에 Java 언어 확장 | Microsoft Docs
description: Java 언어 확장을 사용 하 여 SQL Server 2019에서 Java 코드를 실행 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/12/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2d69a255c56c3b15051a393b74eb1492a4f830f4
ms.sourcegitcommit: 93e3bb8941411b808e00daa31121367e96fdfda1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49359340"
---
# <a name="java-language-extension-in-sql-server-2019"></a>SQL Server 2019에 Java 언어 확장 

SQL Server 2019 년부터 하면 사용자 지정 Java 코드를 실행할 수는 [확장성 프레임 워크](../concepts/extensibility-framework.md) 데이터베이스 엔진 인스턴스를 추가 합니다. 

확장성 프레임 워크는 외부 코드를 실행 하는 것에 대 한 아키텍처: Java (SQL Server 2019에서 시작) [Python (SQL Server 2017부터)](../concepts/extension-python.md), 및 [(SQL Server 2016부터) R](../concepts/extension-r.md)합니다. 코드 실행 핵심 엔진 프로세스에서 분리 되었지만 SQL Server 쿼리 실행을 사용 하 여 완벽 하 게 통합 됩니다. 즉, 수를 외부 런타임에 모든 SQL Server 쿼리에서 데이터를 푸시 및 사용 하거나 SQL Server에 다시 결과 유지 합니다.

모든 프로그래밍 언어 확장을 마찬가지로 시스템 저장 프로시저 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 미리 컴파일된 Java 코드를 실행 하기 위한 인터페이스입니다.

## <a name="prerequisites"></a>필수 구성 요소

SQL Server 2019가 필요 합니다. 이전 버전 Java 통합이 필요는 없습니다. 

Windows 및 Linux에서 Java 버전 요구 사항이 달라 집니다. Java Runtime Environment (JRE)의 최소 요구 사항 이지만 Jdk는 Java 컴파일러 또는 개발 패키지를 해야 하는 경우에 유용 합니다. JDK 포괄적 이며 JDK를 설치 하는 경우 이므로 JRE 필요 하지 않습니다.

| 운영 체제 | Java 버전 | JRE 다운로드 | JDK 다운로드 |
|------------------|--------------|--------------|--------------|
| Windows          | 1.10         | [JRE 10](http://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) | [JDK 10](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)  |
| Linux            | 1.8          |  [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) | [JDK 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  |  

Linux에서 **mssql server-확장성 java** 이미 설치 되어 있지 않으면 자동으로 패키지 JRE 1.8 설치 합니다. 설치 스크립트는 또한 라는 JAVA_HOME 환경 변수를 JVM 경로 추가 합니다.

Windows, 좋습니다 기본/program 파일에서 JDK를 설치 / 폴더를 가능한 경우. 그렇지 않은 경우 실행 파일에 권한을 부여 하려면 추가 구성 필요 합니다. 자세한 내용은 참조는 [(Windows) 권한을 부여](#perms-nonwindows) 이 문서의 섹션입니다.

> [!Note]
> Java는 이전 버전과 호환, 이전 버전에서 작동 하지만이 초기 CTP 릴리스에 지원 되는 버전과 테스트 테이블에 나열 됩니다 지정 합니다.

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>Linux에 설치

설치할 수는 [함께 데이터베이스 엔진 및 Java 확장](../../linux/sql-server-linux-setup-machine-learning.md#chained-installation), 또는 Java 지원 기존 인스턴스에 추가 합니다. 다음 예제에서는 기존 설치에 Java 확장을 추가합니다.  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility-java
```

설치 하는 경우 **mssql server-확장성 java**를 이미 설치 되어 있지 않으면 패키지가 JRE 1.8을 자동으로 설치 합니다. 또한 JVM 경로 JAVA_HOME 라는 환경 변수에 추가 됩니다.

설치를 완료 한 후에 다음 단계로 [외부 스크립트 실행 구성](#configure-script-execution)합니다.

> [!Note]
> 인터넷에 연결 된 장치에서 패키지 종속성 다운로드 되 고 주 패키지 설치의 일부로 설치 합니다. 오프 라인 설치를 비롯 한 자세한 정보를 참조 하세요 [Linux에서 SQL Server Machine Learning 설치](../../linux/sql-server-linux-setup-machine-learning.md)합니다.

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>Windows에 설치

1. [설치 프로그램을 실행](../install/sql-machine-learning-services-windows-install.md) SQL Server 2019를 설치 합니다.

2. 기능 선택에 도달 하면 선택할 **Machine Learning 서비스 (데이터베이스 내)** 합니다. 

   Java 통합 기계 학습 라이브러리가 함께 제공 되지 않습니다, 하지만 확장성 프레임 워크를 제공 하는 설치 옵션입니다. 원하는 경우 R 및 Python을 생략할 수 있습니다.

3. 설치 마법사를 완료 하 고 후 다음 두 태스크를 계속 합니다.

### <a name="add-the-javahome-variable"></a>JAVA_HOME 변수를 추가 합니다.

JAVA_HOME 환경 변수가 Java 인터프리터의 위치를 지정 하 합니다. 이 단계에서는 Windows에서에 대 한 시스템 환경 변수를 만듭니다.

1. 찾아 JDK/JRE 설치 경로 (예: C:\Program Files\Java\jdk-10.0.2)를 복사 합니다.

  CTP 2.0에서 1.10 Java 용 에서만 기본 jdk 폴더로 JAVA_HOME을 설정 합니다. 

  Java 1.8에 대 한 확장 (예: "C:\Program Files\Java\jdk1.8.0_181\bin\server" JDK의 Windows에서 jvm.dll 연결할 경로. 또는 JRE 기본 폴더를 가리킬 수 있습니다: "C:\Program Files\Java\jre1.8.0_181"입니다.

2. 제어판에서 엽니다 **시스템 및 보안**오픈 **시스템**, 클릭 **고급 시스템 속성**합니다.

3. 클릭 **환경 변수**합니다.

4. JAVA_HOME에 대 한 새 시스템 변수를 만듭니다.

   ![Java 홈에 대 한 환경 변수](../media/java/env-variable-java-home.png "Java에 대 한 설정")

<a name="perms-nonwindows"></a>

### <a name="grant-permissions-to-java-executables"></a>Java 실행 파일에 권한 부여

기본적으로 외부 프로세스를 실행 하는 계정 JRE 또는 JDK 파일에 액세스를 하지 않습니다. 이 섹션에서는 액세스할 수 있도록 권한을 부여 하려면 다음 PowerShell 스크립트를 실행 합니다.

1. 찾아 JDK 또는 JRE 설치 위치를 복사 합니다. 예를 들어, C:\Program Files\Java\jdk-10.0.2 수 있습니다.

2. 관리자 권한으로 PowerShell을 엽니다. 이 작업에 익숙하지 참조 [이 문서에서는](https://www.top-password.com/blog/5-ways-to-run-powershell-as-administrator-in-windows-10/) 팁에 대 한 합니다.

3. 권한을 부여 하려면 다음 스크립트를 실행 **SQLRUserGroup** Java 실행 파일에 대 한 사용 권한. 

  **SQLRUserGroup** 실행 하는 외부 프로세스에서 사용 권한을 지정 합니다. 기본적으로이 그룹의 구성원 권한이 R 및 Python 프로그램 파일에서 SQL Server, 없습니다 Java 설치 합니다. Java 실행 파일을 실행 하려면 기울여야 **SQLRUserGroup** 권한이 있습니다.

   ```powershell
   $Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>"
   $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("SQLRUsergroup","FullControl","Allow")
   $Acl.SetAccessRule($Ar)
   Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
   ```
4. 권한을 부여 하려면 다음 스크립트를 실행 **ALL APPLICATION PACKAGES** 사용 권한도 있습니다. 

  SQL Server 2019 컨테이너 바꿉니다 작업자 계정을 격리 메커니즘으로 멤버는 실행 패드 서비스 계정의 id 아래에 있는 컨테이너 내에서 실행 되는 프로세스를 **SQLRUserGroup**합니다. 자세한 내용은 [SQL Server 2019에 차이가 설치](../install/sql-machine-learning-services-ver15.md)합니다.

   ```powershell
   $Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>" 
   $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("ALL APPLICATION PACKAGES","FullControl","Allow") 
   $Acl.SetAccessRule($Ar) 
   Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
   ```

5. SQL Server에서 실행 하려는.class 또는.jar 파일이 포함 된 모든 Java 클래스 경로 폴더에서 이전 두 단계를 반복 합니다. C:\JavaPrograms\my-app와 같은 경로에서 컴파일된 프로그램을 유지 하는 경우 부여 하는 예를 들어 **SQLRUserGroup** 하 고 **ALL APPLICATION PACKAGES** 폴더에 대 한 권한이 프로그램을 로드할 수 있도록 합니다.

  루트 폴더에서 시작 하는 전체 경로 대 한 권한을 부여 해야 합니다. 만 하 고 있는 폴더에 대 한 권한 코드를 로드 하기 위한 충분 한 수 없습니다.

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>스크립트 실행 구성

이 시점에서 거의 Linux 또는 Windows에서 Java 코드를 실행할 수 있습니다. 마지막 단계에서는 SQL Server Management Studio 또는 외부 스크립트 실행을 사용 하도록 설정 하는 TRANSACT-SQL 스크립트를 실행 하는 다른 도구를 전환 합니다.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>설치 확인

설치가 작동 확인, 만들기 및 실행을 [샘플 응용 프로그램](java-first-sample.md) 방금 설치한, 이전에 구성한 클래스 경로에서 파일을 배치 하는 JDK를 사용 하 여 합니다.

## <a name="differences-in-ctp-20"></a>CTP 2.0의 차이점

Machine Learning Services에 익숙한 경우 확장에 대 한 권한 부여 및 격리 모델은이 릴리스에서 변경 되었습니다. 자세한 내용은 [SQL Server Machine Learning Services 2019 설치에서 차이점](../install/sql-machine-learning-services-ver15.md)합니다.

## <a name="limitations-in-ctp-20"></a>CTP 2.0의에서 제한 사항

* 입력 및 출력 버퍼에 있는 값의 수를 초과할 수 없습니다 `MAX_INT (2^31-1)` Java 배열에서 할당 될 수 있는 요소의 최대 개수 이기 때문입니다.

* 출력에서 매개 변수 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 이 버전에서 지원 되지 않습니다.

* 이 버전에서는 입력 및 출력 데이터 집합에 대 한 LOB 데이터 형식이 지원 되지 않습니다. 참조 [Java와 SQL Server 데이터 형식](java-sql-datatypes.md) 형식이이 CTP에 지원 되는 데이터에 대 한 세부 정보에 대 한 합니다.

* Sp_execute_external_script 매개 변수를 사용 하 여 스트리밍 @r_rowsPerRead 이 CTP에서 지원 되지 않습니다.

* Sp_execute_external_script 매개 변수를 사용 하 여 분할 @input_data_1_partition_by_columns 이 CTP에서 지원 되지 않습니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java를 호출 하는 방법](howto-call-java-from-sql.md)
+ [SQL Server에서 Java 샘플](java-first-sample.md)
+ [Java와 SQL Server 데이터 형식](java-sql-datatypes.md)