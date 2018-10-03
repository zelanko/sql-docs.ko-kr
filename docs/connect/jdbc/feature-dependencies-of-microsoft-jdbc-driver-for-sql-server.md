---
title: Microsoft JDBC Driver for SQL Server의 기능 종속성 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61c66d192a158fb754563e2d103eba946dee47c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830361"
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server의 기능 종속성

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 페이지는 SQL Server 용 Microsoft JDBC Driver에 의존 하는 라이브러리를 나열 합니다. 프로젝트는 다음 종속성이 있습니다.

## <a name="compile-time"></a>컴파일 시간

- `azure-keyvault`: 항상 암호화 Azure Key Vault 기능 (선택 사항) azure Key Vault Provider
- `adal4j`: Azure Active Directory 인증 기능 및 (선택 사항) Azure Key Vault 기능에 대 한 Java 용 azure active Directory 라이브러리

## <a name="test-time"></a>테스트 시간

위의 두 기능 중 하나 필요로 하는 특정 프로젝트 pom 파일에서 해당 종속성을 명시적으로 선언 해야 합니다.

**_예를 들어:_**  사용 하는 경우 _Azure Active Directory 인증 기능_를 다시 선언 해야 _adal4j_ pom 파일 프로젝트의 종속성. 다음 코드 조각을 참조 하세요.

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>
```

**_예를 들어:_**  사용 하는 경우 _Azure Key Vault 기능_를 다시 선언 해야 _azure keyvault_ 종속성 및 _adal4j_ 프로젝트의 pom 파일에 종속성이 있습니다. 다음 코드 조각을 참조 하세요.

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC 드라이버 종속성 요구 사항

### <a name="working-with-azure-key-vault-provider"></a>Azure Key Vault 공급자를 사용 합니다.

- JDBC 드라이버 버전 7.0.0-종속성 버전: Azure-keyvault (버전 1.0.0), Adal4j (버전 1.6.0) 및 해당 종속성 ([샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-7-0-0.md))
- JDBC 드라이버 버전 6.4.0-종속성 버전: Azure-keyvault (버전 1.0.0), Adal4j (버전 1.4.0) 및 해당 종속성 ([샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 드라이버 버전 6.2.2-종속성 버전: Azure-keyvault (버전 1.0.0), Adal4j (버전 1.4.0) 및 해당 종속성 ([샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 드라이버 버전 6.0.0-종속성 버전: Azure-keyvault (버전 0.9.7), Adal4j (버전 1.3.0) 및 해당 종속성 ( [샘플 응용 프로그램](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> V6.2.2 및 v6.4.0 드라이버 버전을 사용 하 여 azure-keyvault-java 종속성 버전 1.0.0으로 업데이트 되었습니다. 그러나 새 버전 (버전 0.9.7) 이전 버전과 호환 되지 및 따라서 드라이버에는 기존 구현을 중단 합니다. 드라이버에서 새 구현을 Azure 키 자격 증명 모음 공급자를 사용 하는 클라이언트 프로그램에서 중단 하는 API를 변경 해야 합니다.

> 이 문제는 인증 콜백 메커니즘을 사용 하 여 제거 생성자에 추가 되므로 다시 Azure Key Vault 공급자에 대 한 이전 버전과 호환성 최신 드라이버 버전 v7.0.0를 사용 하 여 해결 되었습니다.

### <a name="working-with-azure-active-directory-authentication"></a>Azure Active Directory 인증 사용

- JDBC 드라이버 버전 7.0.0-종속성 버전: Ada4j (버전 1.6.0) 및 해당 종속성
- JDBC 드라이버 버전 6.4.0-종속성 버전: Adal4j (버전 1.4.0) 및 해당 종속성
- JDBC 드라이버 버전 6.2.2-종속성 버전: Adal4j (버전 1.4.0) 및 해당 종속성
- JDBC 드라이버 버전 6.0.0-종속성 버전: Adal4j (버전 1.3.0) 및 해당 종속성이 버전의 드라이버를 사용 하 여을 연결할 수 있습니다 _ActiveDirectoryIntegrated_ Windows 운영 체제에만 인증 모드 sqljdbc_auth.dll 및 Active Directory 인증 라이브러리를 사용 하 여 SQL server (ADALSQL 합니다. DLL)입니다.

드라이버 버전에서 6.4.0부터 응용 프로그램 필요한 것은 아니며 ADALSQL를 사용 하 여 합니다. Windows 운영 체제에서 DLL입니다. 에 대 한 **비 Windows 운영 체제**, 드라이버가 Kerberos 티켓 ActiveDirectoryIntegrated 인증과 함께 작동 하도록 요구 합니다. Kerberos를 사용 하 여 Active Directory에 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows, Linux 및 Mac에서 설정 하는 Kerberos 티켓](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)합니다.

에 대 한 **Windows 운영 체제**, 드라이버 sqljdbc_auth.dll 기본적으로 찾아 Kerberos 티켓 설정 또는 Azure 라이브러리 종속성이 필요 하지 않습니다. 그러나 sqljdbc_auth.dll을 사용할 수 없는 경우 다른 운영 체제에서 Active Directory에 인증 하는 것에 대 한 Kerberos 티켓에 대 한 드라이버가 찾습니다.

이 기능을 사용 하 여 샘플 응용 프로그램을 찾을 수 있습니다 [여기](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)합니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 GitHub 리포지토리](https://github.com/microsoft/mssql-jdbc)  
 [JDBC 드라이버 API 참조](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
