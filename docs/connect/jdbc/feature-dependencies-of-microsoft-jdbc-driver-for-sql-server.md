---
title: SQL Server용 Microsoft JDBC Driver의 기능 종속성 | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b9d9fea0f211809fd65b65459d50daa7a85db88
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736954"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver의 기능 종속성

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 SQL Server 용 Microsoft JDBC Driver에 의존 하는 라이브러리를 나열 합니다. 프로젝트는 다음 종속성이 있습니다.

## <a name="compile-time"></a>컴파일 시간

 - `com.microsoft.azure:azure-keyvault`: 항상 암호화 Azure Key Vault 기능 (선택 사항)에 대 한 azure Key Vault Provider
 - `com.microsoft.azure:azure-keyvault-webkey`: 항상 암호화 Azure Key Vault 기능 (선택 사항)에 대 한 azure Key Vault Provider
 - `com.microsoft.azure:adal4j`: Azure Active Directory 인증 기능 및 (선택 사항) Azure Key Vault 기능에 대 한 Java 용 azure Active Directory 라이브러리
 - `com.microsoft.rest:client-runtime`: Azure Active Directory 인증 기능 및 (선택 사항) Azure Key Vault 기능에 대 한 Java 용 azure Active Directory 라이브러리
- `org.osgi:org.osgi.core`: OSGi 프레임 워크 지원 위한 OSGi 핵심 라이브러리입니다.
- `org.osgi:org.osgi.compendium`: OSGi 프레임 워크 지원 위한 OSGi 개론 라이브러리입니다.

## <a name="test-time"></a>테스트 시간

이전 기능 중 하나 필요로 하는 특정 프로젝트를 명시적으로 해당 POM 파일에 해당 종속성을 선언 해야 합니다.

**예를 들어:** 다시 선언 해야 하는 Azure Active Directory 인증 기능을 사용 하는 경우는 `adal4j` POM 파일 프로젝트의 종속성. 다음 코드 조각을 참조 하세요.

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.0.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>
```

**예를 들어:** 다시 선언 해야 하는 Azure Key Vault 기능을 사용 하는 경우는 `azure-keyvault` 종속성 및 `adal4j` POM 파일 프로젝트의 종속성. 다음 코드 조각을 참조 하세요.

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.0.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault-webkey</artifactId>
    <version>1.2.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC 드라이버 종속성 요구 사항

### <a name="working-with-the-azure-key-vault-provider"></a>Azure Key Vault 공급자를 사용 합니다.

- JDBC 드라이버 버전 7.2.0-종속성 버전: -Azure-keyvault (버전 1.2.0), Azure Keyvault Webkey (버전 1.2.0) Adal4j (1.6.3 버전), 클라이언트-런타임-에-AutoRest (1.6.5) 및 해당 종속성 ([샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample.md))
- JDBC 드라이버 버전 7.0.0-종속성 버전: -Azure-keyvault (버전 1.0.0) Adal4j (버전 1.6.0) 및 해당 종속성 ([샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample.md))
- JDBC 드라이버 버전 6.4.0-종속성 버전: -Azure-keyvault (버전 1.0.0) Adal4j (버전 1.4.0) 및 해당 종속성 ([샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 드라이버 버전 6.2.2-종속성 버전: -Azure-keyvault (버전 1.0.0) Adal4j (버전 1.4.0) 및 해당 종속성 ([샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 드라이버 버전 6.0.0-종속성 버전: -Azure-keyvault (버전 0.9.7) Adal4j (버전 1.3.0) 및 해당 종속성 ( [샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> 6.2.2 및 6.4.0 드라이버 버전을 사용 하 여 azure-keyvault-java 종속성 버전 1.0.0으로 업데이트 되었습니다. 그러나 새 버전 (0.9.7) 이전 버전과 호환 되지 및 드라이버의 기존 구현을 중단 합니다. 드라이버에서 새 구현을 Azure 키 자격 증명 모음 공급자를 사용 하는 클라이언트 프로그램에서 중단 하는 API를 변경 해야 합니다.
>
> 이 문제가 최신 드라이버 버전 (7.0.0)를 사용 하 여 해결 되었습니다. 인증 콜백 메커니즘을 사용 하는 제거 생성자는 이전 버전과 호환성을 위해 Azure Key Vault Provider에 다시 추가 됩니다.

### <a name="working-with-azure-active-directory-authentication"></a>Azure Active Directory 인증 사용

- JDBC 드라이버 버전 7.2.0-종속성 버전: Adal4j (1.6.3 버전), 클라이언트-런타임-에-AutoRest (1.6.5) 및 해당 종속성
- JDBC 드라이버 버전 7.0.0-종속성 버전: Adal4j (버전 1.6.0) 및 해당 종속성
- JDBC 드라이버 버전 6.4.0-종속성 버전: Adal4j (버전 1.4.0) 및 해당 종속성
- JDBC 드라이버 버전 6.2.2-종속성 버전: Adal4j (버전 1.4.0) 및 해당 종속성
- JDBC 드라이버 버전 6.0.0-종속성 버전: Adal4j (버전 1.3.0) 및 해당 종속성입니다. 이 버전의 드라이버를 사용 하 여 연결할 수 있습니다 _ActiveDirectoryIntegrated_ 인증 모드는 Windows 운영 체제 및 SQL Server (sqljdbc_auth.dll 및 Active Directory 인증 라이브러리를 사용 하 여만 ADALSQL 합니다. DLL)입니다.

드라이버 버전에서 6.4.0 부터는 응용 프로그램이 필요한 것은 아니며 ADALSQL를 사용 하 여 합니다. Windows 운영 체제에서 DLL입니다. 에 대 한 *비 Windows 운영 체제*, 드라이버가 ActiveDirectoryIntegrated 인증과 함께 작동 하도록 Kerberos 티켓을 요구 합니다. Kerberos를 사용 하 여 Active Directory에 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows, Linux 및 Mac에서 설정 하는 Kerberos 티켓](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)합니다.

에 대 한 *Windows 운영 체제*, 드라이버 sqljdbc_auth.dll 기본적으로 찾아 Kerberos 티켓 설정 또는 Azure 라이브러리 종속성이 필요 하지 않습니다. Sqljdbc_auth.dll을 사용할 수 없는 경우 다른 운영 체제에서 Active Directory에 인증 하는 것에 대 한 Kerberos 티켓에 대 한 드라이버를 찾습니다.

가져올 수 있습니다는 [샘플 응용 프로그램](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) 이 기능을 사용 하는 합니다.

## <a name="see-also"></a>관련 항목:

[JDBC 드라이버 GitHub 리포지토리](https://github.com/microsoft/mssql-jdbc)  
 [JDBC 드라이버 API 참조](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
