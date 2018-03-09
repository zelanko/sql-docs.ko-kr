---
title: "JDBC 드라이버에 대 한 시스템 요구 사항 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: e6a4aa824e50fd10add0b40c483b74b674e56a6e
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC 드라이버의 시스템 요구 사항
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  데이터에 액세스할은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 를 사용 하 여는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 다음 구성 요소가 컴퓨터에 설치 되어 있어야 합니다.  
  
-   [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]  
  
     Microsoft JDBC Driver 아래 Microsoft 다운로드 센터 링크에서 다운로드할 수 있습니다. 
     * [Microsoft JDBC Driver 6.4 for SQL Server](http://go.microsoft.com/fwlink/?linkid=868290)
     * [Microsoft JDBC Driver 6.2 for SQL Server](http://go.microsoft.com/fwlink/?linkid=852460)
     * [Microsoft JDBC Driver 6.0 for SQL Server](http://go.microsoft.com/fwlink/?linkid=841535)
     * [Microsoft JDBC Driver 4.2 for SQL Server](http://go.microsoft.com/fwlink/?linkid=841534) 
     * [Microsoft JDBC Driver 4.1 for SQL Server](http://go.microsoft.com/fwlink/?linkid=841533) 
  
-   Java Runtime Environment  
  
## <a name="java-runtime-environment-requirements"></a>Java Runtime Environment 요구 사항  
 SQL Server 용 Microsoft JDBC 드라이버 6.4 이상에서는 Sun Java SE Development Kit (JDK) 9.0 및 Java Runtime Environment (JRE) 9.0 지원 됩니다.

 SQL Server용 Microsoft JDBC Driver 4.2부터 Sun JDK(Java SE Development Kit) 8.0 및 JRE(Java Runtime Environment) 8.0이 지원됩니다. JDBC 4.1 및 4.2 API를 포함하도록 JDBC(Java Database Connectivity) 사양 API에 대한 지원이 확장되었습니다.  
  
 SQL Server용 Microsoft JDBC Driver 4.1부터는 Sun JDK(Java SE Development Kit) 7.0 및 JRE(Java Runtime Environment) 7.0이 지원됩니다.  
  
 부터는 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], JDBC 4.0 API를 포함 하도록 JDBC Java Database Connectivity () 사양 API에 대 한 지원이 확장 되었습니다. JDBC 4.0 API는 Sun Java SE Development Kit(API) JDK 6.0 및 Java Runtime Environment(JRE) 6.0에 새로 추가되었습니다. JDBC 4.0은 JDBC 3.0 API를 포함합니다.  
  
 배포 하는 경우는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Windows 및 UNIX 운영 체제 설치 패키지를 사용 해야 *sqljdbc_\<버전 > _enu.exe* 및 *sqljdbc_\<버전 > _ enu.tar.gz*각각. JDBC 드라이버를 배포 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버 배포](../../connect/jdbc/deploying-the-jdbc-driver.md) 항목입니다.  
  
**SQL Server 용 Microsoft JDBC Driver 6.4:**  

  JDBC 드라이버 6.4 각 설치 패키지에 3 개의 JAR 클래스 라이브러리가 포함: **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, 및 **mssql-jdbc-6.4.0.jre9.jar** .

  JDBC 드라이버 6.4 작동 하며 모든 주요 Sun 호환 Java 가상 컴퓨터에서 지원 하도록 만들어졌지만 Sun JRE 7.0, 8.0 및 9.0에 대해서만 테스트 됩니다.
  
  SQL Server 용 Microsoft JDBC 드라이버 6.4에 포함 된 3 개의 JAR 파일에서 제공 하는 지원을 요약는 다음과 같습니다.  
  
  |JAR|JDBC 버전 규격|권장 Java 버전|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 또는 더 낮은 throw 예외를 사용합니다.<br /><br /> 6.4의 새로운 기능 포함: Linux, Kerberos, 도메인 간 인증에 Kerberos 제한 위임, 쿼리 제한 시간, 소켓 제한 시간은 자동 검색의 SPN에 대 한 영역에 대 한 사용자/암호 방법에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용할 수 있도록 합니다. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 또는 더 낮은 throw 예외를 사용합니다.<br /><br /> 6.4의 새로운 기능 포함: Linux, Kerberos, 도메인 간 인증에 Kerberos 제한 위임, 쿼리 제한 시간, 소켓 제한 시간은 자동 검색의 SPN에 대 한 영역에 대 한 사용자/암호 방법에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용할 수 있도록 합니다. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|Java Runtime Environment (JRE) 9.0 필요합니다. JRE 8.0 또는 더 낮은 throw 예외를 사용합니다.<br /><br /> 6.4의 새로운 기능 포함: Linux, Kerberos, 도메인 간 인증에 Kerberos 제한 위임, 쿼리 제한 시간, 소켓 제한 시간은 자동 검색의 SPN에 대 한 영역에 대 한 사용자/암호 방법에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용할 수 있도록 합니다. |    


  JDBC 드라이버 6.4 Maven 중앙 저장소 및는 POM에 다음 코드를 추가 하 여 Maven 프로젝트에 추가할 수 있습니다 사용할 수도 있습니다. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```    
**SQL Server 용 Microsoft JDBC Driver 6.2:**  
  
  JDBC 드라이버 6.2 각 설치 패키지에 두 개의 JAR 클래스 라이브러리가 포함: **mssql-jdbc-6.2.1.jre7.jar**, 및 **mssql-jdbc-6.2.1.jre8.jar**합니다. 
  
 JDBC 드라이버 6.2 작동 하며 모든 주요 Sun 호환 Java 가상 컴퓨터에서 지원 하도록 만들어졌지만 Sun JRE 5.0, 6.0, 7.0 및 8.0에 대해서만 테스트 됩니다. 
  
 SQL Server 용 Microsoft JDBC Driver 6.0 및 4.2에 포함 된 두 개의 JAR 파일에서 제공 하는 지원을 요약는 다음과 같습니다.  
  
|JAR|JDBC 버전 규격|권장 Java 버전|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.2.1.jre7.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 또는 더 낮은 throw 예외를 사용합니다.<br /><br /> 6.2의 새로운 기능 포함: Linux, Kerberos, 도메인 간 인증에 Kerberos 제한 위임, 쿼리 제한 시간, 소켓 제한 시간은 자동 검색의 SPN에 대 한 영역에 대 한 사용자/암호 방법에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용 합니다. |  
|mssql-jdbc-6.2.1.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 또는 더 낮은 throw 예외를 사용합니다.<br /><br /> 6.2의 새로운 기능 포함: Linux, Kerberos, 도메인 간 인증에 Kerberos 제한 위임, 쿼리 제한 시간, 소켓 제한 시간은 자동 검색의 SPN에 대 한 영역에 대 한 사용자/암호 방법에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용|    

  JDBC 드라이버 6.2 Maven 중앙 저장소 및는 POM에 다음 코드를 추가 하 여 Maven 프로젝트에 추가할 수 있습니다 사용할 수도 있습니다. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 및 4.2 for SQL Server:**  
  
  JDBC Driver 6.0 및 4.2 각 설치 패키지에 두 개의 JAR 클래스 라이브러리가 포함 되어: **sqljdbc41.jar**, 및 **sqljdbc42.jar**합니다. 
  
 JDBC Driver 6.0 및 4.2를 사용 하 고 모든 주요 Sun 호환 Java 가상 컴퓨터에서 지원 하도록 설계 되었습니다 되지만 Sun JRE 5.0, 6.0, 7.0 및 8.0에 대해서만 테스트 됩니다. 
  
 SQL Server 용 Microsoft JDBC Driver 6.0 및 4.2에 포함 된 두 개의 JAR 파일에서 제공 하는 지원을 요약는 다음과 같습니다.  
  
|JAR|JDBC 버전 규격|권장 Java 버전|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE 6.0 또는 더 낮은 throw 예외를 사용합니다.<br /><br /> 6.0 및 4.2 패키지의 새로운 기능에는 JDBC 4.1 준수 및 대량 복사가 포함됩니다.<br /><br /> 또한 6.0 패키지에만의 새로운 기능 포함: Azure Active Directory 인증 상시 암호화, 테이블 반환 매개 변수를 투명 하 게 연결할 Always On 가용성 그룹을 개선에 대 한 매개 변수 메타 데이터 검색에 준비 쿼리 및 도메인 이름 IDN (Internationalized)|  
|sqljdbc42.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE 7.0 또는 더 낮은 throw 예외를 사용합니다.<br /><br /> 6.0 및 4.2 패키지의 새로운 기능에는 JDBC 4.1 준수, JDBC 4.2 준수 및 대량 복사가 포함됩니다.<br /><br /> 또한 6.0 패키지에만의 새로운 기능 포함: Azure Active Directory 인증 상시 암호화, 테이블 반환 매개 변수를 투명 하 게 연결할 Always On 가용성 그룹을 개선에 대 한 매개 변수 메타 데이터 검색에 준비 쿼리 및 도메인 이름 IDN (Internationalized)|  
  
 **SQL Server 용 Microsoft JDBC Driver 4.1:**  
  
 JDBC Driver 4.1의 각 설치 패키지 하나 JAR 클래스 라이브러리가 포함 됩니다.: **sqljdbc41.jar**합니다.  
    
|JAR|Description|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** 클래스 라이브러리는 JDBC 4.0 API에 대 한 지원을 제공 합니다. 모든 기능으로는 JDBC 4.0 드라이버는 JDBC 4.0 API 메서드가 포함 됩니다. JDBC 4.1은 지원 되지 않습니다 ("SQLFeatureNotSupportedException" 예외를 throw).<br /><br /> **sqljdbc41.jar** 클래스 라이브러리에는 환경 JRE (Java Runtime) 7.0이 필요 합니다. 사용 하 여 **sqljdbc41.jar** JRE 6.0 또는 5.0에서 예외를 throw 합니다.<br /><br /> 
  
 JDBC 드라이버는 모든 주요 Sun 호환 Java 가상 컴퓨터에서 작동하고 지원되도록 설계되어 있지만 테스트는 Sun JRE 5.0, 6.0 및 7.0 이상에서 수행됩니다.  
  
 다음은 SQL Server 용 Microsoft JDBC Driver 4.1에 포함 된 JAR 파일에서 제공 된 지원에 대 한 요약입니다.  
  
|JAR|JDBC 버전|JRE(실행 가능)|JDK(컴파일 가능)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>SQL Server 요구 사항  
 JDBC 드라이버는 Azure SQL 데이터베이스 및 SQL Server에 대 한 연결을 지원합니다. SQL Server용 Microsoft JDBC Driver 4.2 및 4.1의 경우 SQL Server 2008에서 지원이 시작됩니다.
  
## <a name="operating-system-requirements"></a>운영 체제 요구 사항  
 JDBC 드라이버는 JVM(Java Virtual Machine)의 사용을 지원하는 모든 운영 체제에서 작동하도록 설계되어 있지만 Sun Solaris, SUSE Linux 및 Windows 운영 체제에서만 공식적으로 테스트가 완료되었습니다.  
  
## <a name="supported-languages"></a>지원되는 언어  
 JDBC 드라이버는 모든 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 열 데이터 정렬이 있습니다. JDBC 드라이버에서 지 원하는 데이터 정렬에 대 한 자세한 내용은 참조 [JDBC 드라이버의 국제 기능](../../connect/jdbc/international-features-of-the-jdbc-driver.md)합니다.  
  
 데이터 정렬에 대 한 자세한 내용은 "데이터 정렬 사용"을 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
