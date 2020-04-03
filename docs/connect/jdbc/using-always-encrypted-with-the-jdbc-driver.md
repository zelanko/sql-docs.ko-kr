---
title: Always Encrypted와 JDBC 드라이버 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37057985b6c552091d2989d56a13c52b0b0cf5ac
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80271329"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>상시 암호화와 JDBC 드라이버 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 페이지에서는 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 SQL Server용 Microsoft JDBC Driver 6.0(이상)을 사용하여 Java 애플리케이션을 개발하는 방법을 설명합니다.

상시 암호화를 사용하면 클라이언트가 중요한 데이터를 암호화하고 해당 데이터 또는 암호화 키를 SQL Server 또는 Azure SQL Database에 표시하지 않을 수 있습니다. SQL Server용 Microsoft JDBC Driver 6.0 이상과 같이 상시 암호화 지원 드라이버는 클라이언트 애플리케이션의 중요한 데이터를 투명하게 암호화하고 해독하여 이 동작을 구현합니다. 이 드라이버는 Always Encrypted 데이터베이스 열에 해당하는 쿼리 매개 변수를 자동으로 확인하고 SQL Server 또는 Azure SQL Database로 보내기 전에 이러한 매개 변수의 값을 암호화합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 [JDBC 드라이버에 대해 Always Encrypted API 참조](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항
- SQL Server용 Microsoft JDBC Driver 6.0 이상이 개발 컴퓨터에 설치되어 있는지 확인합니다. 
- Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files를 다운로드하여 설치합니다.  zip 파일에 포함된 추가 정보에서 설치 지침 및 가능한 내보내기/가져오기 문제와 관련된 자세한 내용을 읽어야 합니다.  

    - mssql-jdbc-X.X.X.jre7.jar 또는 sqljdbc41.jar를 사용하는 경우 [JCE(Java Cryptography Extension) Unlimited Strength Jurisdiction Policy Files 7 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)에서 정책 파일을 다운로드할 수 있습니다.

    - mssql-jdbc-X.X.X.jre8.jar 또는 sqljdbc42.jar를 사용하는 경우 [JCE(Java Cryptography Extension) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)에서 정책 파일을 다운로드할 수 있습니다.

    - mssql-jdbc-X.X.X.jre9.jar를 사용하는 경우에는 정책 파일을 다운로드할 필요가 없습니다. Java 9의 관할 정책은 기본적으로 무제한 수준 암호화로 설정됩니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업
암호화된 열에 대한 데이터를 암호화하거나 암호 해독하기 위해 SQL Server는 열 암호화 키를 유지 관리합니다. 열 암호화 키는 데이터베이스 메타데이터에 암호화된 형태로 저장됩니다. 각 열 암호화 키에는 열 암호화 키를 암호화하는 데 사용되는 해당 열 마스터 키가 있습니다. 데이터베이스 메타데이터에 열 마스터 키가 포함되어 있지 않습니다. 이러한 키는 클라이언트에서만 보유합니다. 그러나 데이터베이스 메타데이터에는 클라이언트와 관련하여 열 마스터 키가 저장되는 위치에 대한 정보가 포함됩니다. 예를 들어 데이터베이스 메타데이터가 열 마스터 키를 보유하는 키 저장소는 Windows 인증서 저장소이고 암호화 및 암호 해독에 사용되는 특정 인증서는 Windows 인증서 저장소 내의 특정 경로에 있다고 말할 수 있습니다. 클라이언트가 Windows 인증서 저장소에서 해당 인증서에 액세스할 수 있는 경우 인증서를 가져올 수 있습니다. 그런 다음 인증서를 사용하여 열 암호화 키의 암호를 해독할 수 있습니다. 그리고 해당 암호화 키를 통해 해당 열 암호화 키를 사용하는 암호화된 열의 데이터를 해독하거나 암호화할 수 있습니다.

SQL Server용 Microsoft JDBC Driver는 열 마스터 키 저장소 공급 기업을 사용하여 키 저장소와 통신합니다. 해당 공급 기업은 **SQLServerColumnEncryptionKeyStoreProvider**에서 파생된 클래스의 인스턴스입니다.

### <a name="using-built-in-column-master-key-store-providers"></a>기본 제공 열 마스터 키 저장소 공급자 사용
SQL Server용 Microsoft JDBC Driver에는 다음과 같은 기본 제공 열 마스터 키 저장소 공급자가 포함되어 있습니다. 이러한 공급자 중 일부는 공급자를 조회하는 데 사용되는 특정 공급자 이름으로 사전 등록되어 있으며 일부는 추가 자격 증명이나 명시적 등록이 필요합니다.

| 클래스                                                 | Description                                        | 공급자 (조회) 이름  | 사전 등록 여부 |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Azure Key Vault에 대한 키 저장소 공급자입니다. | AZURE_KEY_VAULT         | JDBC 드라이버 버전 7.4.1 이전의 경우 _아니요_, JDBC 드라이버 버전 7.4.1부터 _예_입니다. |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Windows 인증서 저장소에 대한 공급자입니다.      | MSSQL_CERTIFICATE_STORE | _예_                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Java 키 저장소 공급자입니다.                  | MSSQL_JAVA_KEYSTORE     | _예_                |
|||||

사전 등록된 키 저장소 제공자의 경우 이러한 공급자를 사용하기 위해 애플리케이션 코드를 변경할 필요는 없지만 다음 항목에 유의하세요.

- 사용자 또는 DBA는 열 마스터 키 메타데이터에 구성된 공급자 이름이 정확하고 열 마스터 키 경로가 특정 공급자에 대해 적합한 키 경로 형식을 준수하는지 확인해야 합니다. CREATE COLUMN MASTER KEY(Transact-SQL) 문을 실행할 때 적합한 공급자 이름 및 키 경로를 자동으로 생성하는 SQL Server Management Studio 등의 도구를 사용하여 키를 구성하는 것이 좋습니다.
- 애플리케이션에서 키 저장소의 키에 액세스할 수 있는지 확인합니다. 이 작업에는 키 저장소에 따라 애플리케이션 액세스를 키 및/또는 키 저장소에 부여하거나 기타 키 저장소 관련 구성 단계를 수행하는 작업이 포함될 수 있습니다. 예를 들어 SQLServerColumnEncryptionJavaKeyStoreProvider를 사용하려면 연결 속성에 키 저장소의 위치 및 암호를 제공해야 합니다. 

이러한 모든 키 저장소 공급자에 대한 자세한 내용은 다음 섹션을 참조하세요. Always Encrypted를 사용할 키 저장소 공급자를 하나만 구현하면 됩니다.

### <a name="using-azure-key-vault-provider"></a>Azure Key Vault 공급자 사용
Azure 주요 자격 증명 모음은 상시 암호화에 대한 열 마스터 키를 저장 및 관리하는 편리한 옵션입니다(특히 애플리케이션이 Azure에서 호스트되는 경우). SQL Server용 Microsoft JDBC Driver에는 Azure Key Vault에 키가 저장된 애플리케이션용 기본 제공 공급자인 SQLServerColumnEncryptionAzureKeyVaultProvider가 포함되어 있습니다. 이 공급자의 이름은 AZURE_KEY_VAULT입니다. Azure Key Vault 저장소 공급자를 사용하려면 애플리케이션 개발자가 Azure Key Vault에서 자격 증명 모음 및 키를 만들고 Azure Active Directory에서 앱 등록을 만들어야 합니다. 등록된 애플리케이션은 Always Encrypted와 함께 사용하기 위해 생성된 키 자격 증명 모음에 대해 정의된 액세스 정책에서 Get, Decrypt, Encrypt, Unwrap Key, Wrap Key 및 Verify 권한을 가져야 합니다. 키 자격 증명 모음을 설정하고 열 마스터 키를 만드는 방법에 대한 자세한 내용은 [Azure Key Vault - 단계별 가이드](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) 및 [Azure Key Vault에서 열 마스터 키 만들기](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault)를 참조하세요.

Azure Key Vault 공급자를 사용하는 경우, JDBC 드라이버가 열 마스터 키 경로를 신뢰할 수 있는 엔드포인트 목록과 비교하여 유효성을 검사합니다. 드라이버 버전 8.2.2부터 이 목록을 구성할 수 있습니다. 애플리케이션의 작업 디렉터리 안에 “mssql-jdbc.properties” 파일을 만들고 `AKVTrustedEndpoints` 속성을 세미콜론으로 구분된 목록으로 설정하세요. 값이 세미콜론으로 시작되면 기본 목록을 확장합니다. 그러지 않으면 기본 목록을 대체합니다.

이 페이지의 예에서 SQL Server Management Studio를 사용하여 Azure Key Vault 기반 열 마스터 키 및 열 암호화 키를 만든 경우 다시 만들기 위한 T-SQL 스크립트는 고유한 **KEY_PATH** 및 **ENCRYPTED_VALUE**에 대한 이 예와 유사할 수 있습니다.

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
);

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
);
```

JDBC 드라이버를 사용하는 애플리케이션은 Azure Key Vault를 사용할 수 있습니다. 이러한 Azure Key Vault 사용에 대한 구문 또는 문은 JDBC 드라이버 버전 7.4.1부터 변경되었습니다.

#### <a name="jdbc-driver-741-or-later"></a>JDBC 드라이버 7.4.1 이상

이 섹션에서는 JDBC 드라이버 버전 7.4.1 이상에 대해 설명합니다.

JDBC 드라이버를 사용하는 클라이언트 애플리케이션은 JDBC 연결 문자열에서 `keyVaultProviderClientId=<ClientId>;keyVaultProviderClientKey=<ClientKey>`를 언급하여 Azure Key Vault를 사용하도록 구성할 수 있습니다.

다음은 JDBC 연결 문자열에 이 구성 정보를 제공하는 예입니다.

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyVaultProviderClientId=<ClientId>;keyVaultProviderClientKey=<ClientKey>";
```
JDBC 드라이버는 연결 속성 중에 이러한 자격 증명이 있는 경우 **SQLServerColumnEncryptionAzureKeyVaultProvider** 개체를 자동으로 인스턴스화합니다.

#### <a name="jdbc-driver-version-prior-to-741"></a>7\.4.1 이전 JDBC 드라이버 버전

이 섹션에서는 7.4.1 이전 JDBC 드라이버 버전에 대해 설명합니다.

JDBC 드라이버를 사용하는 클라이언트 애플리케이션은 **SQLServerColumnEncryptionAzureKeyVaultProvider** 개체를 인스턴스화한 다음 해당 개체를 드라이버에 등록해야 합니다.

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID**는 Azure Active Directory 인스턴스에 있는 앱 등록의 애플리케이션 ID입니다. **clientKey**는 Azure Key Vault에 대한 API 액세스를 제공하는 해당 애플리케이션에 등록된 키 암호입니다.

애플리케이션에서 SQLServerColumnEncryptionAzureKeyVaultProvider의 인스턴스를 만든 후에는 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 메서드를 사용하여 해당 인스턴스를 드라이버에 등록해야 합니다. SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API를 호출하여 얻을 수 있는 기본 조회 이름인 AZURE_KEY_VAULT를 사용하여 인스턴스를 등록하는 것이 좋습니다. 기본 이름을 사용하면 SQL Server Management Studio 또는 PowerShell과 같은 도구를 사용하여 Always Encrypted 키를 프로비전하고 관리할 수 있습니다. 도구는 기본 이름을 사용하여 열 마스터 키에 대한 메타데이터 개체를 생성합니다. 다음 예에서는 Azure Key Vault 공급자를 등록하는 방법을 보여 줍니다. SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 메서드에 대한 자세한 내용은 [JDBC 드라이버에 대해 Always Encrypted API 참조](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조하세요.

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Azure Key Vault 키 저장소 공급자를 사용하는 경우 JDBC 드라이버의 Azure Key Vault 구현은 애플리케이션에 포함되어야 하는 이러한 라이브러리(GitHub)에 종속됩니다.
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Maven 프로젝트에 이러한 종속성을 포함시키는 방법에 대한 예는 [Apache Maven으로 ADAL4J 및 AKV 종속성 다운로드](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)를 참조하세요.

### <a name="using-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자 사용
SQLServerColumnEncryptionCertificateStoreProvider는 Windows 인증서 저장소에 열 마스터 키를 저장하는 데 사용될 수 있습니다. SSMS(SQL Server Management Studio) Always Encrypted 마법사 또는 기타 지원되는 도구를 사용하여 데이터베이스에서 열 마스터 키 및 열 암호화 키 정의를 만듭니다. 동일한 마법사를 사용하여 Windows 인증서 저장소에서 Always Encrypted 데이터에 대한 열 마스터 키로 사용할 수 있는 자체 서명된 인증서를 생성할 수 있습니다. 열 마스터 키 및 열 암호화 키 T-SQL 구문에 대한 자세한 내용은 각각 [열 마스터 키 만들기](../../t-sql/statements/create-column-master-key-transact-sql.md) 및 [열 암호화 키 만들기](../../t-sql/statements/create-column-encryption-key-transact-sql.md)를 참조하세요.

SQLServerColumnEncryptionCertificateStoreProvider의 이름은 MSSQL_CERTIFICATE_STORE이며 공급자 개체의 getName() API로 쿼리할 수 있습니다. 이 파일은 드라이버에 의해 자동으로 등록되며 애플리케이션을 변경하지 않고 원활하게 사용할 수 있습니다.

이 페이지의 예에서 SQL Server Management Studio를 사용하여 Windows 인증서 저장소 기반 열 마스터 키 및 열 암호화 키를 만든 경우 다시 만들기 위한 T-SQL 스크립트는 고유한 **KEY_PATH** 및 **ENCRYPTED_VALUE**에 대한 이 예와 유사할 수 있습니다.

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
);

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
);
```

> [!IMPORTANT]
> 이 문서의 다른 키 저장소 공급자는 드라이버가 지원하는 모든 플랫폼에서 사용 가능하지만 JDBC 드라이버의 SQLServerColumnEncryptionCertificateStoreProvider 구현은 Windows 운영 체제에서만 사용 가능합니다. 드라이버 패키지에서 사용할 수 있는 mssql-jdbc_auth-\<버전>-\<arch>.dll에 대한 종속성이 있습니다. 이 공급자를 사용하려면 mssql-jdbc_auth-\<버전>-\<arch>.dll 파일을 JDBC 드라이버가 설치된 컴퓨터의 Windows 시스템 경로에 있는 디렉터리에 복사합니다. 또는 java.library.path 시스템 속성을 설정하여 mssql-jdbc_auth-\<버전>-\<arch>.dll의 디렉터리를 지정할 수도 있습니다. 32비트 JVM(Java Virtual Machine)을 실행할 경우 운영 체제가 x64 버전이라도 x86 폴더에 있는 mssql-jdbc_auth-\<버전>-x86.dll 파일을 사용하세요. x64 프로세서에서 64비트 JVM을 실행할 경우 x64 폴더의 mssql-jdbc_auth-\<버전>-x64.dll 파일을 사용하세요. 예를 들어 32비트 JVM을 사용 중이고 JDBC 드라이버가 기본 디렉터리에 설치된 경우 Java 애플리케이션이 시작될 때 다음과 같은 VM(가상 머신) 인수를 사용하여 DLL의 위치를 지정할 수 있습니다. `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Java 키 저장소 공급자 사용
JDBC 드라이버는 Java 키 저장소를 위해 기본 제공된 키 저장소 공급자 구현을 제공합니다. **keyStoreAuthentication** 연결 문자열 속성이 연결 문자열에 존재하고 "JavaKeyStorePassword"로 설정된 경우 드라이버는 자동으로 인스턴스화하고 Java 키 저장소에 대한 공급자를 등록합니다. Java Key Store 공급자의 이름은 MSSQL_JAVA_KEYSTORE입니다. 이 이름은 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API를 사용하여 쿼리할 수도 있습니다. 

클라이언트 애플리케이션에서 드라이버의 Java 키 저장소 인증에 필요한 자격 증명을 지정하는 데 사용할 수 있는 연결 문자열 속성에는 세 가지가 있습니다. 드라이버는 연결 문자열에 있는 이 세 속성의 값을 기준으로 공급자를 초기화합니다.

**keyStoreAuthentication:** 사용할 Java 키 저장소를 식별합니다. SQL Server용 Microsoft JDBC Driver 6.0 이상에서는 이 속성을 통해서만 Java 키 저장소를 인증할 수 있습니다. Java 키 저장소의 경우 이 속성의 값은 `JavaKeyStorePassword`이어야 합니다.

**keyStoreLocation:** 열 마스터 키를 저장하는 Java 키 저장소 파일의 경로입니다. 경로에는 키 저장소 파일 이름이 포함됩니다.

**keyStoreSecret:** 키 저장소 및 키에 사용할 비밀/암호입니다. Java 키 저장소를 사용하는 경우에는 키 저장소와 키 암호가 동일해야 합니다.

다음은 연결 문자열에 이러한 자격 증명을 제공하는 예입니다.

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

SQLServerDataSource 개체를 사용하여 이러한 설정을 가져오거나 설정할 수도 있습니다. 자세한 내용은 [JDBC 드라이버에 대해 Always Encrypted API 참조](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조하세요.

JDBC 드라이버는 연결 속성 사이에 이러한 자격 증명이 있는 경우 SQLServerColumnEncryptionJavaKeyStoreProvider를 자동으로 인스턴스화합니다.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Java 키 저장소용 열 마스터 키 만들기
SQLServerColumnEncryptionJavaKeyStoreProvider는 JKS 또는 PKCS12 키 저장소 유형과 함께 사용할 수 있습니다. 이 공급자에서 사용할 키를 만들거나 가져오려면 Java [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) 유틸리티를 사용합니다. 키의 암호는 키 저장소와 동일해야 합니다. 다음은 keytool 유틸리티를 사용하여 공개 키와 연결된 프라이빗 키를 만드는 방법의 예입니다.

```console
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

이 명령은 공개 키를 만들고 이를 X.509 자체 서명 인증서로 래핑합니다. 이 인증서는 연결된 프라이빗 키와 함께 키 저장소 `keystore.jks`에 저장됩니다. 키 저장소의 이 항목은 `AlwaysEncryptedKey` 별칭으로 식별됩니다.

다음은 PKCS12 저장소 형식을 사용하는 동일한 예제입니다.

```console
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

키 저장소가 PKCS12 형식인 경우 keytool 유틸리티에 키 암호를 입력하라는 메시지가 표시되지 않으며 **SQLServerColumnEncryptionJavaKeyStoreProvider**에서는 키 저장소와 키의 암호가 동일해야 하므로 키 암호에 `-keypass` 옵션을 제공해야 합니다.

.pfx 형식으로 Windows 인증서 저장소에서 인증서를 내보내고 **SQLServerColumnEncryptionJavaKeyStoreProvider**와 함께 사용할 수도 있습니다. 내보낸 인증서는 JKS 키 저장소 형식으로 Java 키 저장소에 가져올 수도 있습니다.

keytool 항목을 만든 후 데이터베이스에 열 마스터 키 메타데이터를 만듭니다. 여기에는 키 저장소 공급자 이름과 키 경로가 필요합니다. 열 마스터 키 메타데이터를 만드는 방법에 대한 자세한 내용은 [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)를 참조하세요. SQLServerColumnEncryptionJavaKeyStoreProvider의 경우 키 경로는 키의 별칭이며 SQLServerColumnEncryptionJavaKeyStoreProvider의 이름은 `MSSQL_JAVA_KEYSTORE`입니다. SQLServerColumnEncryptionJavaKeyStoreProvider 클래스의 getName() 공용 API를 사용하여 이 이름을 쿼리할 수도 있습니다. 

열 마스터 키를 만드는 T-SQL 구문은 다음과 같습니다.

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
);
```

위에서 만든 'AlwaysEncryptedKey'의 경우 열 마스터 키 정의는 다음과 같습니다.

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
);
```

> [!NOTE]
> 기본 제공 SQL Server management Studio 기능은 Java 키 저장소에 대한 열 마스터 키 정의를 만들 수 없습니다. T-SQL 명령을 프로그래밍 방식으로 사용해야 합니다.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Java 키 저장소용 열 암호화 키 만들기
SQL Server Management Studio 또는 기타 도구는 Java 키 저장소에서 열 마스터 키를 사용하여 열 암호화 키를 만들 수 없습니다. 클라이언트 애플리케이션은 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스를 사용하여 프로그래밍 방식으로 열 암호화 키를 만들어야 합니다. 자세한 내용은 [열 마스터 키 저장소 공급자를 사용하여 프로그래밍 방식으로 키 프로비전](#using-column-master-key-store-providers-for-programmatic-key-provisioning)을 참조하세요.

### <a name="implementing-a-custom-column-master-key-store-provider"></a>사용자 지정 열 마스터 키 저장소 공급자 구현
기존 공급자에서 지원하지 않는 열 마스터 키를 키 저장소에 저장하려는 경우 SQLServerColumnEncryptionKeyStoreProvider 클래스를 확장하고 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 메서드를 사용하여 공급자를 등록하여 사용자 지정 공급자를 구현할 수 있습니다.

```java
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

공급자를 등록합니다.

```java
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>열 마스터 키 저장소 공급자를 사용하여 프로그래밍 방식으로 키 프로비전
암호화된 열에 액세스할 때 SQL Server용 Microsoft JDBC Driver는 올바른 열 마스터 키 저장소를 투명하게 찾고 호출하여 열 암호화 키의 암호를 해독합니다. 일반적으로 정상적인 애플리케이션 코드는 열 마스터 키 저장소 공급자를 직접 호출하지 않습니다. 그러나 프로그래밍 방식으로 공급자를 인스턴스화하고 호출하여 Always Encrypted 키를 프로비전하고 관리할 수 있습니다. 이 단계를 수행하여 예를 들어 암호화된 열 암호화 키를 생성하고 열 암호화 키를 부분 열 마스터 키 회전으로 해독할 수 있습니다. 자세한 내용은 [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.

사용자 지정 키 저장소 공급자를 사용하는 경우 고유한 키 관리 도구를 구현해야 할 수 있습니다. Windows 인증서 저장소 또는 Azure Key Vault에 저장된 키를 사용할 때는 SQL Server Management Studio 또는 PowerShell 등 기존 도구를 사용하여 키를 관리 및 프로비전할 수 있습니다. Java 키 저장소에 저장된 키를 사용하는 경우 프로그래밍 방식으로 키를 프로비전해야 합니다. 다음 예제에서는 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스를 사용하여 Java 키 저장소에 저장된 키로 키를 암호화하는 방법을 보여 줍니다.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted {
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<provide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of the column encryption key. The algorithm for the system providers must be
     * RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement();) {

            // Instantiate the Java Key Store provider.
            SQLServerColumnEncryptionKeyStoreProvider storeProvider = new SQLServerColumnEncryptionJavaKeyStoreProvider(keyStoreLocation,
                    keyStoreSecret);

            byte[] encryptedCEK = getEncryptedCEK(storeProvider);

            /**
             * Create column encryption key For more details on the syntax, see:
             * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql Encrypted column encryption key first needs
             * to be converted into varbinary_literal from bytes, for which byteArrayToHex() is used.
             */
            String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                    + columnEncryptionKey
                    + " WITH VALUES ( "
                    + " COLUMN_MASTER_KEY = "
                    + columnMasterKeyName
                    + " , ALGORITHM =  '"
                    + algorithm
                    + "' , ENCRYPTED_VALUE =  0x"
                    + byteArrayToHex(encryptedCEK)
                    + " ) ";
            statement.executeUpdate(createCEKSQL);
            System.out.println("Column encryption key created with name : " + columnEncryptionKey);
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException {
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(keyAlias, algorithm, plainCEK);

        return encryptedCEK;
    }

    public static String byteArrayToHex(byte[] a) {
        StringBuilder sb = new StringBuilder(a.length * 2);
        for (byte b : a)
            sb.append(String.format("%02x", b).toUpperCase());
        return sb.toString();
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>애플리케이션 쿼리에 대해 상시 암호화 사용
암호화된 열을 대상으로 하는 매개 변수의 암호화 및 쿼리 결과의 암호 해독을 설정하는 가장 쉬운 방법은 **columnEncryptionSetting** 연결 문자열 키워드 값을 **Enabled**로 설정하는 것입니다.

다음 연결 문자열은 JDBC 드라이버에서 Always Encrypted를 사용하는 예입니다.

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
```

다음 코드는 SQLServerDataSource 개체를 사용하는 동일한 예입니다.

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(<port>);
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

상시 암호화는 개별 쿼리에도 사용할 수 있습니다. 자세한 내용은 [Always Encrypted가 성능에 미치는 영향 제어](#controlling-the-performance-impact-of-always-encrypted)를 참조하세요. 암호화 또는 암호 해독을 위해 Always Encrypted를 사용하는 것은 적절하지 않습니다. 다음을 확인해야 합니다.
- 애플리케이션에는 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 데이터베이스 권한이 있으며 데이터베이스에서 상시 암호화 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 [상시 암호화의 사용 권한(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)을 참조하세요.
- 애플리케이션은 열 암호화 키를 보호하는 열 마스터 키에 액세스하여 쿼리된 데이터베이스 열을 암호화할 수 있습니다. Java 키 저장소 공급자를 사용하려면 연결 문자열에 추가 자격 증명을 제공해야 합니다. 자세한 내용은 [Java 키 저장소 공급자 사용](#using-java-key-store-provider)을 참조하세요.

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>java.sql.Time 값을 서버에 보내는 방식 구성
**sendTimeAsDatetime** 연결 속성은 java.sql.Time 값을 서버로 보내는 방식을 구성하는 데 사용됩니다. false로 설정하면 시간 값이 SQL Server 시간 형식으로 전송됩니다. true로 설정하면 시간 값이 날짜/시간 형식으로 전송됩니다. 시간 열이 암호화된 경우 암호화된 열은 시간에서 날짜/시간으로의 변환을 지원하지 않으므로 **sendTimeAsDatetime** 속성은 false여야 합니다. 또한 이 속성은 기본적으로 true이므로 암호화된 시간 열을 사용하는 경우 이 속성을 false로 설정해야 합니다. 그렇지 않으면 드라이버에서 예외가 발생합니다. 드라이버 6.0 버전부터 SQLServerConnection 클래스에는 이 속성 값을 프로그래밍 방식으로 구성하는 두 가지 메서드가 있습니다.
 
* public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

이 속성에 대한 자세한 내용은 [java.sql.Time 값을 서버에 보내는 방식 구성](configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조하세요.

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>문자열 값을 서버에 보내는 방식 구성
**sendStringParametersAsUnicode** 연결 속성은 문자열 값이 SQL Server로 전송되는 방법을 구성하는 데 사용됩니다. true로 설정하면 문자열 매개 변수가 유니코드 형식으로 서버에 전송됩니다. false로 설정하면 문자열 매개 변수가 유니코드가 아닌 ASCII 또는 MBCS 등의 형식으로 전송됩니다. 이 속성의 기본값은 true입니다. Always Encrypted가 사용 가능하고 char/varchar/varchar(max) 열이 암호화된 경우에는 **sendStringParametersAsUnicode**의 값을 false로 설정해야 합니다. 이 속성을 true로 설정하면 유니코드 문자를 포함하는 암호화된 char/varchar/varchar(max) 열에서 데이터를 해독할 때 드라이버가 예외를 throw합니다. 이 속성에 대한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정
애플리케이션 쿼리에 대해 Always Encrypted를 사용하도록 설정하면 표준 JDBC API를 사용하여 암호화된 데이터베이스 열의 데이터를 검색하거나 수정할 수 있습니다. 애플리케이션에 필요한 데이터베이스 사용 권한이 있고 열 마스터 키에 액세스할 수 있는 경우, 드라이버는 암호화된 열을 대상으로 하는 모든 쿼리 매개 변수를 암호화하고 암호화된 열에서 검색된 데이터를 해독합니다.

Always Encrypted를 사용하지 않는 경우 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패합니다. 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없는 경우 쿼리가 암호화된 열에서 데이터를 검색할 수 있습니다. 그러나 드라이버는 암호화된 열에서 검색된 값을 해독하지 않고 애플리케이션에서 암호화된 이진 데이터(바이트 배열)를 수신합니다.

다음 표에서는 상시 암호화 사용 여부에 따른 쿼리 동작을 요약합니다.

| 쿼리 특성                                                                           | 상시 암호화가 설정되고 애플리케이션에서 키 및 키 메타데이터에 액세스할 수 있는 경우                                                                                                                        | Always Encrypted가 설정되고 애플리케이션에서 키 또는 키 메타데이터에 액세스할 수 없는 경우 | 상시 암호화를 사용하지 않는 경우                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리                                           | 매개 변수 값이 투명하게 암호화됩니다.                                                                                                                                                           | Error                                                                             | Error                                                                                                               |
| 암호화된 열을 대상으로 하는 매개 변수 없이 암호화된 열에서 데이터를 검색하는 쿼리. | 암호화된 열의 결과가 투명하게 암호 해독됩니다. 애플리케이션에서 암호화된 열에 대해 구성된 SQL Server 형식에 해당하는 JDBC 데이터 형식의 일반 텍스트 값을 수신합니다. | Error                                                                             | 암호화된 열의 결과가 암호 해독되지 않습니다. 애플리케이션에서 암호화된 값을 바이트 배열(byte[])로 수신합니다. |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>암호화된 데이터 삽입 및 검색 예제

다음 예제에는 암호화된 열에서 데이터를 검색 및 수정하는 방법을 설명합니다. 이 예에서는 대상 테이블에 다음 스키마와 암호화된 SSN 및 BirthDate 열이 있다고 가정합니다. 이전 키 저장소 공급자 섹션에 설명된 대로 "MyCMK"라는 열 마스터 키와 "MyCEK"라는 열 암호화 키를 구성한 경우 이 스크립트를 사용하여 테이블을 만들 수 있습니다.

```sql
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY]);
 GO
```

각 Java 코드 예제에 대해 키 저장소 관련 코드를 표시된 위치에 삽입해야 합니다.

Azure Key Vault 키 저장소 공급자를 사용하는 경우:

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Windows 인증서 저장소 키 저장소 공급자를 사용하는 경우:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Java Key Store 키 저장소 공급자를 사용하는 경우:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>데이터 예제 삽입

이 예제에서는 Patients 테이블에 행을 삽입합니다. 다음 항목에 유의하세요.

- 샘플 코드에는 암호화에 대한 내용이 없습니다. SQL Server용 Microsoft JDBC Driver에서는 암호화된 열을 대상으로 하는 매개 변수를 자동으로 검색하고 암호화합니다. 이 동작을 통해 애플리케이션에 투명하게 암호화할 수 있습니다.
- 암호화된 열을 포함하여 데이터베이스 열에 삽입된 값은 SQLServerPreparedStatement를 사용하여 매개 변수로 전달됩니다. 매개 변수를 사용하여 암호화되지 않은 열에 값을 전달하는 것은 선택 사항이지만(그러나 SQL 삽입을 방지할 수 있으므로 매우 권장됨) 암호화된 열을 대상으로 하는 값에 필요합니다. 암호화된 열에 삽입된 값이 쿼리 문에 포함된 리터럴로 전달된 경우 드라이버에서 암호화된 대상 열의 값을 확인할 수 없어 값을 암호화하지 않으므로 쿼리가 실패합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.
- SQL Server용 Microsoft JDBC Driver는 암호화된 열에서 검색한 데이터의 암호를 투명하게 해독하므로 프로그램에서 인쇄한 모든 값은 일반 텍스트로 표시됩니다.
- WHERE 절을 사용하여 조회를 수행하는 경우 WHERE 절에 사용된 값을 매개 변수로 전달해야 드라이버가 데이터베이스로 보내기 전에 이를 투명하게 암호화할 수 있습니다. 다음 예제에서 SSN은 매개 변수로 전달되지만 LastName은 암호화되지 않으므로 LastName은 리터럴로 전달됩니다.
- SSN 열을 대상으로 하는 매개 변수에 사용된 setter 메서드는 setString()이며 char/varchar SQL Server 데이터 형식에 매핑됩니다. 이 매개 변수에 사용되는 setter 메서드가 nchar/nvarchar에 매핑되는 setNString()인 경우, Always Encrypted가 암호화된 nchar/nvarchar 값을 암호화된 char/varchar 값으로 변환하는 것을 지원하지 않으므로 쿼리가 실패합니다.

```java
// <Insert keystore-specific code here>
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement insertStatement = sourceConnection.prepareStatement("INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)")) {
    insertStatement.setString(1, "795-73-9838");
    insertStatement.setString(2, "Catherine");
    insertStatement.setString(3, "Abel");
    insertStatement.setDate(4, Date.valueOf("1996-09-10"));
    insertStatement.executeUpdate();
    System.out.println("1 record inserted.\n");
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>일반 텍스트 데이터 검색 예제

다음 예제에서는 암호화된 값을 기준으로 데이터를 필터링하고 암호화된 열에서 일반 텍스트 데이터를 검색하는 방법을 보여 줍니다. 다음 항목에 유의하세요.

- SQL Server용 Microsoft JDBC Driver가 데이터베이스로 전달하기 전에 투명하게 암호화할 수 있도록 SSN 열에서 필터링하기 위해 WHERE 절에 사용되는 값을 매개 변수로 전달해야 합니다.
- SQL Server용 Microsoft JDBC Driver는 SSN 및 BirthDate 열에서 검색한 데이터의 암호를 투명하게 해독하므로 프로그램에서 인쇄한 모든 값은 일반 텍스트로 표시됩니다.

> [!NOTE]
> 결정적 암호화를 사용하여 열을 암호화하는 경우 쿼리에서 동등 비교를 수행할 수 있습니다. 자세한 내용은 [상시 암호화(데이터베이스 엔진)의 결정적 또는 임의 암호화 선택](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)을 참조하세요.

```java
// <Insert keystore-specific code here>
try (Connection connection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection
                .prepareStatement("\"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;\"");) {
    selectStatement.setString(1, "795-73-9838");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-encrypted-data-example"></a>암호화된 데이터 검색 예제

Always Encrypted를 사용하지 않는 경우에도 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없으면 암호화된 열에서 데이터를 검색할 수 있습니다.

다음 예제에서는 암호화된 열에서 암호화된 이진 데이터를 검색하는 방법을 보여 줍니다. 다음 항목에 유의하세요.

- 연결 문자열에서는 Always Encrypted를 사용하지 않으므로 쿼리에서 SSN 및 BirthDate의 암호화된 값을 바이트 배열로 반환합니다(프로그램에서 값을 문자열로 변환).
- 암호화된 열을 대상으로 하는 매개 변수가 없으면 상시 암호화를 사용하지 않고 암호화된 열에서 데이터를 검색하는 쿼리에 매개 변수가 있을 수 있습니다. 다음 쿼리는 LastName을 기준으로 필터링되며 데이터베이스에서 암호화되지 않습니다. 쿼리가 SSN 또는 BirthDate를 기준으로 필터링되면 쿼리가 실패합니다.

```java
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = sourceConnection
                .prepareStatement("SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;");) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>암호화된 열 쿼리 시 일반적인 문제 방지

이 섹션에서는 Java 애플리케이션에서 암호화된 열을 쿼리할 때 발생하는 일반적인 오류 범주와 이를 방지하는 방법을 설명합니다.

### <a name="unsupported-data-type-conversion-errors"></a>지원되지 않는 데이터 형식 변환 오류

상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 지원되는 형식 변환의 자세한 목록은 [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. 데이터 형식 변환 오류를 방지하기 위해 수행할 수 있는 작업은 다음과 같습니다. 확인할 사항은 다음과 같습니다.

- 암호화된 열을 대상으로 하는 매개 변수의 값을 전달할 때 적절한 setter 메서드를 사용합니다. 매개 변수의 SQL Server 데이터 형식이 대상 열의 형식과 정확히 동일하거나 매개 변수의 SQL Server 데이터 형식이 열의 대상 형식으로 변환되는 것이 지원되는지 확인합니다. 특정 SQL Server 데이터 형식에 해당하는 매개 변수를 전달하기 위해 API 메서드가 SQLServerPreparedStatement, SQLServerCallableStatement 및 SQLServerResultSet 클래스에 추가되었습니다. 예를 들어 열이 암호화되지 않은 경우 setTimestamp() 메서드를 사용하여 매개 변수를 datetime2 또는 datetime 열에 전달할 수 있습니다. 그러나 열이 암호화된 경우에는 데이터베이스의 열 형식을 나타내는 정확한 메서드를 사용해야 합니다. 예를 들어 setTimestamp()를 사용하여 값을 암호화된 datetime2 열에 전달하고 setDateTime()을 사용하여 값을 암호화된 datetime 열에 전달합니다. 새 API의 전체 목록은 [JDBC 드라이버에 대해 Always Encrypted API 참조](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조하세요.
- SQL Server 데이터 형식이 decimal 및 numeric인 열을 대상으로 하는 매개 변수의 정밀도 및 배율이 대상 열에 대해 구성된 정밀도 및 배율과 동일해야 합니다. 10진 및 숫자 데이터 형식을 나타내는 매개 변수/열에 대한 데이터 값과 함께 정밀도 및 규모를 허용하기 위해 API 메서드가 SQLServerPreparedStatement, SQLServerCallableStatement 및 SQLServerResultSet 클래스에 추가되었습니다. 신규/오버로드된 API의 전체 목록은 [JDBC 드라이버에 대해 Always Encrypted API 참조](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조하세요.  
- 대상 열의 값을 수정하는 쿼리에서 SQL Server 데이터 형식이 datetime2, datetimeoffset 또는 time인 열을 대상으로 하는 매개 변수의 소수 초 정밀도/규모가 대상 열의 소수 초 정밀도/규모보다 크지 않아야 합니다. 이러한 데이터 형식을 나타내는 매개 변수에 대한 데이터 값과 함께 소수 초 정밀도/규모를 허용하기 위해 API 메서드가 SQLServerPreparedStatement, SQLServerCallableStatement 및 SQLServerResultSet 클래스에 추가되었습니다. 신규/오버로드된 API의 전체 목록은 [JDBC 드라이버에 대해 Always Encrypted API 참조](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조하세요.

### <a name="errors-due-to-incorrect-connection-properties"></a>잘못된 연결 속성으로 인한 오류

이 섹션에서는 Always Encrypted 데이터를 사용하도록 연결 설정을 적절히 구성하는 방법을 설명합니다. 암호화된 데이터 형식은 제한된 변환을 지원하기 때문에 암호화된 열을 사용할 때 **sendTimeAsDatetime** 및 **sendStringParametersAsUnicode** 연결 설정에 적절한 구성이 필요합니다. 확인할 사항은 다음과 같습니다.

- [sendTimeAsDatetime](setting-the-connection-properties.md) 연결 설정은 암호화된 시간 열에 데이터를 삽입할 때 false로 설정됩니다. 자세한 내용은 [java.sql.Time 값을 서버에 보내는 방식 구성](configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조하세요.
- [sendStringParametersAsUnicode](setting-the-connection-properties.md) 연결 설정은 암호화된 char/varchar/varchar(max) 열에 데이터를 삽입할 때 true(또는 기본값으로 유지)로 설정됩니다.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류

암호화된 열을 대상으로 하는 모든 값은 애플리케이션 내에서 암호화해야 합니다. 암호화된 열에서 삽입/수정하거나 일반 텍스트 값을 기준으로 필터링하면 다음과 같은 오류가 발생합니다.

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

이러한 오류를 방지하려면 다음을 확인합니다.

- 암호화된 열(연결 문자열 또는 특정 쿼리)을 대상으로 하는 애플리케이션 쿼리에 대해 Always Encrypted가 설정되어 있어야 합니다.
- 준비된 문 및 매개 변수를 사용하여 암호화된 열을 대상으로 하는 데이터를 전송합니다. 다음 예제에서는 내부 리터럴을 매개 변수로 전달하는 대신 암호화된 열(SSN)에서 리터럴/상수로 잘못 필터링한 쿼리를 보여 줍니다. 이 쿼리는 실패합니다.

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>입력 매개 변수에 암호화 적용

암호화 적용 기능은 Always Encrypted를 사용할 경우 매개 변수의 암호화를 적용합니다. 암호화가 강제 적용되고 SQL Server에서 매개 변수를 암호화할 필요가 없다고 드라이버에 알리는 경우 매개 변수를 사용하는 쿼리는 실패합니다. 이 속성은 데이터 노출을 야기할 수 있는 잘못된 암호화 메타데이터를 클라이언트에게 제공하는 손상된 SQL Server를 포함하는 보안 공격에 대한 추가 보호를 제공합니다. SQLServerPreparedStatement 및 SQLServerCallableStatement 클래스의 set* 메서드와 SQLServerResultSet 클래스의 update\* 메서드는 암호화 적용 설정을 지정하는 부울 인수를 수락하도록 오버로드됩니다. 이 인수의 값이 false이면 드라이버는 매개 변수를 강제로 암호화하지 않습니다. 암호화 적용을 true로 설정하면 지정 열이 암호화되고 연결 또는 문에서 Always Encrypted를 사용하도록 설정된 경우에만 쿼리 매개 변수가 설정됩니다. 이 속성을 사용하면 암호화될 것으로 예상되는 경우 드라이버가 실수로 SQL Server에 데이터를 일반 텍스트로 보내지 않도록 하는 추가 보안 계층이 제공됩니다.

암호화 적용 설정으로 오버로드된 SQLServerPreparedStatement 및 SQLServerCallableStatement 메서드에 대한 자세한 내용은 [JDBC 드라이버에 대해 Always Encrypted API 참조](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조하세요.  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어

Always Encrypted는 클라이언트 쪽 암호화 기술이므로 데이터베이스가 아닌 클라이언트 쪽에서 대부분의 성능 오버헤드가 발생합니다. 암호화 및 암호 해독 작업의 비용 외에 클라이언트 쪽 성능 오버헤드의 원인은 다음과 같습니다.

- 쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복
- 열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출

이 섹션에서는 SQL Server용 Microsoft JDBC Driver의 기본 제공 성능 최적화와 위의 두 성능 요소의 영향을 제어할 수 있는 방법에 대해 설명합니다.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대한 메타데이터를 검색하기 위한 왕복 제어

연결에 대한 상시 암호화가 설정된 경우 기본적으로 드라이버는 각 매개 변수화된 쿼리에 대해 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)을 호출하고 매개 변수 값 없이 쿼리 문을 SQL Server에 전달합니다. [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)은 쿼리 문을 분석하여 암호화해야 하는 매개 변수가 있는지 확인하고, 필요한 경우 드라이버에서 매개 변수 값을 암호화할 수 있도록 각 매개 변수에 대해 암호화 관련 정보를 반환합니다. 이 동작은 클라이언트 애플리케이션에 대한 높은 수준의 투명도를 보장합니다. 애플리케이션이 매개 변수를 사용하여 암호화된 열을 대상으로 하는 값을 드라이버에 전달하는 한, 애플리케이션(및 애플리케이션 개발자)은 암호화된 열에 액세스하는 쿼리에 유의할 필요가 없습니다.

### <a name="setting-always-encrypted-at-the-query-level"></a>쿼리 수준에서 상시 암호화 설정

매개 변수화된 쿼리의 암호화 메타데이터 검색을 위한 성능 영향을 제어하려면 연결이 아닌 개별 쿼리에 대해 상시 암호화를 설정합니다. 이렇게 하면 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리에 대해서만 sys.sp_describe_parameter_encryption을 호출할 수 있습니다. 단, 이 경우 암호화의 투명성이 저하될 수 있습니다. 데이터베이스 열의 암호화 속성을 변경한 경우 스키마 변경에 맞게 애플리케이션 코드를 변경해야 할 수 있습니다.

개별 쿼리의 Always Encrypted 동작을 제어하려면 해당 특정 문에 대해 암호화된 열을 읽고 쓸 때 데이터를 보내고 받는 방법을 지정하는 열거형 SQLServerStatementColumnEncryptionSetting을 전달하여 개별 문 개체를 구성해야 합니다. 다음은 몇 가지 유용한 지침입니다.

- 클라이언트 애플리케이션이 데이터베이스 연결을 통해 전송하는 대부분의 쿼리가 암호화된 열에 액세스하는 경우 다음 지침을 따릅니다.

    - **columnEncryptionSetting** 연결 문자열 키워드를 **Enabled**로 설정합니다.
    - 암호화된 열에 액세스하지 않는 개별 쿼리에 SQLServerStatementColumnEncryptionSetting.Disabled를 설정합니다. 이 설정은 sys.sp_describe_parameter_encryption이 호출되지 않고 결과 집합 값의 암호 해독도 시도되지 않도록 합니다.
    - 암호화를 요구하는 매개 변수가 없지만 암호화된 열에서 데이터를 검색하는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.ResultSet을 설정합니다. 이 설정은 sys.sp_describe_parameter_encryption 호출 및 매개 변수 암호화가 사용되지 않도록 합니다. 쿼리가 암호화 열에서 결과를 해독할 수 없습니다.

- 클라이언트 애플리케이션이 데이터베이스 연결을 통해 전송하는 대부분의 쿼리가 암호화된 열에 액세스하지 않는 경우 다음 지침을 따르세요.

    - **columnEncryptionSetting** 연결 문자열 키워드를 **Disabled**로 설정합니다.
    - 암호화해야 하는 모든 매개 변수가 있는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.Enabled를 설정합니다. 이 설정은 sys.sp_describe_parameter_encryption이 호출될 뿐만 아니라 암호화된 열에서 검색된 모든 쿼리 결과의 암호가 해독되도록 합니다.
    - 암호화를 요구하는 매개 변수가 없지만 암호화된 열에서 데이터를 검색하는 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.ResultSet을 설정합니다. 이 설정은 sys.sp_describe_parameter_encryption 호출 및 매개 변수 암호화가 사용되지 않도록 합니다. 쿼리가 암호화 열에서 결과를 해독할 수 없습니다.

SQLServerStatementColumnEncryptionSetting 설정을 사용하여 암호화를 우회하고 일반 텍스트 데이터에 액세스할 수는 없습니다. 문에서 열 암호화를 구성하는 방법에 대한 자세한 내용은 [JDBC 드라이버에 대해 Always Encrypted API 참조](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조하세요.  

다음 예제에서는 데이터베이스 연결에 대해 상시 암호화가 사용되지 않습니다. 애플리케이션에서 실행하는 쿼리에는 암호화되지 않은 LastName 열을 대상으로 하는 매개 변수가 있습니다. 쿼리는 암호화된 SSN 및 BirthDate 열에서 데이터를 검색합니다. 이러한 경우 암호화 메타데이터를 검색할 때 sys.sp_describe_parameter_encryption을 호출하지 않아도 됩니다. 그러나 애플리케이션에서 두 암호화된 열에서 일반 텍스트 값을 가져올 수 있도록 쿼리 결과에 대한 암호 해독을 설정해야 합니다. 이러한 기능을 위해 SQLServerStatementColumnEncryptionSetting.ResultSet 설정이 사용됩니다.

```java
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>;" 
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=<keyStoreLocation>" 
        + "keyStoreSecret=<keyStoreSecret>;";

String filterRecord = "SELECT FirstName, LastName, SSN, BirthDate FROM " + tableName + " WHERE LastName = ?";

try (SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection.prepareStatement(filterRecord, ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_READ_ONLY,
                connection.getHoldability(), SQLServerStatementColumnEncryptionSetting.ResultSetOnly);) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("First name: " + rs.getString("FirstName"));
        System.out.println("Last name: " + rs.getString("LastName"));
        System.out.println("SSN: " + rs.getString("SSN"));
        System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱

열 마스터 키 저장소에 대한 호출 수를 줄여 열 암호화 키의 암호를 해독하기 위해 SQL Server용 Microsoft JDBC Driver에서는 일반 텍스트 열 암호화 키를 메모리에 캐시합니다. 데이터베이스 메타데이터에서 암호화된 열 암호화 키 값을 받은 후 드라이버는 제일 먼저 암호화된 키 값에 해당하는 일반 텍스트 열 암호화 키를 찾습니다. 드라이버는 캐시에서 암호화된 열 암호화 키 값을 찾을 수 없는 경우에만 열 마스터 키가 포함된 키 저장소를 호출합니다.

SQLServerConnection 클래스에서 API, setColumnEncryptionKeyCacheTtl()을 사용하여 캐시의 열 암호화 키 항목에 대한 TTL(Time to Live) 값을 구성할 수 있습니다. 캐시의 열 암호화 키 항목에 대한 기본 TTL(Time to Live) 값은 2시간입니다. 캐싱을 해제하려면 값 0을 사용합니다. TTL(Time to Live) 값을 설정하려면 다음 API를 사용합니다.

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

예를 들어 TTL(Time to Live) 값을 10분으로 설정하려면 다음을 사용합니다.

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

DAYS, HOURS, MINUTES 또는 SECONDS만 시간 단위로 지원됩니다.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>SQLServerBulkCopy를 사용하여 암호화된 데이터 복사

SQLServerBulkCopy를 사용하면 데이터의 암호를 해독하지 않고 한 테이블에서 이미 암호화되어 저장된 데이터를 다른 테이블에 복사할 수 있습니다. 이러한 작업을 하려면 다음을 수행합니다.

- 대상 테이블의 암호화 구성이 원본 테이블의 구성과 일치하는지 확인합니다. 특히 두 테이블에 동일한 암호화 열이 있고 동일한 암호화 형식 및 암호화 키를 사용하여 열이 암호화되어야 합니다. 대상 열이 해당 원본 열과 다르게 암호화된 경우 복사 작업 후 대상 테이블의 데이터 암호를 해독할 수 없습니다. 데이터가 손상됩니다.
- 상시 암호화를 사용하지 않고 원본 테이블과 대상 테이블에 대한 데이터베이스 연결을 구성합니다.
- allowEncryptedValueModifications 옵션을 설정합니다. 자세한 내용은 [JDBC 드라이버에서 대량 복사 사용](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)을 참조하세요.

> [!NOTE]
> 이 옵션을 AllowEncryptedValueModifications로 지정하면 SQL Server용 Microsoft JDBC Driver는 데이터가 암호화되었는지 여부 또는 동일한 암호화 형식, 알고리즘 및 키를 대상 열로 사용하여 올바르게 암호화되었는지 확인하지 않아 데이터베이스가 손상될 수 있으므로 주의하여 사용합니다.

## <a name="see-also"></a>참고 항목

[Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
