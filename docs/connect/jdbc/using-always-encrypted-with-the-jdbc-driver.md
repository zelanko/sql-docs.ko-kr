---
title: JDBC 드라이버를 사용 하 여 상시 암호화를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 3/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 64
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c53479e3e94206645382e0c7b2d930a0b63075f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982267"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>상시 암호화와 JDBC 드라이버 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 페이지를 사용 하 여 Java 응용 프로그램을 개발 하는 방법에 대해 설명 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 Microsoft JDBC Driver 6.0 (또는 이상) SQL Server에 대 한 합니다.

상시 암호화를 사용하면 클라이언트가 중요한 데이터를 암호화하고 해당 데이터 또는 암호화 키를 SQL Server 또는 Azure SQL Database에 표시하지 않을 수 있습니다. SQL Server용 Microsoft JDBC Driver 6.0 이상과 같이 상시 암호화 지원 드라이버는 클라이언트 응용 프로그램의 중요한 데이터를 투명하게 암호화하고 해독하여 이 동작을 구현합니다. 드라이버는 쿼리를 자동으로 결정 매개 변수는 항상 암호화 데이터베이스 열에 해당 및 SQL Server 또는 Azure SQL Database로 데이터를 전송 하기 전에 이러한 매개 변수의 값을 암호화 합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 하 고 [Always Encrypted API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.

## <a name="prerequisites"></a>사전 요구 사항
- Microsoft JDBC Driver 있는지 확인 하십시오 6.0 (또는 이상) 개발 컴퓨터에서 SQL Server가 설치에 대 한 합니다. 
- Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files를 다운로드하여 설치합니다.  zip 파일에 포함된 추가 정보에서 설치 지침 및 가능한 내보내기/가져오기 문제와 관련된 자세한 내용을 읽어야 합니다.  

    - mssql-jdbc-X.X.X.jre7.jar 또는 sqljdbc41.jar를 사용하는 경우 [JCE(Java Cryptography Extension) Unlimited Strength Jurisdiction Policy Files 7 Download](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)에서 정책 파일을 다운로드할 수 있습니다.

    - mssql-jdbc-X.X.X.jre8.jar 또는 sqljdbc42.jar를 사용하는 경우 [JCE(Java Cryptography Extension) Unlimited Strength Jurisdiction Policy Files 8 Download](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)에서 정책 파일을 다운로드할 수 있습니다.

    - Mssql-jdbc X.X.X.jre9.jar를 사용 하는 경우 정책 파일이 없는 다운로드 해야 합니다. Java 9에서에서 법적으로 성인이 정책을 무제한 강력한 암호화 기본값으로 사용 됩니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업
SQL Server를 암호화 하거나 암호화 된 열에 대 한 데이터를 해독 하려면 열 암호화 키를 유지 합니다. 열 암호화 키는 데이터베이스 메타데이터에 암호화된 형태로 저장됩니다. 각 열 암호화 키에는 열 암호화 키를 암호화하는 데 사용되는 해당 열 마스터 키가 있습니다. 데이터베이스 메타 데이터는 열 마스터 키를 포함 하지 않습니다. 이러한 키는 클라이언트에서 보관만 됩니다. 그러나 데이터베이스 메타 데이터를 클라이언트 기준으로 열 마스터 키 저장 되는 위치에 대 한 정보를 포함지 않습니다. 예를 들어 데이터베이스 메타 데이터 표시 될 수도 있습니다는 키 저장소를 열 마스터 키가 Windows 인증서 저장소 및 암호화 및 암호 해독에 사용 된 특정 인증서는 Windows 인증서 저장소 내에서 특정 경로 보유 합니다. 클라이언트에 해당 인증서에 대 한 액세스는 Windows 인증서 저장소의 경우에 인증서를 얻을 수 있습니다. 그런 다음 인증서 열 암호화 키를 암호 해독에 사용할 수 있습니다. 그런 다음 암호를 해독 하거나 해당 열 암호화 키를 사용 하는 암호화 된 열에 대 한 데이터를 암호화 하는 암호화 키를 사용할 수 있습니다.

SQL Server 용 Microsoft JDBC Driver는 키 저장소를 사용 하 여에서 파생 된 클래스의 인스턴스는 열 마스터 키 저장소 공급자와 통신 **SQLServerColumnEncryptionKeyStoreProvider**합니다.

### <a name="using-built-in-column-master-key-store-providers"></a>기본 제공 열 마스터 키 저장소 공급자 사용
SQL Server 용 Microsoft JDBC Driver는 다음 기본 제공 열 마스터 키 저장소 공급자와 함께 제공 됩니다. (공급자 조회에 사용) 하는 특정 공급자 이름이 미리 등록 되어 이러한 공급자 중 일부 및 일부 추가 자격 증명이 나 명시적 등록 해야 합니다.

| 클래스 | 설명 | 공급자 (조회) 이름 |미리 등록 되어 있습니까?|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Azure Key Vault에 대 한 키 저장소에 대 한 공급자입니다.| AZURE_KEY_VAULT|아니오|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Windows 인증서 저장소에 대한 공급자입니다.|MSSQL_CERTIFICATE_STORE|사용자 계정 컨트롤
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Java 키 저장소 공급자|MSSQL_JAVA_KEYSTORE|사용자 계정 컨트롤|

미리 등록 된 키 저장소 공급자의 이러한 공급자를 사용 하려면 다음 항목이 응용 프로그램 코드를 변경 필요가 없습니다.

- 사용자 또는 DBA는 열 마스터 키 메타데이터에 구성된 공급자 이름이 정확하고 열 마스터 키 경로가 특정 공급자에 대해 적합한 키 경로 형식을 준수하는지 확인해야 합니다. CREATE COLUMN MASTER KEY(Transact-SQL) 문을 실행할 때 적합한 공급자 이름 및 키 경로를 자동으로 생성하는 SQL Server Management Studio 등의 도구를 사용하여 키를 구성하는 것이 좋습니다.
- 응용 프로그램에 키 저장소에서 키에 액세스할 수 있는지 확인 합니다. 이 작업에는 키 저장소에 따라 응용 프로그램 액세스를 키 및/또는 키 저장소에 부여하거나 기타 키 저장소 관련 구성 단계를 수행하는 작업이 포함될 수 있습니다. 예를 들어 SQLServerColumnEncryptionJavaKeyStoreProvider를 사용 해야 위치 및 연결 속성에서이 키 저장소의 암호를 제공 합니다. 

이러한 키 저장소 공급자의 모든 작업은 다음 섹션에서 자세히 설명 되어 있습니다. 상시 암호화를 사용 하려면 키 저장소 공급자를 구현 해야 합니다.

### <a name="using-azure-key-vault-provider"></a>Azure Key Vault 공급자 사용
Azure 주요 자격 증명 모음은 상시 암호화에 대한 열 마스터 키를 저장 및 관리하는 편리한 옵션입니다(특히 응용 프로그램이 Azure에서 호스트되는 경우). SQL Server 용 Microsoft JDBC Driver에는 Azure Key Vault에 저장 된 키가 있는 응용 프로그램에 대 한 기본 제공 공급자를 SQLServerColumnEncryptionAzureKeyVaultProvider, 포함 되어 있습니다. 이 공급자의 이름은 위해 AZURE_KEY_VAULT입니다. Azure Key Vault 저장소 공급자를 사용 하려면 응용 프로그램 개발자는 Azure Key Vault에 자격 증명 모음 및 키를 만들고 Azure Active Directory에 앱 등록을 만드는 해야 합니다. 등록된 된 응용 프로그램에는 부여, 암호 해독, 암호화, 키 래핑 해제, 키 래핑 및 확인 권한을 얻으려면 Always Encrypted 사용 하기 위해 만든 key vault에 대해 정의 된 액세스 정책에서를 사용 해야 합니다. 열 마스터 키를 만들고 key vault를 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [Azure Key Vault-단계별](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) 하 고 [Azure Key Vault에 열 마스터 키 만들기](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault)합니다.

Azure Key Vault를 만든 경우이 페이지의 예제에서 열 마스터 키와 SQL Server Management Studio를 사용 하 여 열 암호화 키를 기반에 대 한 T-SQL 스크립트를 다시 만드는 비슷할 수 있습니다는 고유한 자체를 사용 하 여이 예제에서는 **KEY_ 경로** 하 고 **ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
)
```

Azure Key Vault를 사용 하려면 클라이언트 응용 프로그램을 SQLServerColumnEncryptionAzureKeyVaultProvider 인스턴스화하고 드라이버를 사용 하 여 등록 해야 합니다.

초기화 SQLServerColumnEncryptionAzureKeyVaultProvider의 예는 다음과 같습니다.  

```
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID** 인스턴스에 Azure Active Directory 앱 등록의 응용 프로그램 ID입니다. **clientKey** Azure Key Vault에 대 한 API 액세스를 제공 하는 해당 응용 프로그램에서 키 암호 등록 됩니다.

응용 프로그램 SQLServerColumnEncryptionAzureKeyVaultProvider의 인스턴스를 만든 후 응용 프로그램 sqlserverconnection.registercolumnencryptionkeystoreproviders () 메서드를 사용 하 여 드라이버를 사용 하 여 인스턴스를 등록 해야 합니다. 인스턴스를 위해 AZURE_KEY_VAULT SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API를 호출 하 여 가져올 수 있는 기본 조회 이름을 사용 하 여 등록 되어 있는지 것이 좋습니다. 기본 이름을 사용 하 여 SQL Server Management Studio 또는 PowerShell과 같은 도구를 사용 하 여 프로 비전 (도구 열 마스터 키 메타 데이터 개체를 생성 하려면 기본 이름을 사용 하는 데 사용) 하는 Always Encrypted 키 관리를 수 있습니다. 다음 예제에서는 Azure Key Vault 공급자 등록 Sqlserverconnection.registercolumnencryptionkeystoreproviders () 메서드에 대 한 자세한 내용은 참조 하세요. [Always Encrypted API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Azure Key Vault 키 저장소 공급자를 사용 하는 경우 Azure Key Vault에 대 한 구현의 JDBC 드라이버 응용 프로그램을 사용 하 여 포함 되어야 합니다 (GitHub)에서 이러한 라이브러리에 종속성이 있습니다.
>
>  [java에 대 한 azure sdk](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-라이브러리-에-java 라이브러리](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Maven 프로젝트에 이러한 종속성을 포함 하는 방법의 예제를 참조 하세요. [다운로드 ADAL4J 및 AKV와의 종속성을 Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자를 사용 하 여
SQLServerColumnEncryptionCertificateStoreProvider는 Windows 인증서 저장소에 열 마스터 키를 저장하는 데 사용될 수 있습니다. SQL Server Management Studio (SSMS)는 Always Encrypted 마법사 또는 기타 지원 되는 도구를 사용 하 여 데이터베이스에 열 마스터 키와 열 암호화 키 정의 만들 수 있습니다. 상시 암호화 데이터에 대 한 열 마스터 키로 사용할 수 있는 Windows 인증서 저장소에 자체 서명 된 인증서를 생성 하려면 동일한 마법사를 사용할 수 있습니다. 열 마스터 키와 열 암호화 키 T-SQL 구문에 대 한 자세한 내용은 참조 하세요. [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) 하 고 [CREATE COLUMN ENCRPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 각각.

SQLServerColumnEncryptionCertificateStoreProvider 이름의 MSSQL_CERTIFICATE_STORE 이며 공급자 개체의 getName() API에서 쿼리할 수 있습니다. 드라이버에 의해 자동으로 등록 됩니다 하 고 응용 프로그램 변경 없이 원활 하 게 사용할 수 있습니다.

T-SQL 스크립트를 다시 만드는 특정 자체를사용하여이예제에서는비슷하게보일수있습니다Windows인증서저장소를만든경우이페이지의예제기반열마스터키및SQLServerManagementStudio를사용하여열암호화키,**KEY_PATH** 하 고 **ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
)
```

> [!IMPORTANT]
> 이 문서의 다른 키 저장소 공급자를 드라이버에서 지 원하는 모든 플랫폼에서 사용할 수 있지만 SQLServerColumnEncryptionCertificateStoreProvider 구현의 JDBC 드라이버는 Windows 운영 체제에만 제공 됩니다. 드라이버 패키지에서 사용할 수 있는 sqljdbc_auth.dll에서 종속성을 갖습니다. 이 공급자를 사용하려면 sqljdbc_auth.dll 파일을 JDBC 드라이버가 설치된 컴퓨터의 Windows 시스템 경로에 있는 디렉터리에 복사합니다. 또는 java.libary.path 시스템 속성에 sqljdbc_auth.dll의 디렉터리를 지정할 수도 있습니다. 32비트 JVM(Java Virtual Machine)을 실행할 경우 운영 체제가 x64 버전이라도 x86 폴더에 있는 sqljdbc_auth.dll 파일을 사용하십시오. x64 프로세서에서 64비트 JVM을 실행할 경우 x64 폴더의 sqljdbc_auth.dll 파일을 사용하십시오. 예를 들어 32비트 JVM을 사용 중이고 JDBC 드라이버가 기본 디렉터리에 설치된 경우 Java 응용 프로그램이 시작될 때 다음과 같은 VM(가상 머신) 인수를 사용하여 DLL의 위치를 지정할 수 있습니다. `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Java 키 저장소 공급자를 사용 하 여
JDBC 드라이버는 Java 키 저장소를 위해 기본 제공된 키 저장소 공급자 구현을 제공합니다. 경우는 **keyStoreAuthentication** 연결 문자열 속성은 연결 문자열에 "JavaKeyStorePassword"로 설정 되어를 드라이버에서 자동으로 인스턴스화합니다 하 고 Java 키 저장소에 대 한 공급자를 등록 합니다. Java 키 저장소 공급자의 이름은 MSSQL_JAVA_KEYSTORE입니다. 이 이름은 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API를 사용 하 여 쿼리할 수도 있습니다. 

드라이버 Java 키 저장소에 인증 해야 하는 자격 증명을 지정 하는 클라이언트 응용 프로그램을 허용 하는 세 가지 연결 문자열 속성이 있습니다. 드라이버는 연결 문자열에 이러한 세 속성의 값을 기반으로 하는 공급자를 초기화 합니다.

**keyStoreAuthentication:** Java 키 저장소를 사용 하 게 식별 합니다. Microsoft JDBC Driver for SQL Server 6.0 이상에이 속성을 통해 Java 키 저장소에 인증할 수 있습니다. Java 키 저장소의 경우이 속성의 값 이어야 합니다 `JavaKeyStorePassword`합니다.

**keyStoreLocation:** 열 마스터 키를 저장 하는 Java 키 저장소 파일의 경로입니다. 경로 키 저장소 파일 이름을 포함 합니다.

**keyStoreSecret:** 키 뿐만 아니라 keystore에 사용할 암호/암호. Java 키 저장소를 사용 하는 것에 대 한 키 저장소와 키 암호가 동일 해야 합니다.

연결 문자열에 이러한 자격 증명을 제공 하는 예는 다음과 같습니다.

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

가져올 하거나 SQLServerDataSource 개체를 사용 하 여 이러한 설정을 설정할 수도 있습니다. 자세한 내용은 [Always Encrypted API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.

JDBC 드라이버는 자동으로 이러한 자격 증명은 연결 속성에 있는 경우는 SQLServerColumnEncryptionJavaKeyStoreProvider를 인스턴스화합니다.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Java 키 저장소에 대 한 열 마스터 키 만들기
SQLServerColumnEncryptionJavaKeyStoreProvider JKS 또는 PKCS12 키 저장소 형식으로 사용할 수 있습니다. 만들기 또는 가져오기에이 공급자를 사용 하 여 사용할 키를 사용 하 여 Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) 유틸리티입니다. 키에는 자체 키 저장소와 동일한 암호를 있어야 합니다. 공개 키 및 keytool 유틸리티를 사용 하 여 연결된 된 개인 키를 만드는 방법의 예는 다음과 같습니다.

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

이 명령은 공개 키를 만들고 'keystore.jks' 연결된 된 개인 키와 함께 키 저장소에 저장 된 인증서를 자체 서명 된 X.509에 래핑합니다. 키 저장소에서이 항목은 'AlwaysEncryptedKey' 별칭으로 식별 됩니다.

사용 하 여 동일한 PKCS12 저장소 형식의 예는 다음과 같습니다.

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

키 저장소 PKCS12 형식의 경우 keytool 유틸리티 키 암호를 표시 하지 않습니다 및 키 암호를 키 저장소 및 키 동일 합니다 SQLServerColumnEncryptionJavaKeyStoreProvider 필요-keypass 옵션을 사용 하 여 제공 해야 합니다. 암호입니다.

또한.pfx 형식으로 Windows 인증서 저장소에서 인증서를 내보낼 수 있으며 SQLServerColumnEncryptionJavaKeyStoreProvider를 사용 하는. 내보낸된 인증서 JKS 키 저장소 형식으로 Java 키 저장소에 가져올 수도 있습니다.

Keytool 항목을 만든 후 키 저장소 공급자 이름 및 키 경로 데이터베이스에 열 마스터 키 메타 데이터를 만듭니다. 열 마스터 키 메타 데이터를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)합니다. SQLServerColumnEncryptionJavaKeyStoreProvider에 대 한 키 경로 키의 별칭만 이며는 SQLServerColumnEncryptionJavaKeyStoreProvider의 이름은 'MSSQL_JAVA_KEYSTORE'입니다. 또한 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스의 getName() 공용 API를 사용 하 여이 이름을 쿼리할 수 있습니다. 

열 마스터 키를 만들기 위한 T-SQL 구문은 다음과 같습니다.

```
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

'AlwaysEncryptedKey' 위에서 만든, 열 마스터 키 정의 됩니다.

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> 기본 제공 SQL Server management Studio 기능은 Java 키 저장소에 대 한 열 마스터 키 정의 만들 수 없습니다. 프로그래밍 방식으로 T-SQL 명령은 사용 해야 합니다.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Java 키 저장소에 대 한 열 암호화 키 만들기
열 암호화 키를 만드는 Java 키 저장소에 열 마스터 키를 사용 하 여 SQL Server Management Studio 또는 다른 도구를 사용할 수 없습니다. 클라이언트 응용 프로그램을 프로그래밍 방식으로 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스를 사용 하 여 열 암호화 키를 만들어야 합니다. 자세한 내용은 [프로그래밍 방식으로 키 프로 비전을 위한 열 마스터 키 저장소 공급자를 사용 하 여](#using-column-master-key-store-providers-for-programmatic-key-provisioning)입니다.

### <a name="implementing-a-custom-column-master-key-store-provider"></a>사용자 지정 열 마스터 키 저장소 공급자 구현
기존 공급자에서 지원하지 않는 열 마스터 키를 키 저장소에 저장하려는 경우 SQLServerColumnEncryptionKeyStoreProvider 클래스를 확장하고 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 메서드를 사용하여 공급자를 등록하여 사용자 지정 공급자를 구현할 수 있습니다.

```
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

```
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>열 마스터 키 저장소 공급자를 사용하여 프로그래밍 방식으로 키 프로비전
암호화된 열에 액세스할 때 SQL Server용 Microsoft JDBC Driver는 올바른 열 마스터 키 저장소를 투명하게 찾고 호출하여 열 암호화 키의 암호를 해독합니다. 일반적으로 정상적인 응용 프로그램 코드는 열 마스터 키 저장소 공급자를 직접 호출하지 않습니다. 그러나 인스턴스화 및 프로그래밍 방식으로 프로 비전 하 고 상시 암호화 키 관리 공급자를 호출할 수, 수 있습니다. 예를 들어 일부 열 마스터 키 회전으로 열 암호화 키를 암호 해독 및 암호화 된 열 암호화 키를 생성 하려면이 단계를 수행할 수 있습니다. 자세한 내용은 [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.

사용자 지정 키 저장소 공급자를 사용하는 경우 고유한 키 관리 도구를 구현해야 할 수 있습니다. Windows 인증서 저장소 또는 Azure Key Vault에 저장 된 키를 사용 하면 관리 키 프로 비전을 SQL Server Management Studio 또는 PowerShell과 같은 기존 도구를 사용할 수 있습니다. Java 키 저장소에 저장 된 키를 사용할 때 키를 프로그래밍 방식으로 프로 비전 해야 합니다. 다음 예제에서는 Java 키 저장소에 저장 된 키를 사용 하 여 키를 암호화 하려면 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스를 사용 하 여 보여 줍니다.

```
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<proide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider =
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key
                 * For more details on the syntax, see:
                 * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = "
                        + columnMasterKeyName
                        + " , ALGORITHM =  '"
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x"
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {
        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation :
         *      Path where keystore is located, including the keystore file name.
         * 2) keyStoreSecret :
         *      Password of the keystore and the key.
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>응용 프로그램 쿼리에 대해 상시 암호화 사용
암호화된 열을 대상으로 하는 매개 변수의 암호화 및 쿼리 결과의 암호 해독을 설정하는 가장 쉬운 방법은 **columnEncryptionSetting** 연결 문자열 키워드 값을 **Enabled**로 설정하는 것입니다.

다음 연결 문자열은 JDBC 드라이버에서 상시 암호화를 사용 하도록 설정의 예:

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
```

다음 코드는 SQLServerDataSource 개체를 사용 하는 동등한 예제가:

```
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

상시 암호화는 개별 쿼리에도 사용할 수 있습니다. 자세한 내용은 [상시 암호화의 성능 영향 제어](#controlling-the-performance-impact-of-always-encrypted)입니다. 암호화 또는 암호 해독을 위해 상시 암호화를 사용하는 것은 적절하지 않습니다. 다음을 확인해야 합니다.
- 응용 프로그램에는 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 데이터베이스 권한이 있으며 데이터베이스에서 상시 암호화 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 [상시 암호화의 사용 권한(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)을 참조하세요.
- 응용 프로그램은 열 암호화 키를 보호하는 열 마스터 키에 액세스하여 쿼리된 데이터베이스 열을 암호화할 수 있습니다. Java 키 저장소 공급자를 사용 하려면 연결 문자열에 추가 자격 증명을 제공 해야 합니다. 자세한 내용은 [사용 하 여 Java 키 저장소 공급자](#using-java-key-store-provider)합니다.

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>java.sql.Time 값을 서버에 보내는 방식 구성
합니다 **sendTimeAsDatetime** java.sql.Time 값을 서버로 보내는 방식을 구성할 연결 속성을 사용 합니다. 시간 값을 false로 설정 된 경우 SQL Server 시간 형식으로 전송 됩니다. 값이 날짜/시간 형식으로 전송 되는 시간을 true로 설정 하면 됩니다. 시간 열을 암호화 합니다 **sendTimeAsDatetime** 암호화 된 열 시간에서 날짜/시간 변환을 지원 하지 속성이 false 여야 합니다. False로 설정 해야 암호화 된 시간 열을 사용 하는 경우이 속성이 기본값인 true로 설정 하 여 이므로 참고도 선택 합니다. 그렇지 않으면 드라이버는 예외가 throw 됩니다. 드라이버의 버전 6.0 이상에서는 SQLServerConnection 클래스에이 속성의 값을 프로그래밍 방식으로 구성 하는 두 가지 방법 있습니다.
 
* public void setSendTimeAsDatetime (부울 sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

이 속성에 대 한 자세한 내용은 참조 하세요. [어떻게 구성 java.sql.Time 값을 서버로 전송 됩니다](configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>문자열 값에는 서버에 보내는 방식 구성
합니다 **sendStringParametersAsUnicode** 연결 속성은 문자열 값에 SQL Server로 보내는 방식 구성 하는 데 사용 됩니다. true로 설정하면 문자열 매개 변수가 유니코드 형식으로 서버에 전송됩니다. 경우 문자열 매개 변수를 false로 설정 예: ASCII 또는 유니코드 대신 MBCS 유니코드가 아닌 형식으로 전송 됩니다. 이 속성의 기본값은 true입니다. 상시 암호화 사용 시점과 char/varchar/varchar(max) 열이 암호화의 가치 **sendStringParametersAsUnicode** false로 설정 해야 합니다. 이 속성 설정 된 경우 true, 드라이버 예외가 throw 됩니다 유니코드 문자가 포함 된 암호화 된 char/varchar/varchar(max) 열에서 데이터를 암호 해독 하는 경우. 이 속성에 대 한 자세한 내용은 참조 하세요. [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)합니다.
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정
응용 프로그램 쿼리에 대해 상시 암호화를 사용 하면 암호화 된 데이터베이스 열에 데이터를 검색 하거나 수정할 표준 JDBC Api를 사용할 수 있습니다. 응용 프로그램에 필요한 데이터베이스 권한이 있고 열 마스터 키에 액세스할 수, 하는 경우 드라이버는 암호화 된 열을 대상 암호화 된 열에서 검색 한 데이터를 해독 하는 쿼리 매개 변수를 암호화 됩니다.

상시 암호화를 사용하지 않는 경우 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패합니다. 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없는 경우 쿼리가 암호화된 열에서 데이터를 검색할 수 있습니다. 그러나 드라이버는 암호화된 열에서 검색된 값을 해독하지 않고 응용 프로그램에서 암호화된 이진 데이터(바이트 배열)를 수신합니다.

다음 표에서는 상시 암호화 사용 여부에 따른 쿼리 동작을 요약합니다.

|쿼리 특성 | 상시 암호화가 설정되고 응용 프로그램에서 키 및 키 메타데이터에 액세스할 수 있는 경우|상시 암호화가 설정되고 응용 프로그램에서 키 또는 키 메타데이터에 액세스할 수 없는 경우 | 상시 암호화를 사용하지 않는 경우|
|:---|:---|:---|:---|
| 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리 | 매개 변수 값이 투명하게 암호화됩니다. | Error | Error|
| 암호화된 열을 대상으로 하는 매개 변수 없이 암호화된 열에서 데이터를 검색하는 쿼리.| 암호화된 열의 결과가 투명하게 암호 해독됩니다. 응용 프로그램에서 암호화된 열에 대해 구성된 SQL Server 형식에 해당하는 JDBC 데이터 형식의 일반 텍스트 값을 수신합니다. | Error | 암호화된 열의 결과가 암호 해독되지 않습니다. 응용 프로그램에서 암호화된 값을 바이트 배열(byte[])로 수신합니다.

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>암호화 된 데이터 예제 삽입 및 검색 
다음 예제에는 암호화된 열에서 데이터를 검색 및 수정하는 방법을 설명합니다. 예제에서는 다음 스키마와 암호화 된 SSN 및 BirthDate 열을 사용 하 여 대상 테이블을 가정 합니다. 명명 된 열 마스터 키를 구성한 경우 "MyCMK" 및 열 암호화 키 이름이 "MyCEK" (위의 키 저장소 공급자 섹션에서 설명)으로,이 스크립트를 사용 하 여 테이블을 만들 수 있습니다.

```
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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

각 Java 코드 예제에 명시 된 위치에 키 저장소 관련 코드를 삽입 해야 합니다.

Azure Key Vault 키 저장소 공급자로 사용 하는 경우

```
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Windows 인증서 저장소 키 저장소 공급자를을 사용 하는 경우

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Java 키 저장소 키 저장소 공급자를을 사용 하는 경우

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>데이터 예제 삽입
이 예제에서는 Patients 테이블에 행을 삽입합니다. 다음 항목에 유의하세요.
- 샘플 코드에는 암호화에 대한 내용이 없습니다. SQL Server 용 Microsoft JDBC Driver는 자동으로 검색 하 고 암호화 된 열을 대상으로 하는 매개 변수를 암호화 합니다. 이 동작을 통해 응용 프로그램에 투명하게 암호화할 수 있습니다.
- 암호화 된 열을 포함 하 여 데이터베이스 열에 삽입 된 값은 SQLServerPreparedStatement를 사용 하 여 매개 변수로 전달 됩니다. 매개 변수를 사용하여 암호화되지 않은 열에 값을 전달하는 것은 선택 사항이지만(그러나 SQL 삽입을 방지할 수 있으므로 매우 권장됨) 암호화된 열을 대상으로 하는 값에 필요합니다. 암호화 된 열에 삽입 된 값 쿼리 문에 포함 된 리터럴로 전달 하는 경우 드라이버는 대상 암호화 된 열에서 값을 확인할 수 없으며 값을 암호화 하지 때문에 쿼리가 실패 합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.
- SQL Server 용 Microsoft JDBC 드라이버는 암호화 된 열에서 검색 한 데이터 암호 해독 투명 하 게 프로그램이 인쇄 하는 모든 값, 일반 텍스트로 됩니다.
- WHERE 절을 드라이버 투명 하 게 암호화할 수는 데이터베이스에 보내기 전에 되도록 매개 변수로 전달할 해야 하는 WHERE 절에 사용 된 값을 사용 하 여 조회 수행 하려는 경우 합니다. 다음 예의 SSN 매개 변수로 전달 됩니다 있지만 LastName 암호화 되지 않은 성 리터럴로 전달 됩니다.
- SSN 열을 대상으로 하는 매개 변수에 대해 사용 되는 setter 메서드 setString() char/varchar SQL Server 데이터 형식에 매핑되는 경우 이 매개 변수에 사용되는 setter 메서드가 nchar/nvarchar에 매핑되는 setNString()인 경우, 상시 암호화가 암호화된 nchar/nvarchar 값을 암호화된 char/varchar 값으로 변환하는 것을 지원하지 않으므로 쿼리가 실패합니다.

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))
        {
            insertStatement.setString(1, "795-73-9838");
            insertStatement.setString(2, "Catherine");
            insertStatement.setString(3, "Abel");
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));
            insertStatement.executeUpdate();
            System.out.println("1 record inserted.\n");
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>일반 텍스트 데이터 검색 예제
다음 예제에서는 암호화된 값을 기준으로 데이터를 필터링하고 암호화된 열에서 일반 텍스트 데이터를 검색하는 방법을 보여 줍니다. 다음 항목에 유의하세요.
- SQL Server용 Microsoft JDBC Driver가 데이터베이스로 전달하기 전에 투명하게 암호화할 수 있도록 SSN 열에서 필터링하기 위해 WHERE 절에 사용되는 값을 매개 변수로 전달해야 합니다.
- SQL Server용 Microsoft JDBC Driver는 SSN 및 BirthDate 열에서 검색한 데이터의 암호를 투명하게 해독하므로 프로그램에서 인쇄한 모든 값은 일반 텍스트로 표시됩니다.

> [!NOTE]
> 결정적 암호화를 사용하여 열을 암호화하는 경우 쿼리에서 동등 비교를 수행할 수 있습니다. 자세한 내용은 [상시 암호화(데이터베이스 엔진)의 결정적 또는 임의 암호화 선택](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)을 참조하세요.

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";
    
        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "795-73-9838");
            ResultSet rs = selectStatement.executeQuery();
            while(rs.next())
            {
                System.out.println("SSN: " +rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName")+
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>암호화된 데이터 검색 예제
상시 암호화를 사용하지 않는 경우에도 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없으면 암호화된 열에서 데이터를 검색할 수 있습니다.

다음 예제에서는 암호화된 열에서 암호화된 이진 데이터를 검색하는 방법을 보여 줍니다. 다음 항목에 유의하세요.
- 연결 문자열에서는 상시 암호화를 사용하지 않으므로 쿼리에서 SSN 및 BirthDate의 암호화된 값을 바이트 배열로 반환합니다(프로그램에서 값을 문자열로 변환).
- 암호화된 열을 대상으로 하는 매개 변수가 없으면 상시 암호화를 사용하지 않고 암호화된 열에서 데이터를 검색하는 쿼리에 매개 변수가 있을 수 있습니다. 다음 쿼리는 LastName을 기준으로 필터링되며 데이터베이스에서 암호화되지 않습니다. 쿼리가 SSN 또는 BirthDate를 기준으로 필터링되면 쿼리가 실패합니다.

```
try
{
    String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;";

        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "Abel");
            ResultSet rs = selectStatement.executeQuery();
            while (rs.next())
            {
                System.out.println("SSN: " + rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName") +
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>암호화된 열 쿼리 시 일반적인 문제 방지
이 섹션에서는 Java 응용 프로그램에서 암호화된 열을 쿼리할 때 발생하는 일반적인 오류 범주와 이를 방지하는 방법을 설명합니다.

### <a name="unsupported-data-type-conversion-errors"></a>지원되지 않는 데이터 형식 변환 오류
상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 지원되는 형식 변환의 자세한 목록은 [상시 암호화(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. 데이터 형식 변환 오류를 방지하기 위해 수행할 수 있는 작업은 다음과 같습니다. 다음 사항을 확인 합니다

- 암호화 된 열을 대상으로 하는 매개 변수 값을 전달 하는 경우에 적절 한 setter 메서드를 사용 합니다. SQL Server 데이터 형식의 매개 변수는 정확 하 게 대상 열의 형식과 같은 열의 대상 형식으로 매개 변수의 SQL Server 데이터 형식의 변환이 지원 확인 합니다. API 메서드가 특정 SQL Server 데이터 형식에 해당 하는 매개 변수를 전달 하려면 SQLServerPreparedStatement, SQLServerCallableStatement와 및 SQLServerResultSet 클래스에 추가 되었습니다. 예를 들어, 열 암호화 되어 있지 않으면 setTimestamp() 메서드를 사용 하 여는 datetime2 또는 날짜/시간 열의 매개 변수를 전달 합니다. 하지만 열 암호화 된 경우 데이터베이스의 열 형식을 나타내는 정확한 메서드를 사용 해야 합니다. 예를 들어 setTimestamp() 사용 하 여 암호화 된 datetime2 열에 값을 전달할를 setDateTime()를 사용 하 여 암호화 된 datetime 열에 값을 전달 합니다. 참조 [Always Encrypted API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) 목록은 새로운 Api에 대 한 합니다.
- SQL Server 데이터 형식이 decimal 및 numeric인 열을 대상으로 하는 매개 변수의 정밀도 및 배율이 대상 열에 대해 구성된 정밀도 및 배율과 동일해야 합니다. API 메서드가 전체 자릿수 및 소수 10 진수 및 숫자 데이터 형식을 나타내는 매개 변수/열에 대 한 데이터 값과 함께 적용할 SQLServerPreparedStatement, SQLServerCallableStatement와 및 SQLServerResultSet 클래스에 추가 되었습니다. 참조 [Always Encrypted API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) 오버 로드/새 api 목록은 합니다.  
- datetime2, datetimeoffset 또는 time SQL Server 데이터 형식 열을 대상으로 하는 매개 변수의 소수 자릿수 초의 정밀도/소수 대상 열의 값을 수정 하는 쿼리에서 대상 열에 대 한 초 소수 부분 정밀도/소수 보다 크지 않습니다. . API 메서드가 이러한 데이터 형식을 나타내는 매개 변수에 대 한 데이터 값과 함께 소수 자릿수 초의 정밀도/소수 적용할 SQLServerPreparedStatement, SQLServerCallableStatement와 및 SQLServerResultSet 클래스에 추가 되었습니다. 오버 로드/새 Api의 전체 목록은 참조 하세요 [Always Encrypted API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.   

### <a name="errors-due-to-incorrect-connection-properties"></a>잘못 된 연결 속성으로 인 한 오류
이 섹션에는 상시 암호화 데이터를 사용 하 여 적절 하 게 연결 설정을 구성 하는 방법을 설명 합니다. 암호화 된 데이터 형식 제한 된 변환을 지원 하므로 합니다 **sendTimeAsDatetime** 하 고 **sendStringParametersAsUnicode** 연결 설정을 암호화 된 열을 사용 하는 경우 적절 한 구성이 필요 합니다. 다음 사항을 확인 합니다 
- [sendTimeAsDatetime](setting-the-connection-properties.md) 시간 열을 암호화 된 데이터를 삽입 하는 경우 연결 설정이 false로 설정 됩니다. 자세한 내용은 [java.sql.Time 값을 서버로 보내는 방식 구성](configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.
- [sendStringParametersAsUnicode](setting-the-connection-properties.md) 연결 설정이 true (또는 기본값으로 그대로) 데이터를 삽입 char/varchar/varchar(max) 열을 암호화 하는 경우.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류
암호화된 열을 대상으로 하는 모든 값은 응용 프로그램 내에서 암호화해야 합니다. 암호화된 열에서 삽입/수정하거나 일반 텍스트 값을 기준으로 필터링하면 다음과 같은 오류가 발생합니다.

```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

이러한 오류를 방지하려면 다음을 확인합니다.
- 암호화된 열(연결 문자열 또는 특정 쿼리)을 대상으로 하는 응용 프로그램 쿼리에 대해 상시 암호화가 설정되어 있어야 합니다.
- 준비 된 문을 사용 하 고 암호화 된 열을 데이터 대상으로 보낼 매개 변수. 다음 예제에서는 내부 리터럴을 매개 변수로 전달하는 대신 암호화된 열(SSN)에서 리터럴/상수로 잘못 필터링한 쿼리를 보여 줍니다. 이 쿼리는 실패 합니다.

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>입력된 매개 변수에서 암호화를 강제 적용
상시 암호화를 사용 하는 경우 매개 변수의 암호화를 적용 하는 암호화 기능입니다. 암호화를 사용하도록 적용하고 SQL Server가 매개 변수를 암호화하지 않아도 되는 것을 드라이버에 알리는 경우 매개 변수를 사용하는 쿼리는 실패합니다. 이 속성은 데이터 노출을 야기할 수 있는 잘못된 암호화 메타데이터를 클라이언트에게 제공하는 손상된 SQL Server를 포함하는 보안 공격에 대한 추가 보호를 제공합니다. SQLServerPreparedStatement 및 SQLServerCallableStatement 클래스 및 업데이트 집합 * 메서드\* SQLServerResultSet 클래스의 메서드는 강제 암호화 설정을 지정 하는 부울 인수를 허용 하도록 오버 로드 합니다. 이 인수의 값이 false 이면 드라이버는 매개 변수에서 암호화를 요구 하지 않습니다. 암호화 설정 된 경우 true, 쿼리 매개 변수는 경우에 전송 대상 열 암호화 되 고 연결 또는 문이 상시 암호화 사용 합니다. 이 속성을 사용 하는 추가 보안 계층을를 드라이버 실수로 데이터를 보내지 않습니다 SQL 서버에 일반 텍스트로 암호화 되도록 예상 되는 경우 확인을 제공 합니다.

강제 암호화 설정 사용 하 여 SQLServerPreparedStatement 및 SQLServerCallableStatement 메서드 오버 로드 된 자세한 내용은 참조 하세요. [Always Encrypted API 참조 JDBC 드라이버](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어
상시 암호화는 클라이언트 쪽 암호화 기술이므로 데이터베이스가 아닌 클라이언트 쪽에서 대부분의 성능 오버헤드가 발생합니다. 암호화 및 암호 해독 작업의 비용 외에 클라이언트 쪽 성능 오버헤드의 원인은 다음과 같습니다.
- 쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복
- 열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출

이 섹션에서는 SQL Server용 Microsoft JDBC Driver의 기본 제공 성능 최적화와 위의 두 성능 요소의 영향을 제어할 수 있는 방법에 대해 설명합니다.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대한 메타데이터를 검색하기 위한 왕복 제어
연결에 대한 상시 암호화가 설정된 경우 기본적으로 드라이버는 각 매개 변수화된 쿼리에 대해 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)을 호출하고 매개 변수 값 없이 쿼리 문을 SQL Server에 전달합니다. [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)은 쿼리 문을 분석하여 암호화해야 하는 매개 변수가 있는지 확인하고, 필요한 경우 드라이버에서 매개 변수 값을 암호화할 수 있도록 각 매개 변수에 대해 암호화 관련 정보를 반환합니다. 이 동작은 클라이언트 응용 프로그램에 대한 높은 수준의 투명도를 보장합니다. 드라이버에 암호화 된 열을 대상으로 하는 값을 전달할 매개 변수를 사용 하는 응용 프로그램,으로 응용 프로그램 (및 응용 프로그램 개발자)는 알 필요가 어떤 쿼리가 암호화 된 열 액세스 합니다.

### <a name="setting-always-encrypted-at-the-query-level"></a>쿼리 수준에서 상시 암호화 설정
매개 변수화된 쿼리의 암호화 메타데이터 검색을 위한 성능 영향을 제어하려면 연결이 아닌 개별 쿼리에 대해 상시 암호화를 설정합니다. 이렇게 하면 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리에 대해서만 sys.sp_describe_parameter_encryption을 호출할 수 있습니다. 단, 이 경우 암호화의 투명성이 저하될 수 있습니다. 데이터베이스 열의 암호화 속성을 변경한 경우 스키마 변경에 맞게 응용 프로그램 코드를 변경해야 할 수 있습니다.

개별 쿼리의 Always Encrypted 동작을 제어 하려면 sqlserverstatementcolumnencryptionsetting은 데이터를 전송 및 읽고 쓸 때 수신 하는 방법을 지정 하는 열거형을 전달 하 여 개별 statement 개체를 구성 해야 해당 특정 문에 대 한 암호화 된 열입니다. 다음은 몇 가지 유용한 지침입니다.
- 클라이언트 응용 프로그램이 데이터베이스 연결을 통해 전송하는 대부분의 쿼리가 암호화된 열에 액세스하는 경우 다음 지침을 따릅니다.
    - **columnEncryptionSetting** 연결 문자열 키워드를 **Enabled**로 설정합니다.
    - 암호화된 모든 열에 액세스하지 않는 개별 쿼리에 SQLServerStatementColumnEncryptionSetting.Disabled를 설정합니다. 이 설정은 sys.sp_describe_parameter_encryption이 호출되지 않고 결과 집합 값의 암호 해독도 시도되지 않도록 합니다.
    - 암호화를 요구하는 매개 변수가 없지만 암호화된 열에서 데이터를 검색하는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.ResultSet을 설정합니다. 이 설정은 sys.sp_describe_parameter_encryption 호출 및 매개 변수 암호화가 사용되지 않도록 합니다. 쿼리가 암호화 열에서 결과를 해독할 수 없습니다.
- 클라이언트 응용 프로그램이 데이터베이스 연결을 통해 전송하는 대부분의 쿼리가 암호화된 열에 액세스하지 않는 경우 다음 지침을 따릅니다.
    - **columnEncryptionSetting** 연결 문자열 키워드를 **Disabled**로 설정합니다.
    - 암호화해야 하는 모든 매개 변수가 있는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.Enabled를 설정합니다. 이 설정은 sys.sp_describe_parameter_encryption이 호출될 뿐만 아니라 암호화된 열에서 검색된 모든 쿼리 결과의 암호가 해독되도록 합니다.
    - 암호화를 요구하는 매개 변수가 없지만 암호화된 열에서 데이터를 검색하는 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.ResultSet을 설정합니다. 이 설정은 sys.sp_describe_parameter_encryption 호출 및 매개 변수 암호화가 사용되지 않도록 합니다. 쿼리가 암호화 열에서 결과를 해독할 수 없습니다.

Sqlserverstatementcolumnencryptionsetting은 설정은 암호화를 무시 하 고 일반 텍스트 데이터에 액세스를 사용할 수 없습니다. 문에서 열 암호화를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [Always Encrypted API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.  

다음 예제에서는 데이터베이스 연결에 대해 상시 암호화가 사용되지 않습니다. 응용 프로그램에서 실행하는 쿼리에는 암호화되지 않은 LastName 열을 대상으로 하는 매개 변수가 있습니다. 쿼리는 암호화된 SSN 및 BirthDate 열에서 데이터를 검색합니다. 이러한 경우 암호화 메타데이터를 검색할 때 sys.sp_describe_parameter_encryption을 호출하지 않아도 됩니다. 그러나 응용 프로그램에서 두 암호화된 열에서 일반 텍스트 값을 가져올 수 있도록 쿼리 결과에 대한 암호 해독을 설정해야 합니다. SQLServerStatementColumnEncryptionSetting.ResultSet 설정 되어 있는지 확인 됩니다.

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord,
        ResultSet.TYPE_FORWARD_ONLY,
        ResultSet.CONCUR_READ_ONLY,
        connection.getHoldability(),
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");
ResultSet rs = selectStatement.executeQuery();
while(rs.next()) {
    System.out.println("First name: " + rs.getString("FirstName"));
    System.out.println("Last name: " + rs.getString("LastName"));
    System.out.println("SSN: " + rs.getString("SSN"));
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
}
rs.close();
selectStatement.close();
connection.close();
```

### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱
열 마스터 키 저장소에 대한 호출 수를 줄여 열 암호화 키의 암호를 해독하기 위해 SQL Server용 Microsoft JDBC Driver에서는 일반 텍스트 열 암호화 키를 메모리에 캐시합니다. 데이터베이스 메타데이터에서 암호화된 열 암호화 키 값을 받은 후 드라이버는 제일 먼저 암호화된 키 값에 해당하는 일반 텍스트 열 암호화 키를 찾습니다. 드라이버는 캐시에서 암호화된 열 암호화 키 값을 찾을 수 없는 경우에만 열 마스터 키가 포함된 키 저장소를 호출합니다.

SQLServerConnection 클래스의 setColumnEncryptionKeyCacheTtl(), API를 사용 하 여 캐시의 열 암호화 키 항목에 대 한 활성 시간 값을 구성할 수 있습니다. 캐시의 열 암호화 키 항목에 대 한 기본 활성 시간 값에 2 시간입니다. 캐시를 해제 하려면 값 0 사용 합니다. Time-to-live 값을 설정 하려면 다음 API를 사용 합니다.

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

예를 들어 10 분의-time-to-live 값을 설정 하려면 다음을 사용 합니다.

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

일, 시간, 분 또는 초를 시간 단위로 지원 됩니다.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>SQLServerBulkCopy를 사용 하 여 암호화 된 데이터를 복사 합니다.
SQLServerBulkCopy를 사용하면 데이터의 암호를 해독하지 않고 한 테이블에서 이미 암호화되어 저장된 데이터를 다른 테이블에 복사할 수 있습니다. 이렇게 하려면 다음을 수행합니다.

- 대상 테이블의 암호화 구성이 원본 테이블의 구성과 일치하는지 확인합니다. 특히 두 테이블에 동일한 암호화 열이 있고 동일한 암호화 형식 및 암호화 키를 사용하여 열이 암호화되어야 합니다. 대상 열이 해당 원본 열과 다르게 암호화된 경우 복사 작업 후 대상 테이블의 데이터 암호를 해독할 수 없습니다. 데이터가 손상됩니다.
- 상시 암호화를 사용하지 않고 원본 테이블과 대상 테이블에 대한 데이터베이스 연결을 구성합니다.
- AllowEncryptedValueModifications 옵션을 설정 합니다. 자세한 내용은 [JDBC 드라이버를 사용 하 여 대량 복사를 사용 하 여](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)입니다.

> [!NOTE]
> 이 옵션을 AllowEncryptedValueModifications로 지정하면 SQL Server용 Microsoft JDBC Driver는 데이터가 암호화되었는지 여부 또는 동일한 암호화 형식, 알고리즘 및 키를 대상 열로 사용하여 올바르게 암호화되었는지 확인하지 않아 데이터베이스가 손상될 수 있으므로 주의하여 사용합니다.

## <a name="see-also"></a>참고 항목
[Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
