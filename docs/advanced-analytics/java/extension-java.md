---
title: SQL Server 2019에 Java 언어 확장 | Microsoft Docs
description: Java 언어 확장을 사용 하 여 SQL Server 2019에서 Java 코드를 실행 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8acb0a72435306cdec8740ffb41ff499eea61fac
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715156"
---
# <a name="java-language-extension-in-sql-server-2019"></a>SQL Server 2019에 Java 언어 확장 

SQL Server 2019 년부터 하면 사용자 지정 Java 코드를 실행할 수는 [확장성 프레임 워크](../concepts/extensibility-framework.md) 데이터베이스 엔진 인스턴스를 추가 합니다. 

확장성 프레임 워크는 외부 코드를 실행 하는 것에 대 한 아키텍처: Java (SQL Server 2019에서 시작) [Python (SQL Server 2017부터)](../concepts/extension-python.md), 및 [(SQL Server 2016부터) R](../concepts/extension-r.md)합니다. 코드 실행 핵심 엔진 프로세스에서 분리 되었지만 SQL Server 쿼리 실행을 사용 하 여 완벽 하 게 통합 됩니다. 즉, 수를 외부 런타임에 모든 SQL Server 쿼리에서 데이터를 푸시 및 사용 하거나 SQL Server에 다시 결과 유지 합니다.

모든 프로그래밍 언어 확장을 마찬가지로 시스템 저장 프로시저 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 미리 컴파일된 Java 코드를 실행 하기 위한 인터페이스입니다.

## <a name="1---feature-installation"></a>1-기능 설치

Java 언어 확장을 설치 하려면 Windows 또는 Linux에서 SQL Server 2019 설치 프로그램을 실행 합니다. SQL Server 2019 데이터베이스 엔진 인스턴스를 반드시 입력 해야 합니다. Java 통합 버전에 추가할 수 없습니다.

Windows를 시작 합니다 [설치 마법사](../install/sql-machine-learning-services-windows-install.md)합니다. 기능 선택에서 선택 **Machine Learning 서비스 (데이터베이스 내)** 합니다. Java 통합 기계 학습 라이브러리가 함께 제공 되지 않습니다, 하지만 확장성 프레임 워크를 제공 하는 설치 옵션입니다. 원하는 경우 R 및 Python을 생략할 수 있습니다.

Linux에서 설치 합니다 [데이터베이스 엔진](https://docs.microsoft.com/sql/linux/sql-server-linux-setup), 뿐만 [확장성 패키지 및 Java 확장 패키지](../../linux/sql-server-linux-setup-machine-learning.md)합니다.

다음 예제에서는 각 Linux 운영 체제에 대 한 구문을 보여 줍니다.

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility
sudo zypper install mssql-server-extensibility-java
```

## <a name="2---configuration"></a>2-구성

SQL Server Management Studio 또는 TRANSACT-SQL 스크립트를 실행 하는 다른 도구를 사용 하면 데이터베이스 엔진 인스턴스에서 외부 스크립트 실행을 구성할 합니다.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="3---bring-your-own-java"></a>3-사용자 고유의 Java를 제공 합니다.

R 및 Python과 같은 이전 언어 통합에서 한 가지 차이점은 제어 하는 SQL Server를 사용 하 여 JVM 사용 되는 합니다.

| Java 버전 | 운영 체제 |
|--------------|------------------|
| [1.10 Java](http://jdk.java.net/10/)   | Windows |
| Java 1.8   | Linux | 

Java는 이전 버전과 호환, 이전 버전에서 작동 하지만이 초기 CTP 릴리스에 지원 되는 버전과 테스트 테이블에 나열 됩니다 지정 합니다.

> [!Note]
>Java에서 SQL Server를 실행 하려면 기술적으로 해야 합니다 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) JRE ()를 설치 합니다. JDK가 개발 키트 Java 컴파일러 등 기타 개발 관련 패키지 있습니다. 개발 환경이 이미 있고 서버 컴퓨터에서 Java 런타임 하기만 하는 경우 JDK 설치 지침을 무시 하 고만 JRE를 설치할 수 있습니다.

## <a name="jdk-on-windows"></a>Windows에서 JDK

Windows 버전을 다운로드 합니다 [Java SE 개발 키트 (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)합니다.

기본/program 파일에서 JDK를 설치 / 폴더 권한을 부여할 필요가 없도록 하려면 읽기 권한이 **ALL APPLICATION PACKAGES** 하며 **SQLRUserGroup** 대체 위치에서 보안 그룹 . .Class 또는.jar 파일을 보관할 위치를 Java classpath 폴더 액세스에 대 한 동일한 지침에 적용 됩니다. 

> [!Note]
> 확장에 대 한 권한 부여 및 격리 모델은이 릴리스에서 변경 되었습니다. 자세한 내용은 [SQL Server Machine Learning Services 2019 설치에서 차이점](../install/sql-machine-learning-services-ver15.md)합니다.

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>기본이 아닌 JDK 폴더 (Windows만 해당)에 액세스 권한 부여

기본 폴더에 JDK/JRE를 설치 하는 경우이 단계를 건너뛸 수 있습니다. 설치 하는 기본이 아닌 폴더에 대 한 액세스 권한을 부여 하려면 다음 PowerShell 스크립트를 실행 합니다 **SQLRUsergroup** 및 JVM 및 Java classpath에 액세스 하기 위한 (ALL_APPLICATION_PACKAGES)에서 SQL Server 서비스 계정입니다.

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup 권한

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>"
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("SQLRUsergroup","FullControl","Allow")
$Acl.SetAccessRule($Ar)
Set-Acl ""<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

#### <a name="appcontainer-permissions"></a>AppContainer 권한

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>" 
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("ALL APPLICATION PACKAGES","FullControl","Allow") 
$Acl.SetAccessRule($Ar) 
Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

### <a name="add-the-jdk-path-to-javahome"></a>JAVA_HOME에 JDK 경로 추가
"JAVA_HOME" 하면 이름을 지정 하는 시스템 환경 변수를 JDK/JRE 설치 경로 (예: "C:\Program Files\Java\jdk-10.0.2")를 추가 해야 합니다. 

시스템 변수를 만들려면 제어판을 사용 하 여 > 시스템 및 보안 > 액세스 하기 위해 시스템 **시스템 속성 고급**합니다. 클릭 **환경 변수** 다음 JAVA_HOME에 대 한 새 시스템 변수를 만듭니다.

![Java 홈에 대 한 환경 변수](../media/java/env-variable-java-home.png "Java에 대 한 설정")

## <a name="jdk-on-linux"></a>Linux에서 JDK

Linux의 mssql server-확장성 java 패키지를 자동으로 설치 JRE 1.8 아직 설치 되지 않은 경우. 또한 JVM 경로 JAVA_HOME 라는 환경 변수에 추가 됩니다.

## <a name="limitations-in-ctp-20"></a>CTP 2.0의에서 제한 사항

* 입력 및 출력 버퍼에 있는 값의 수를 초과할 수 없습니다 `MAX_INT (2^31-1)` Java 배열에서 할당 될 수 있는 요소의 최대 개수 이기 때문입니다.

* Sp_execute_external_script에서 출력 매개 변수는이 버전에서 지원 되지 않습니다.

* 이 버전에서는 입력 및 출력 데이터 집합에 대 한 LOB 데이터 형식이 지원 되지 않습니다. 참조 [Java와 SQL Server 데이터 형식](java-sql-datatypes.md) 형식이이 CTP에 지원 되는 데이터에 대 한 세부 정보에 대 한 합니다.

* Sp_execute_external_script 매개 변수를 사용 하 여 스트리밍 @r_rowsPerRead 이 CTP에서 지원 되지 않습니다.

* Sp_execute_external_script 매개 변수를 사용 하 여 분할 @input_data_1_partition_by_columns 이 CTP에서 지원 되지 않습니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java를 호출 하는 방법](howto-call-java-from-sql.md)
+ [SQL Server에서 Java 샘플](java-first-sample.md)
+ [Java와 SQL Server 데이터 형식](java-sql-datatypes.md)