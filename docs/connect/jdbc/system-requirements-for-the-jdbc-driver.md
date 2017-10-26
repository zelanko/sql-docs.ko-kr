---
title: "JDBC 드라이버에 대 한 시스템 요구 사항 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eed93fab6f0ceec655b7b9f6b392abc390b5f0ff
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC 드라이버의 시스템 요구 사항
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  데이터에 액세스할은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 를 사용 하 여는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 다음 구성 요소가 컴퓨터에 설치 되어 있어야 합니다.  
  
-   [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]  
  
     Microsoft JDBC Driver 아래 Microsoft 다운로드 센터 링크에서 다운로드할 수 있습니다. 
     * [SQL Server 용 Microsoft JDBC Driver 6.2](http://go.microsoft.com/fwlink/?linkid=852460)
     * [SQL Server 용 Microsoft JDBC Driver 6.0](http://go.microsoft.com/fwlink/?linkid=841535)
     * [SQL Server 용 Microsoft JDBC Driver 4.2](http://go.microsoft.com/fwlink/?linkid=841534) 
     * [SQL Server 용 Microsoft JDBC Driver 4.1](http://go.microsoft.com/fwlink/?linkid=841533) 
     * [SQL Server용 Microsoft JDBC Driver 4.0](http://go.microsoft.com/fwlink/?linkid=841532)
  
-   Java Runtime Environment  
  
## <a name="java-runtime-environment-requirements"></a>Java Runtime Environment 요구 사항  
 SQL Server용 Microsoft JDBC Driver 4.2부터 Sun JDK(Java SE Development Kit) 8.0 및 JRE(Java Runtime Environment) 8.0이 지원됩니다. JDBC 4.1 및 4.2 API를 포함하도록 JDBC(Java Database Connectivity) 사양 API에 대한 지원이 확장되었습니다.  
  
 SQL Server용 Microsoft JDBC Driver 4.1부터는 Sun JDK(Java SE Development Kit) 7.0 및 JRE(Java Runtime Environment) 7.0이 지원됩니다.  
  
 부터는 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], JDBC 4.0 API를 포함 하도록 JDBC Java Database Connectivity () 사양 API에 대 한 지원이 확장 되었습니다. JDBC 4.0 API는 Sun Java SE Development Kit(API) JDK 6.0 및 Java Runtime Environment(JRE) 6.0에 새로 추가되었습니다. JDBC 4.0은 JDBC 3.0 API를 포함합니다.  
  
 배포 하는 경우는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Windows 및 UNIX 운영 체제 설치 패키지를 사용 해야 *sqljdbc_\<버전 > _enu.exe* 및 *sqljdbc_\<버전 > _ enu.tar.gz*각각. JDBC 드라이버를 배포 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버 배포](../../connect/jdbc/deploying-the-jdbc-driver.md) 항목입니다.  
  
**SQL Server 용 Microsoft JDBC Driver 6.2:**  
  
  JDBC 드라이버 6.2 각 설치 패키지에 두 개의 JAR 클래스 라이브러리가 포함: **mssql-jdbc-6.2.1.jre7.jar**, 및 **mssql-jdbc-6.2.1.jre8.jar**합니다. 
  
 JDBC 드라이버 6.2 작동 하며 모든 주요 Sun 호환 Java 가상 컴퓨터에서 지원 하도록 만들어졌지만 Sun JRE 5.0, 6.0, 7.0 및 8.0에 대해서만 테스트 됩니다. 
  
 SQL Server 용 Microsoft JDBC Driver 6.0 및 4.2에 포함 된 두 개의 JAR 파일에서 제공 하는 지원을 요약는 다음과 같습니다.  
  
|JAR|JDBC 버전 규격|권장 Java 버전|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.2.1.jre7.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE를 사용 하 여 예외가 6.0 또는 lower를 만들 throw 됩니다.<br /><br /> 6.2의 새로운 기능 포함: Linux, Kerberos, 도메인 간 인증에 Kerberos 제한 위임, 쿼리 제한 시간, 소켓 제한 시간은 자동 검색의 SPN에 대 한 영역에 대 한 사용자/암호 방법에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용 합니다. |  
|mssql-jdbc-6.2.1.jre8.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE를 사용 하 여 예외가 7.0 또는 lower를 만들 throw 됩니다.<br /><br /> 6.2의 새로운 기능 포함: Linux, Kerberos, 도메인 간 인증에 Kerberos 제한 위임, 쿼리 제한 시간, 소켓 제한 시간은 자동 검색의 SPN에 대 한 영역에 대 한 사용자/암호 방법에 대 한 Azure AD 인증 및 준비 문 핸들 다시 사용|    

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
|sqljdbc41.jar|4.1|7|JRE(Java Runtime Environment) 7.0이 필요합니다. JRE를 사용 하 여 예외가 6.0 또는 lower를 만들 throw 됩니다.<br /><br /> 6.0 및 4.2 패키지의 새로운 기능에는 JDBC 4.1 준수 및 대량 복사가 포함됩니다.<br /><br /> 또한 6.0 패키지에만의 새로운 기능 포함: Azure Active Directory 인증 상시 암호화, 테이블 반환 매개 변수를 투명 하 게 연결할 Always On 가용성 그룹을 개선에 대 한 매개 변수 메타 데이터 검색에 준비 쿼리 및 도메인 이름 IDN (Internationalized)|  
|sqljdbc42.jar|4.2|8|JRE(Java Runtime Environment) 8.0이 필요합니다. JRE를 사용 하 여 예외가 7.0 또는 lower를 만들 throw 됩니다.<br /><br /> 6.0 및 4.2 패키지의 새로운 기능에는 JDBC 4.1 준수, JDBC 4.2 준수 및 대량 복사가 포함됩니다.<br /><br /> 또한 6.0 패키지에만의 새로운 기능 포함: Azure Active Directory 인증 상시 암호화, 테이블 반환 매개 변수를 투명 하 게 연결할 Always On 가용성 그룹을 개선에 대 한 매개 변수 메타 데이터 검색에 준비 쿼리 및 도메인 이름 IDN (Internationalized)|  
  
 **SQL Server 용 Microsoft JDBC Driver 4.1:**  
  
 JDBC Driver 4.1의 각 설치 패키지 하나 JAR 클래스 라이브러리가 포함 됩니다.: **sqljdbc41.jar**합니다.  
    
|JAR|Description|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** 클래스 라이브러리는 JDBC 4.0 API에 대 한 지원을 제공 합니다. 모든 기능으로는 JDBC 4.0 드라이버는 JDBC 4.0 API 메서드가 포함 됩니다. JDBC 4.1은 지원되지 않습니다("SQLFeatureNotSupportedException" 예외가 발생함).<br /><br /> **sqljdbc41.jar** 클래스 라이브러리에는 환경 JRE (Java Runtime) 7.0이 필요 합니다. 사용 하 여 **sqljdbc41.jar** JRE 6.0 또는 5.0에서 예외가 throw 됩니다.<br /><br /> 
  
 JDBC 드라이버는 모든 주요 Sun 호환 Java 가상 컴퓨터에서 작동하고 지원되도록 설계되어 있지만 테스트는 Sun JRE 5.0, 6.0 및 7.0 이상에서 수행됩니다.  
  
 다음은 SQL Server 용 Microsoft JDBC Driver 4.1에 포함 된 JAR 파일에서 제공 된 지원에 대 한 요약입니다.  
  
|JAR|JDBC 버전|JRE(실행 가능)|JDK(컴파일 가능)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
 **SQL Server 용 Microsoft JDBC Driver 4.0:**  
  
 이전 버전과 호환성 및 가능한 업그레이드 시나리오를 지원 하려면 JDBC 드라이버 두 개의 JAR 클래스 라이브러리가 포함 되어의 각 설치 패키지: **sqljdbc.jar** 및 **sqljdbc4.jar**합니다.  
  
|JAR|Description|  
|---------|-----------------|  
|sqljdbc.jar|**sqljdbc.jar** 클래스 라이브러리는 JDBC 3.0을 지원 합니다.<br /><br /> **sqljdbc.jar** 클래스 라이브러리에는 Java 런타임 환경 (JRE) 버전 5.0이 필요 합니다. 사용 하 여 **sqljdbc.jar** on JRE 6.0 또는 JRE 7.0 데이터베이스에 연결할 때 예외를 throw 합니다.<br /><br /> **참고:** JDBC 드라이버가 JRE 1.4를 지원 하지 않습니다. JDBC 드라이버를 사용하려면 JRE 1.4를 JRE 5.0, JRE 6.0 또는 JRE 7.0으로 업그레이드해야 합니다. 응용 프로그램이 JDK 5.0 API 또는 JDK 6.0 API와 호환되지 않아 다시 컴파일해야 하는 경우도 있습니다. 자세한 내용은 Sun Microsystems 웹 사이트에 있는 설명서를 참조하세요.<br /><br /> [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]JDK 7을 지원 하지 않습니다.|  
|sqljdbc4.jar|**sqljdbc4.jar** 클래스 라이브러리는 JDBC 4.0 API에 대 한 지원을 제공 합니다. 기능을 모두 포함 된 **sqljdbc.jar** 새 JDBC 4.0 API 메서드가 뿐만 아니라 합니다.<br /><br /> **sqljdbc4.jar** 클래스 라이브러리에는 Java 런타임 환경 (JRE) 버전 6.0 또는 7.0이 필요 합니다. 사용 하 여 **sqljdbc4.jar** JRE 5.0에서 예외가 throw 됩니다.<br /><br /> **참고:** 사용 **sqljdbc4.jar** 응용 프로그램은 JDBC 4.0 API 기능을 사용 하지 않는 경우에 응용 프로그램이 JRE 6.0 또는 7.0에서 실행 해야 합니다는 경우.|  
  
 JDBC 드라이버는 모든 주요 Sun 호환 Java 가상 컴퓨터에서 작동하고 지원되도록 설계되어 있지만 테스트는 Sun JRE 5.0, 6.0 및 7.0 이상에서 수행됩니다.  
  
## <a name="sql-server-requirements"></a>SQL Server 요구 사항  
 JDBC 드라이버는 Azure SQL 데이터베이스 및 SQL Server에 대 한 연결을 지원합니다. SQL Server용 Microsoft JDBC Driver 4.2 및 4.1의 경우 SQL Server 2008에서 지원이 시작됩니다. SQL Server용 Microsoft JDBC Driver 4.0의 경우 SQL Server 2005에서 지원이 시작됩니다.  
  
## <a name="operating-system-requirements"></a>운영 체제 요구 사항  
 JDBC 드라이버는 JVM(Java Virtual Machine)의 사용을 지원하는 모든 운영 체제에서 작동하도록 설계되어 있지만 Sun Solaris, SUSE Linux 및 Windows 운영 체제에서만 공식적으로 테스트가 완료되었습니다.  
  
## <a name="supported-languages"></a>지원되는 언어  
 JDBC 드라이버는 모든 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 열 데이터 정렬이 있습니다. JDBC 드라이버에서 지 원하는 데이터 정렬에 대 한 자세한 내용은 참조 [JDBC 드라이버의 국제 기능](../../connect/jdbc/international-features-of-the-jdbc-driver.md)합니다.  
  
 데이터 정렬에 대 한 자세한 내용은 "데이터 정렬 사용"을 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

