---
title: JDBC Driver의 시스템 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b317b3483d24087df203eb14fdabe7b12f2539
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893970"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC 드라이버의 시스템 요구 사항
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]의 데이터에 액세스하려면 컴퓨터에 다음 구성 요소를 설치해야 합니다.

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]([다운로드](download-microsoft-jdbc-driver-for-sql-server.md))
- Java Runtime Environment

## <a name="java-runtime-environment-requirements"></a>Java Runtime Environment 요구 사항  

 SQL Server용 Microsoft JDBC Driver 7.4부터는 JDK(Java Development Kit) 12.0 및 JRE(Java Runtime Environment) 12.0이 지원됩니다.

 SQL Server용 Microsoft JDBC Driver 7.2부터는 JDK(Java Development Kit) 11.0 및 JRE(Java Runtime Environment) 11.0이 지원됩니다.
 
 SQL Server용 Microsoft JDBC Driver 7.0부터는 JDK(Java Development Kit) 10.0 및 JRE(Java Runtime Environment) 10.0이 지원됩니다.

 SQL Server용 Microsoft JDBC Driver 6.4부터는 JDK(Java Development Kit) 9.0 및 JRE(Java Runtime Environment) 9.0이 지원됩니다.

 SQL Server용 Microsoft JDBC Driver 4.2부터는 JDK(Java Development Kit) 8.0 및 JRE(Java Runtime Environment) 8.0이 지원됩니다. JDBC 4.1 및 4.2 API를 포함하도록 JDBC(Java Database Connectivity) 사양 API에 대한 지원이 확장되었습니다.
  
 SQL Server용 Microsoft JDBC Driver 4.1부터는 JDK(Java Development Kit) 7.0 및 JRE(Java Runtime Environment) 7.0이 지원됩니다.
  
 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]에서는 JDBC 4.0 API를 포함하도록 JDBC(Java Database Connectivity) 사양 API에 대한 지원이 확장되었습니다. JDBC 4.0 API는 JDK(Java Development Kit) 6.0 및 JRE(Java Runtime Environment) 6.0의 일부로 제공되었습니다. JDBC 4.0은 JDBC 3.0 API를 포함합니다.
  
 Windows 및 UNIX 운영 체제에서 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 배포하는 경우 각각 설치 패키지 *sqljdbc_\<version>_enu.exe* 및 *sqljdbc_\<version>_enu.tar.gz*를 사용해야 합니다. JDBC Driver를 배포하는 방법에 대한 자세한 내용은 [Deploying the JDBC Driver](../../connect/jdbc/deploying-the-jdbc-driver.md)(JDBC Driver 배포) 항목을 참조하세요.  

**SQL Server용 Microsoft JDBC Driver 7.4:**  

  JDBC Driver 7.4에는 각 설치 패키지에 **mssql-jdbc-7.4.1.jre8.jar**, **mssql-jdbc-7.4.1.jre11.jar** 및 **mssql-jdbc-7.4.1.jre12.jar**라는 세 개의 JAR 클래스 라이브러리가 포함되어 있습니다.

  JDBC Driver 7.4는 모든 주요 Java 가상 머신에서 사용 가능하고 지원되지만, OpenJDK 1.8, OpenJDK 11.0, OpenJDK 12.0, Azul Zulu JRE 1.8, Azul Zulu JRE 11.0 및 Azul Zulu JRE 12.0에서만 테스트되었습니다.
  
  SQL Server용 Microsoft JDBC Driver 7.4에 포함된 2개의 JAR 파일에서 제공하는 지원은 다음과 같이 요약됩니다.  
  
  |JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.4.1. jre8|4.2|8|JRE(Java Runtime Environment) 1.8이 필요합니다. JRE 1.7 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 7\.4의 새로운 기능에는 JDK 12 지원, NTLM 인증 및 useFmtOnly가 포함 됩니다. |    
|mssql-jdbc-7.4.1. jre11|4.3|11|JRE(Java Runtime Environment) 11.0이 필요합니다. JRE 10.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 7\.4의 새로운 기능에는 JDK 12 지원, NTLM 인증 및 useFmtOnly가 포함 됩니다. |  
|mssql-jdbc-7.4.1. jre12|4.3|12|JRE(Java Runtime Environment) 12.0이 필요합니다. JRE 11.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 7\.4의 새로운 기능에는 JDK 12 지원, NTLM 인증 및 useFmtOnly가 포함 됩니다. |   


  JDBC Driver 7.4는 Maven 중앙 리포지토리에서도 사용할 수 있고 POM.XML에 다음 코드를 추가하여 Maven 프로젝트에 추가할 수 있습니다.  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
</dependency>
```

**SQL Server용 Microsoft JDBC Driver 7.2:**  

  JDBC Driver 7.2에는 각 설치 패키지에 **mssql-jdbc-7.2.2.jre8.jar** 및 **mssql-jdbc-7.2.2.jre11.jar**라는 두 개의 JAR 클래스 라이브러리가 포함되어 있습니다.

  JDBC Driver 7.2는 모든 주요 Java 가상 머신에서 사용 가능하고 지원되지만, OpenJDK 8.0 및 , OpenJDK 11.0, Azul Zulu JRE 8.0 및 Azul Zulu JRE 11.0.에서만 테스트되었습니다.
  
  SQL Server용 Microsoft JDBC Driver 7.2에 포함된 2개의 JAR 파일에서 제공하는 지원은 다음과 같이 요약됩니다.  
  
  |JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.2.2.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 7\.2의 새로운 기능은 JDK 11 지원, Active Directory MSI(관리 서비스 ID) 인증, OSGi 지원, SQLServerError API 등입니다. |    
|mssql-jdbc-7.2.2.jre11.jar|4.3|10|JRE(Java Runtime Environment) 11.0이 필요합니다. JRE 10.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 7\.2의 새로운 기능은 JDK 11 지원, Active Directory MSI(관리 서비스 ID) 인증, OSGi 지원, SQLServerError API 등입니다. |    


  JDBC Driver 7.2는 Maven 중앙 리포지토리에서도 사용할 수 있고 POM.XML에 다음 코드를 추가하여 Maven 프로젝트에 추가할 수 있습니다.  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
</dependency>
```
 
**SQL Server용 Microsoft JDBC Driver 7.0**  

  JDBC Driver 7.0에는 설치 패키지 각각에 **mssql-jdbc-7.0.0.jre8.jar** 및 **mssql-jdbc-7.0.0.jre10.jar**이라는 두 개의 JAR 클래스 라이브러리가 포함되어 있습니다.

  JDBC Driver 7.0은 모든 주요 Java 가상 머신에서 사용 가능하고 지원되지만, OpenJDK 8.0 및 10.0에서만 테스트되었습니다.
  
  다음에는 SQL Server용 Microsoft JDBC Driver 7.0에 포함된 2개의 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
  |JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 7\.0의 새로운 기능은 JDK 10 지원, 기본 준수 수준을 JDBC 4.2 사양으로 업데이트, 공간 데이터 형식 지원, cancelQueryTimeout 연결 속성, 경계 요청 메서드, useBulkCopyForBatchInsert 연결 속성, 데이터 검색 및 분류 정보, UTF-8 기능 확장 및 CityHash 지원 등입니다. |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|JRE(Java Runtime Environment) 10.0이 필요합니다. JRE 9.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 7\.0의 새로운 기능은 JDK 10 지원, 기본 준수 수준을 JDBC 4.2 사양으로 업데이트, 공간 데이터 형식 지원, cancelQueryTimeout 연결 속성, 경계 요청 메서드, useBulkCopyForBatchInsert 연결 속성, 데이터 검색 및 분류 정보, UTF-8 기능 확장 및 CityHash 지원 등입니다. |    


  JDBC Driver 7.0은 Maven 중앙 리포지토리에서도 사용할 수 있고 POM.XML에 다음 코드를 추가하여 Maven 프로젝트에 추가할 수 있습니다.  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```
  
**SQL Server용 Microsoft JDBC Driver 6.4:**  

  JDBC Driver 6.4에는 설치 패키지 각각에 **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** 및 **mssql-jdbc-6.4.0.jre9.jar**이라는 세 개의 JAR 클래스 라이브러리가 포함되어 있습니다.

  JDBC Driver 6.4는 모든 주요 Java 가상 머신에서 사용 가능하고 지원되지만, OpenJDK 7.0, 8.0 및 9.0에서만 테스트되었습니다.
  
  다음에는 SQL Server용 Microsoft JDBC Driver 6.4에 포함된 3개의 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
  |JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 6\.4의 새로운 기능은 Linux용 Azure AD 인증, Kerberos에 대한 보안 주체/암호 방식, 도메인 간 인증을 위해 SPN에서 REALM 자동 검색, Kerberos 제한 위임, 쿼리 시간 제한, 소켓 시간 제한, 준비된 문 재사용 등입니다. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 6\.4의 새로운 기능은 Linux용 Azure AD 인증, Kerberos에 대한 보안 주체/암호 방식, 도메인 간 인증을 위해 SPN에서 REALM 자동 검색, Kerberos 제한 위임, 쿼리 시간 제한, 소켓 시간 제한, 준비된 문 재사용 등입니다. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|JRE(Java Runtime Environment) 9.0이 필요합니다. JRE 8.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 6\.4의 새로운 기능은 Linux용 Azure AD 인증, Kerberos에 대한 보안 주체/암호 방식, 도메인 간 인증을 위해 SPN에서 REALM 자동 검색, Kerberos 제한 위임, 쿼리 시간 제한, 소켓 시간 제한, 준비된 문 재사용 등입니다. |

JDBC Driver 6.4는 Maven 중앙 리포지토리에서도 사용할 수 있고 POM.XML에 다음 코드를 추가하여 Maven 프로젝트에 추가할 수 있습니다. 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**SQL Server용 Microsoft JDBC Driver 6.2:**  
  
  JDBC Driver 6.2에는 각 설치 패기지에 **mssql-jdbc-6.2.2.jre7.jar** 및 **mssql-jdbc-6.2.2.jre8.jar**의 두 JAR 클래스 라이브러리가 포함되어 있습니다. 
  
 JDBC Driver 6.2는 모든 주요 Java 가상 머신에서 사용 가능하고 지원되지만, Sun JRE 5.0, 6.0, 7.0 및 8.0에서만 테스트되었습니다.
  
 다음에는 SQL Server용 Microsoft JDBC Driver 6.0 및 4.2에 포함된 두 개의 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
|JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|
|mssql-jdbc-6.2.2.jre7.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 6\.2의 새로운 기능은 Linux용 Azure AD 인증, Kerberos에 대한 보안 주체/암호 방식, 도메인 간 인증을 위해 SPN에서 REALM 자동 검색, Kerberos 제한 위임, 쿼리 시간 제한, 소켓 시간 제한, 준비된 문 재사용 등입니다. |  
|mssql-jdbc-6.2.3.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 6\.2의 새로운 기능은 Linux용 Azure AD 인증, Kerberos에 대한 보안 주체/암호 방식, 도메인 간 인증을 위해 SPN에서 REALM 자동 검색, Kerberos 제한 위임, 쿼리 시간 제한, 소켓 시간 제한, 준비된 문 재사용 등입니다.|    

  JDBC Driver 6.2는 Maven 중앙 리포지토리에서도 사용할 수 있고 POM.XML에 다음 코드를 추가하여 Maven 프로젝트에 추가할 수 있습니다. 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **SQL Server용 Microsoft JDBC Driver 6.0 및 4.2:**  
  
  JDBC Drivers 6.0 및 4.2의 각 설치 패키지에는 **sqljdbc41.jar** 및 **sqljdbc42.jar**라는 두 개의 JAR 클래스 라이브러리가 포함되어 있습니다. 
  
 JDBC Driver 6.0 및 4.2는 모든 주요 Java 가상 머신에서 사용 가능하고 지원되지만, Sun JRE 5.0, 6.0, 7.0 및 8.0에 대해서만 테스트되었습니다.
  
 다음에는 SQL Server용 Microsoft JDBC Driver 6.0 및 4.2에 포함된 두 개의 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
|JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 6\.0 및 4.2 패키지의 새로운 기능에는 JDBC 4.1 준수 및 대량 복사가 포함됩니다.<br /><br /> 또한 6.0 패키지만의 새로운 기능에는 Always Encrypted, 테이블 반환 매개 변수, Azure Active Directory 인증, Always On 가용성 그룹에 투명하게 연결, 준비된 쿼리에 한 매개 변수 메타데이터 검색 향상 및 IDN(다국어 도메인 이름)이 포함됩니다.|  
|sqljdbc42.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 이전 버전을 사용하면 예외가 throw됩니다.<br /><br /> 6\.0 및 4.2 패키지의 새로운 기능에는 JDBC 4.1 준수, JDBC 4.2 준수 및 대량 복사가 포함됩니다.<br /><br /> 또한 6.0 패키지만의 새로운 기능에는 Always Encrypted, 테이블 반환 매개 변수, Azure Active Directory 인증, Always On 가용성 그룹에 투명하게 연결, 준비된 쿼리에 한 매개 변수 메타데이터 검색 향상 및 IDN(다국어 도메인 이름)이 포함됩니다.|  
  
 **SQL Server용 Microsoft JDBC Driver 4.1:**  
  
 JDBC Driver 4.1의 각 설치 패키지에는 **sqljdbc41.jar**라는 하나의 JAR 클래스 라이브러리가 포함되어 있습니다.  
    
|JAR|설명|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** 클래스 라이브러리는 JDBC 4.0 API를 지원합니다. 이 라이브러리에는 JDBC 4.0 드라이버의 모든 기능과 함께 JDBC 4.0 API 메서드가 포함되어 있습니다. JDBC 4.1은 지원되지 않습니다(“SQLFeatureNotSupportedException” 예외가 throw됨).<br /><br /> **sqljdbc41.jar** 클래스 라이브러리에는 JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 및 5.0에서 **sqljdbc41.jar**를 사용하면 예외가 throw됩니다.<br /><br /> 
  
 JDBC Driver는 모든 주요 Java 가상 머신에서 사용 가능하고 지원되지만, Sun JRE 5.0, 6.0 및 7.0에서 테스트되었습니다.
  
 다음에는 SQL Server용 Microsoft JDBC Driver 4.1에 포함된 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
|JAR|JDBC 버전|JRE(실행 가능)|JDK(컴파일 가능)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>SQL Server 요구 사항  
 JDBC 드라이버는 Azure SQL 데이터베이스 및 SQL Server에 대한 연결을 지원합니다. SQL Server용 Microsoft JDBC Driver 4.2 및 4.1의 경우 SQL Server 2008에서 지원이 시작됩니다.
  
## <a name="operating-system-requirements"></a>운영 체제 요구 사항  
 JDBC 드라이버는 JVM(Java Virtual Machine)의 사용을 지원하는 모든 운영 체제에서 작동하도록 설계되어 있지만 Sun Solaris, SUSE Linux 및 Windows 운영 체제에서만 공식적으로 테스트가 완료되었습니다.  
  
## <a name="supported-languages"></a>지원되는 언어  
 JDBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 열 데이터 정렬을 지원합니다. JDBC Driver에서 지원하는 데이터 정렬에 대한 자세한 내용은 [International Features of the JDBC Driver](../../connect/jdbc/international-features-of-the-jdbc-driver.md)(JDBC Driver의 국가별 기능)를 참조하세요.  
  
 데이터 정렬에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "데이터 정렬 사용"을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
