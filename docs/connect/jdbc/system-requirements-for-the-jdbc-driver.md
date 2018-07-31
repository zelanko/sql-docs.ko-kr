---
title: JDBC 드라이버 시스템 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 306c7bcd764ed70f23c51667580fb9f8e79f0e65
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37978725"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC 드라이버의 시스템 요구 사항
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]의 데이터에 액세스하려면 컴퓨터에 다음 구성 요소를 설치해야 합니다.

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]([다운로드](download-microsoft-jdbc-driver-for-sql-server.md))
- Java Runtime Environment

## <a name="java-runtime-environment-requirements"></a>Java Runtime Environment 요구 사항  
 SQL Server용 Microsoft JDBC Driver 6.4부터는 Sun JDK(Java SE Development Kit) 9.0 및 JRE(Java Runtime Environment) 9.0이 지원됩니다.

 SQL Server용 Microsoft JDBC Driver 4.2부터 Sun JDK(Java SE Development Kit) 8.0 및 JRE(Java Runtime Environment) 8.0이 지원됩니다. JDBC 4.1 및 4.2 API를 포함하도록 JDBC(Java Database Connectivity) 사양 API에 대한 지원이 확장되었습니다.  
  
 SQL Server용 Microsoft JDBC Driver 4.1부터는 Sun JDK(Java SE Development Kit) 7.0 및 JRE(Java Runtime Environment) 7.0이 지원됩니다.  
  
 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]에서는 JDBC 4.0 API를 포함하도록 JDBC(Java Database Connectivity) 사양 API에 대한 지원이 확장되었습니다. JDBC 4.0 API는 Sun Java SE Development Kit(API) JDK 6.0 및 Java Runtime Environment(JRE) 6.0에 새로 추가되었습니다. JDBC 4.0은 JDBC 3.0 API를 포함합니다.  
  
 Windows 및 UNIX 운영 체제에서 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 배포하는 경우 각각 설치 패키지 *sqljdbc_\<version>_enu.exe* 및 *sqljdbc_\<version>_enu.tar.gz*를 사용해야 합니다. JDBC 드라이버를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [JDBC 드라이버 배포](../../connect/jdbc/deploying-the-jdbc-driver.md) 항목입니다.  
  
**SQL Server용 Microsoft JDBC Driver 6.4:**  

  JDBC Driver 6.4 각 설치 패키지에 대 한 3 개의 JAR 클래스 라이브러리가: **mssql-jdbc-6.4.0.jre7.jar**를 **mssql-jdbc-6.4.0.jre8.jar**, 및 **mssql-jdbc-6.4.0.jre9.jar** .

  JDBC Driver 6.4는 모든 주요 Sun 동등 Java 가상 머신에서 사용 가능하고 지원되지만 Sun JRE 7.0, 8.0 및 9.0에 대해서만 테스트되었습니다.
  
  다음에는 SQL Server용 Microsoft JDBC Driver 6.4에 포함된 3개의 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
  |JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 또는 낮은 throw 예외를 사용합니다.<br /><br /> 6.4의 새로운 기능 포함: linux의 경우 사용자/암호 메서드 Kerberos 도메인 간 인증, Kerberos Constrained Delegation, 쿼리 제한 시간, 소켓 시간 제한에 대 한 SPN에서 REALM의 자동 검색에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용 합니다. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 또는 낮은 throw 예외를 사용합니다.<br /><br /> 6.4의 새로운 기능 포함: linux의 경우 사용자/암호 메서드 Kerberos 도메인 간 인증, Kerberos Constrained Delegation, 쿼리 제한 시간, 소켓 시간 제한에 대 한 SPN에서 REALM의 자동 검색에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용 합니다. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|JRE(Java Runtime Environment) 9.0이 필요합니다. JRE 8.0 또는 낮은 throw 예외를 사용합니다.<br /><br /> 6.4의 새로운 기능 포함: linux의 경우 사용자/암호 메서드 Kerberos 도메인 간 인증, Kerberos Constrained Delegation, 쿼리 제한 시간, 소켓 시간 제한에 대 한 SPN에서 REALM의 자동 검색에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용 합니다. |    


  JDBC Driver 6.4 Maven 중앙 리포지토리에서 사용할 수 있는 이기도 하며 POM에 다음 코드를 추가 하 여 Maven 프로젝트에 추가할 수 있습니다. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```    
**SQL Server용 Microsoft JDBC Driver 6.2:**  
  
  JDBC Driver 6.2 각 설치 패키지에 대 한 두 개의 JAR 클래스 라이브러리가: **mssql-jdbc-6.2.1.jre7.jar**, 및 **mssql-jdbc-6.2.1.jre8.jar**합니다. 
  
 JDBC Driver 6.2는 모든 주요 Sun 동등 Java 가상 머신에서 사용 가능하고 지원되지만 Sun JRE 5.0, 6.0, 7.0 및 8.0에 대해서만 테스트되었습니다. 
  
 다음에는 SQL Server용 Microsoft JDBC Driver 6.0 및 4.2에 포함된 두 개의 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
|JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.2.1.jre7.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 또는 낮은 throw 예외를 사용합니다.<br /><br /> 6.2의 새로운 기능 포함: linux의 경우 사용자/암호 메서드 Kerberos 도메인 간 인증, Kerberos Constrained Delegation, 쿼리 제한 시간, 소켓 시간 제한에 대 한 SPN에서 REALM의 자동 검색에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용 합니다. |  
|mssql-jdbc-6.2.1.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 또는 낮은 throw 예외를 사용합니다.<br /><br /> 6.2의 새로운 기능 포함: linux의 경우 사용자/암호 메서드 Kerberos 도메인 간 인증, Kerberos Constrained Delegation, 쿼리 제한 시간, 소켓 시간 제한에 대 한 SPN에서 REALM의 자동 검색에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용|    

  JDBC Driver 6.2 Maven 중앙 리포지토리에서 사용할 수 있는 이기도 하며 POM에 다음 코드를 추가 하 여 Maven 프로젝트에 추가할 수 있습니다. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```    

 **SQL Server용 Microsoft JDBC Driver 6.0 및 4.2:**  
  
  JDBC 드라이버 6.0 및 4.2의 각 설치 패키지 두 개의 JAR 클래스 라이브러리가 포함 됩니다. **sqljdbc41.jar**, 및 **sqljdbc42.jar**합니다. 
  
 JDBC Driver 6.0 및 4.2는 모든 주요 Sun 동등 Java 가상 머신에서 사용 가능하고 지원되지만 Sun JRE 5.0, 6.0, 7.0 및 8.0에 대해서만 테스트되었습니다. 
  
 다음에는 SQL Server용 Microsoft JDBC Driver 6.0 및 4.2에 포함된 두 개의 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
|JAR|JDBC 버전 규격|권장 Java 버전|설명|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 또는 낮은 throw 예외를 사용합니다.<br /><br /> 6.0 및 4.2 패키지의 새로운 기능에는 JDBC 4.1 준수 및 대량 복사가 포함됩니다.<br /><br /> 또한 6.0 패키지에만의 새로운 기능 포함: Azure Active Directory 인증 상시 암호화, 테이블 반환 매개 변수를 Always On 가용성 그룹에 대 한 매개 변수 메타 데이터 검색 개선에 대 한 투명 하 게 연결 준비 쿼리 및 다국어 도메인 이름 (IDN)|  
|sqljdbc42.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 또는 낮은 throw 예외를 사용합니다.<br /><br /> 6.0 및 4.2 패키지의 새로운 기능에는 JDBC 4.1 준수, JDBC 4.2 준수 및 대량 복사가 포함됩니다.<br /><br /> 또한 6.0 패키지에만의 새로운 기능 포함: Azure Active Directory 인증 상시 암호화, 테이블 반환 매개 변수를 Always On 가용성 그룹에 대 한 매개 변수 메타 데이터 검색 개선에 대 한 투명 하 게 연결 준비 쿼리 및 다국어 도메인 이름 (IDN)|  
  
 **SQL Server용 Microsoft JDBC Driver 4.1:**  
  
 JDBC Driver 4.1의 각 설치 패키지 하나 JAR 클래스 라이브러리가 포함 됩니다.: **sqljdbc41.jar**합니다.  
    
|JAR|설명|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** 클래스 라이브러리는 JDBC 4.0 API를 지원합니다. 이 라이브러리에는 JDBC 4.0 드라이버의 모든 기능과 함께 JDBC 4.0 API 메서드가 포함되어 있습니다. JDBC 4.1은 지원되지 않습니다("SQLFeatureNotSupportedException" 예외가 throw됨).<br /><br /> **sqljdbc41.jar** 클래스 라이브러리에는 JRE(Java Runtime Environment) 7.0이 필요합니다. 사용 하 여 **sqljdbc41.jar** JRE 6.0 또는 5.0에서 예외를 throw 합니다.<br /><br /> 
  
 JDBC 드라이버는 모든 주요 Sun 호환 Java 가상 머신에서 작동하고 지원되도록 설계되어 있지만 테스트는 Sun JRE 5.0, 6.0 및 7.0에서 수행됩니다.  
  
 다음에는 SQL Server용 Microsoft JDBC Driver 4.1에 포함된 JAR 파일에서 제공하는 지원이 요약되어 있습니다.  
  
|JAR|JDBC 버전|JRE(실행 가능)|JDK(컴파일 가능)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>SQL Server 요구 사항  
 JDBC 드라이버는 Azure SQL 데이터베이스 및 SQL Server에 대한 연결을 지원합니다. SQL Server용 Microsoft JDBC Driver 4.2 및 4.1의 경우 SQL Server 2008에서 지원이 시작됩니다.
  
## <a name="operating-system-requirements"></a>운영 체제 요구 사항  
 JDBC 드라이버는 JVM(Java Virtual Machine)의 사용을 지원하는 모든 운영 체제에서 작동하도록 설계되어 있지만 Sun Solaris, SUSE Linux 및 Windows 운영 체제에서만 공식적으로 테스트가 완료되었습니다.  
  
## <a name="supported-languages"></a>지원되는 언어  
 JDBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 모든 열 데이터 정렬을 지원합니다. JDBC 드라이버에서 지 원하는 데이터 정렬에 대 한 자세한 내용은 참조 하세요. [JDBC 드라이버의 국가별 기능](../../connect/jdbc/international-features-of-the-jdbc-driver.md)합니다.  
  
 데이터 정렬에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서의 "데이터 정렬 사용"을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
