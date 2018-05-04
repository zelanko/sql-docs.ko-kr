---
title: SQL Server 용 Microsoft JDBC Driver의 종속성 기능 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
caps.latest.revision: 57
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 052628258ae1d8c1f31430ea132ed594a976be98
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server의 기능 종속성
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

 이 페이지에는 SQL Server 용 Microsoft JDBC Driver에 의존 하는 라이브러리의 목록을 포함 합니다. 프로젝트에는 다음과 같은 종속성.
 
 ## <a name="compile-time"></a>컴파일 시간
 - `azure-keyvault` : 항상 암호화 Azure 키 자격 증명 모음 기능 (선택 사항)에 대해 azure 키 자격 증명 모음 공급자
 - `adal4j` : Azure Active Directory 인증 기능 및 Azure 키 자격 증명 모음 기능은 (선택 사항)에 대 한 Java 용 azure active Directory 라이브러리

 ##  <a name="test-time"></a>테스트 시간
위의 두 가지 기능 중 하나 필요로 하는 특정 프로젝트의 pom 파일에서 해당 종속성을 명시적으로 선언 해야 합니다.

***예를 들어:*** 사용 중인 경우 *Azure Active Directory 인증 기능*, 다시 선언 해야 합니다 *adal4j* 프로젝트의 pom 파일에 대 한 종속성입니다. 다음 코드 조각은 참조 하십시오. 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>
```

***예를 들어:*** 사용 중인 경우 *Azure 키 자격 증명 모음 기능* 다시 선언 해야 *azure keyvault* 종속성 및 *adal4j* 종속성에 프로그램 프로젝트의 pom 파일입니다. 다음 코드 조각은 참조 하십시오. 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```
 
 ## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC 드라이버에 대 한 종속성 요구 사항

 ### <a name="azure-keyvault-feature"></a>Azure Keyvault 기능:
- JDBC 드라이버 버전 6.0.0 
    - 종속성 버전: Azure-Keyvault (0.9.7 버전), Adal4j (1.3.0 버전) 및 해당 종속성 ( [샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))
- JDBC 드라이버 버전 6.2.2 (최신 6.4.0 포함) 이상
    - 종속성 버전: Azure-Keyvault (버전 1.0.0), Adal4j (1.4.0 버전) 및 해당 종속성 ([샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))

> [!NOTE]
>   V6.2.2를 기준으로 azure-keyvault java 종속성 1.0.0 버전으로 업데이트 됩니다. 그러나 새 버전이 이전 버전 (버전 0.9.7)와 호환 되지 않습니다 및 따라서 기존 구현을 드라이버에서 중단 합니다. 드라이버에서 새 구현에 Azure 키 자격 증명 모음 기능을 사용 하는 클라이언트 프로그램을 중단 하는 API 변경 해야 합니다.

  
 ### <a name="azure-active-directory-authentication"></a>Azure Active Directory 인증:
- JDBC 드라이버 버전 6.0.0 
    - 종속성 버전: Adal4j (1.3.0 버전)과 해당 종속 항목
        - 이 버전의 드라이버에 연결할 수 있습니다를 사용 하 여 *ActiveDirectoryIntegrated* 운영 체제 및 sqljdbc_auth.dll 및 Active Directory 인증 라이브러리를 사용 하 여 SQL Server (에 대 한 windows 인증 모드 ADALSQL 합니다. DLL)입니다. 
- JDBC 드라이버 버전 6.4.0
    - 종속성 버전: Adal4j (버전 1.4.0)와 그 종속성
        - 이 버전의 드라이버에서 응용 프로그램 하지 않아도 ADALSQL 사용 됩니다. DLL입니다. 운영 체제에 따라. 에 대 한 **비 Windows 운영 체제**, 드라이버가 Kerberos 티켓 ActiveDirectoryIntegrated 인증과 함께 작동 하도록 요구 합니다. 참조 [Windows, Linux 및 Mac에서 설정 하는 Kerberos 티켓](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) 내용을 확인 합니다. 에 대 한 **Windows 운영 체제**, 기본적으로 드라이버에서는 sqljdbc_auth.dll 로드 되 고 Kerberos 티켓 설치 프로그램 또는 adal4j 종속성 필요 하지 않습니다. 그러나 sqljdbc_auth.dll 로드 되지 않은 경우 드라이버 작동 하며 동일한 방식으로 Windows 이외의 운영 체제 입력 한 다음 예제에 설명 된 설치 해야 합니다:이 기능을 사용 하 여 샘플 응용 프로그램을 찾을 수 있습니다 [여기](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) .

 ## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 GitHub 리포지토리](https://github.com/microsoft/mssql-jdbc)  
 [JDBC 드라이버 API 참조](../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  