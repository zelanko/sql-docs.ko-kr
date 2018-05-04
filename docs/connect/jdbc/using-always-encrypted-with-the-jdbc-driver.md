---
title: JDBC 드라이버와 함께 상시 암호화를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 3/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 64
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88bcc472734964bc890f788d3878b6e1513f4ee4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>JDBC 드라이버와 함께 상시 암호화를 사용 하 여
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 페이지를 사용 하 여 Java 응용 프로그램을 개발 하는 방법에 대해 설명 [항상 암호화](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 Microsoft JDBC Driver 6.0 (또는 이상) for SQL Server.

항상 암호화 된 클라이언트가 중요 한 데이터를 암호화 하는 데이터 또는 SQL Server 또는 Azure SQL 데이터베이스에 암호화 키를 표시 하지 않을 수 있습니다. 상시 암호화 지원 드라이버 등 Microsoft JDBC Driver 6.0 (또는 그 이상) for SQL Server, 투명 하 게 암호화 하 고 클라이언트 응용 프로그램의 중요 한 데이터를 해독 하 여이 문제를 얻습니다. 드라이버는 쿼리를 자동으로 결정 매개 변수 항상 암호화 데이터베이스 열에 해당 하 고 SQL Server 또는 Azure SQL 데이터베이스에 보내기 전에 해당 매개 변수 값을 암호화 합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 참조 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소
- 있는지 Microsoft JDBC Driver 6.0 (또는 이상) 확인 하십시오 SQL Server는 개발 컴퓨터에 설치 합니다. 
- Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files를 다운로드하여 설치합니다.  내보내기/가져오기 문제에 설치 지침 및 관련 세부 정보에 대 한 zip 파일에 포함 된 추가 정보를 참조 해야 합니다.  

    - 정책 파일을 다운로드할 수 mssql-jdbc-X.X.X.jre7.jar 또는 sqljdbc41.jar을 사용 하는 경우 [Java Cryptography Extension (JCE) 무제한 강도 Jurisdiction Policy Files 7 다운로드](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - 정책 파일을 다운로드할 수 mssql-jdbc-X.X.X.jre8.jar 또는 sqljdbc42.jar를 사용 하는 경우 [Java Cryptography Extension (JCE) 무제한 강도 Jurisdiction Policy Files 8 다운로드](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - Mssql-jdbc X.X.X.jre9.jar를 사용 하 여 정책 파일이 없습니다를 다운로드 해야 합니다. Java 9 jurisdiction 정책 무제한 강도 암호화 기본값으로 사용 됩니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 사용
을 암호화 하거나 암호화 된 열에 대 한 데이터를 해독 하려면 SQL Server에는 열 암호화 키 유지 관리 합니다. 열 암호화 키는 데이터베이스 메타 데이터에 암호화 된 형태로 저장 됩니다. 각 열 암호화 키는 열 암호화 키를 암호화 하는 데 사용 되는 해당 열 마스터 키에 있습니다. 데이터베이스 메타 데이터는 열 마스터 키를 포함 되지 않습니다. 이러한 키는 클라이언트에서 유지 됩니다. 그러나 데이터베이스 메타 데이터에 클라이언트를 기준으로 열 마스터 키 저장 되는 위치에 대 한 정보를 포함 합니다. 예를 들어 데이터베이스 메타 데이터 표시 될 수도 있음를 보유 하는 열 마스터 키가 Windows 인증서 저장소 및 암호화 및 암호 해독에 사용 되는 특정 인증서가 Windows 인증서 저장소 내에서 특정 경로에 있는 키 저장소입니다. 클라이언트의 Windows 인증서 저장소에 해당 인증서에 액세스할 수 있으면 인증서를 얻을 수 있습니다. 열 암호화 키의 암호를 해독 하는 인증서를 사용한 다음 있습니다. 그 암호화 키를 해독 하거나 해당 열 암호화 키를 사용 하는 암호화 된 열에 대 한 데이터 암호화 사용 될 수 있습니다.

파생 된 클래스의 인스턴스는 열 마스터 키 저장소 공급자를 사용 키 저장소와 통신 하는 SQL Server 용 Microsoft JDBC Driver **SQLServerColumnEncryptionKeyStoreProvider**합니다.

### <a name="using-built-in-column-master-key-store-providers"></a>기본 제공 열 마스터 키 저장소 공급자 사용
SQL Server 용 Microsoft JDBC 드라이버는 다음과 같은 기본 제공 열 마스터 키 저장소 공급자 함께 제공 됩니다. (공급자 조회에 사용) 하는 특정 공급자 이름이 미리 등록 되어 이러한 공급자 중 일부 및 일부 추가 자격 증명이 나 명시적 등록 해야 합니다.

| 클래스 | Description | 공급자 (조회) 이름 |미리 등록?|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Azure 키 자격 증명 모음에 대 한 키 저장소에 대 한 공급자입니다.| AZURE_KEY_VAULT|아니요|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Windows 인증서 저장소에 대 한 공급자입니다.|MSSQL_CERTIFICATE_STORE|예
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Java keystore에 대 한 공급자|MSSQL_JAVA_KEYSTORE|예|

미리 등록 된 키 저장소 공급자에 대 한 모든 응용 프로그램 코드를 변경 하려면 이러한 공급자를 사용 하지만 다음 사항에 유의 필요가 없습니다.

- 사용자 (또는 DBA)는 열 마스터 키 메타 데이터에 구성 된 공급자 이름이 올바른지와 열 마스터 키 경로 지정 된 공급자에 유효한 키 경로 형식을 준수 되도록 해야 합니다. CREATE COLUMN MASTER KEY (TRANSACT-SQL) 문을 실행할 때 적합 한 공급자 이름 및 키 경로 자동으로 생성 하는 SQL Server Management Studio 등의 도구를 사용 하 여 키를 구성 하는 것이 좋습니다.
- 응용 프로그램 키 저장소에 키에 액세스할 수 있는지 확인 합니다. 이 작업은 키 및/또는 키 저장소에 따라 키 저장소에 대 한 응용 프로그램 액세스 권한을 부여 하거나 다른 키 저장소 관련 구성 단계를 수행 포함 될 수 있습니다. 예를 들어는 SQLServerColumnEncryptionJavaKeyStoreProvider를 사용 하는 것에 대 한 필요한 위치 및 연결 속성에서 키 저장소의 암호를 제공 합니다. 

이러한 키 저장소 공급자의 모든 작업은 다음 섹션에서 자세히 설명 되어 있습니다. 상시 암호화를 사용 하려면 키 저장소 공급자 구현 하기만 하면 됩니다.

### <a name="using-azure-key-vault-provider"></a>Azure Key Vault 공급자 사용
Azure 키 자격 증명 모음에 저장 하 고 상시 암호화를 위한 열 마스터 키를 관리 (특히 응용 프로그램에서 호스팅되는 경우 Azure) 편리한 옵션입니다. SQL Server 용 Microsoft JDBC Driver에는 Azure 키 자격 증명 모음에 저장 된 키가 있는 응용 프로그램에 대 한 기본 제공 공급자, SQLServerColumnEncryptionAzureKeyVaultProvider, 포함 되어 있습니다. 이 공급자의 이름은 AZURE_KEY_VAULT입니다. Azure 키 자격 증명 모음 저장소 공급자를 사용 하려면 응용 프로그램 개발자는 Azure Active Directory에 앱 등록을 만드는 Azure 키 자격 증명 모음에 자격 증명 모음 및 해당 키를 만드는 데 필요한 합니다. 등록 된 응용 프로그램에는 부여, 암호 해독, 암호화, 키 래핑 해제, 래핑할 키 및 확인 권한의 얻을 상시 암호화와 함께 사용 하기 위해 만든 키 자격 증명 모음에 대해 정의 된 액세스 정책에를 사용 해야 합니다. 키 자격 증명 모음을 설정 하 고 열 마스터 키 생성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 키 자격 증명 모음 – 단계별](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) 및 [Azure 키 자격 증명 모음에 열 마스터 키 만들기](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault)합니다.

Azure 키 자격 증명 모음을 만든 경우이 페이지의 예제에서 열 마스터 키와 SQL Server Management Studio를 사용 하 여 열 암호화 키를 기반으로 다시 작성 하는 T-SQL 스크립트 유사 하 게 나타날 자체 특정이 예제 **KEY_ 경로** 및 **ENCRYPTED_VALUE**:

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

Azure 키 자격 증명 모음을 사용 하려면 클라이언트 응용 프로그램의 SQLServerColumnEncryptionAzureKeyVaultProvider 인스턴스화하고 드라이버에 등록 해야 합니다.

SQLServerColumnEncryptionAzureKeyVaultProvider 초기화의 예는 다음과 같습니다.  

```
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID** Azure Active Directory 인스턴스에서 응용 프로그램 등록의 응용 프로그램 ID입니다. **clientKey** Azure 키 자격 증명 모음에 대 한 API 액세스를 제공 하는 해당 응용 프로그램에서 키 암호 등록 되어 있습니다.

응용 프로그램 SQLServerColumnEncryptionAzureKeyVaultProvider의 인스턴스를 만든 후 sqlserverconnection.registercolumnencryptionkeystoreproviders () 메서드를 사용 하 여 드라이버와 응용 프로그램 인스턴스를 등록 해야 합니다. AZURE_KEY_VAULT SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API를 호출 하 여 가져올 수 있는 기본 조회 이름을 사용 하는 인스턴스는 등록 것이 좋습니다. 기본 이름을 사용 하면 프로 비전 및 관리 (도구 열 마스터 키 메타 데이터 개체를 생성 하는 기본 이름을 사용 하는 데 사용) 하는 상시 암호화 키를 SQL Server Management Studio 또는 PowerShell과 같은 도구를 사용할 수 있습니다. 다음 예제에서는 Azure 키 자격 증명 모음 공급자 등록 Sqlserverconnection.registercolumnencryptionkeystoreproviders () 메서드에 대 한 자세한 내용은 참조 하십시오. [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Azure 키 자격 증명 모음 키 저장소 공급자를 사용 하는 경우 JDBC 드라이버의 Azure 주요 자격 증명 모음 구현에 의존 응용 프로그램과 함께 포함 되어야 합니다 (GitHub)에서 이러한 라이브러리:
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Maven 프로젝트에서 이러한 종속성을 포함 하는 방법의 예제를 보려면 [다운로드 ADAL4J 및 AKV 종속성 Apache Maven으로](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자를 사용 하 여
Windows 인증서 저장소에 열 마스터 키를 저장 하는 SQLServerColumnEncryptionCertificateStoreProvider는 사용할 수 있습니다. SQL Server Management Studio (SSMS)에서 상시 암호화 마법사 또는 기타 지원 되는 도구를 사용 하 여 데이터베이스에 열 마스터 키와 열 암호화 키 정의 만들 수 있습니다. 항상 암호화 된 데이터에 대 한 열 마스터 키로 사용할 수 있는 Windows 인증서 저장소에 자체 서명 된 인증서를 생성 하 동일한 마법사를 사용할 수 있습니다. 열 마스터 키와 열 암호화 키 T-SQL 구문에 대 한 자세한 내용은 참조 하십시오. [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) 및 [CREATE COLUMN ENCRPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 각각.

SQLServerColumnEncryptionCertificateStoreProvider의 이름은 MSSQL_CERTIFICATE_STORE 이며 공급자 개체의 getName() API에서 쿼리할 수 있습니다. 드라이버에 의해 자동으로 등록 하 고 모든 응용 프로그램 변경 없이 원활 하 게 사용할 수 있습니다.

Windows 인증서 저장소를 만든 경우이 페이지의 예제에서 열 마스터 키와 SQL Server Management Studio를 사용 하 여 열 암호화 키를 기반으로 다시 작성 하는 T-SQL 스크립트 유사 하 게 나타날 자체 특정 이예제**KEY_PATH** 및 **ENCRYPTED_VALUE**:

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
> 이 문서에서 다른 키 저장소 공급자를 드라이버에서 지 원하는 모든 플랫폼에서 사용할 수 있는 동안 SQLServerColumnEncryptionCertificateStoreProvider 구현의 JDBC 드라이버를 Windows 운영 체제 에서만 가능 합니다. 드라이버 패키지에서 사용할 수 있는 sqljdbc_auth.dll에 종속성을 갖습니다. 이 공급자를 사용 하려면 JDBC 드라이버를 설치한 컴퓨터에서 Windows 시스템 경로에 있는 디렉터리를 sqljdbc_auth.dll 파일을 복사 합니다. 또는 java.libary.path 시스템 속성에 sqljdbc_auth.dll의 디렉터리를 지정할 수도 있습니다. 32비트 JVM(Java Virtual Machine)을 실행할 경우 운영 체제가 x64 버전이라도 x86 폴더에 있는 sqljdbc_auth.dll 파일을 사용하십시오. x64 프로세서에서 64비트 JVM을 실행할 경우 x64 폴더의 sqljdbc_auth.dll 파일을 사용하십시오. 예를 들어 32 비트 JVM을 사용 하는 경우 JDBC 드라이버는 기본 디렉터리에 설치 되어 있으면 Java 응용 프로그램을 시작 하는 경우에 다음 가상 컴퓨터 (VM) 인수를 사용 하 여 DLL의 위치를 지정할 수 있습니다. `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Java 키 저장소 공급자를 사용 하 여
JDBC 드라이버는 Java 키 저장소에 대 한 기본 제공 키 저장소 공급자 구현을 제공 됩니다. 경우는 **keyStoreAuthentication** 연결 문자열 속성은 연결 문자열에 및 "JavaKeyStorePassword"로 설정 된, 드라이버는 자동으로 인스턴스화 및 Java 키 저장소에 대 한 공급자를 등록 합니다. Java 키 저장소 공급자의 이름은 MSSQL_JAVA_KEYSTORE입니다. 이 이름은 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API를 사용 하 여 쿼리할 수도 있습니다. 

드라이버는 Java 키 저장소에 인증 해야 합니다. 자격 증명을 지정 하는 클라이언트 응용 프로그램을 사용할 수 있는 세 가지 연결 문자열 속성이 있습니다. 드라이버는 연결 문자열에서 이러한 세 속성의 값을 기반으로 하는 공급자를 초기화 합니다.

**keyStoreAuthentication:** 사용 하는 Java 키 저장소를 식별 합니다. Microsoft JDBC Driver for SQL Server 6.0 이상으로이 속성을 통해 Java 키 저장소에 인증할 수 있습니다. Java 키 저장소에 대 한이 속성에 대 한 값 이어야 합니다 `JavaKeyStorePassword`합니다.

**keyStoreLocation:** 열 마스터 키를 저장 하는 Java 키 저장소 파일의 경로입니다. 경로는 키 저장소 파일 이름이 포함 됩니다.

**keyStoreSecret:** 키 뿐만 아니라 keystore에 사용할 보안/암호입니다. Java 키 저장소를 사용 하는 것에 대 한 키 저장소 및 키 암호 동일 해야 합니다.

연결 문자열에 이러한 자격 증명을 제공 하는 예제는 다음과 같습니다.

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

가져오기 하거나 SQLServerDataSource 개체를 사용 하 여 이러한 설정을 설정할 수 있습니다. 자세한 내용은 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.

이 자격 증명은 연결 속성에 나타나야 하는 경우 JDBC 드라이버는 SQLServerColumnEncryptionJavaKeyStoreProvider를 자동으로 인스턴스화합니다.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Java 키 저장소에 대 한 열 마스터 키 만들기
SQLServerColumnEncryptionJavaKeyStoreProvider JKS, PKCS12 키 저장소 유형을 사용할 수 있습니다. 만들기 또는 가져오기에이 공급자와 함께 사용할 키를 사용 하 여이 Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) 유틸리티입니다. 키가 암호 자체 키 저장소와 동일 포함 해야 합니다. 공개 키 및 keytool 유틸리티를 사용 하 여 연결된 된 개인 키를 만드는 방법의 예는 다음과 같습니다.

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

이 명령은 공개 키를 만들고이 자체 서명 된 인증서 관련된 개인 키와 함께 ' keystore.jks' 키 저장소에 저장 되는 X.509에 래핑합니다. 키 저장소에이 항목은 'AlwaysEncryptedKey' 별칭으로 식별 됩니다.

동일한 형식을 사용 하 여 한 PKCS12 저장소의 예는 다음과 같습니다.

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

키 저장소 PKCS12 형식의 없으면 keytool 유틸리티 키 암호에 대해 묻지 않습니다 및 키 암호는 SQLServerColumnEncryptionJavaKeyStoreProvider 키 저장소와 키 같으면의 필요에 따라-keypass 옵션으로 제공 해야 합니다. 암호입니다.

.Pfx 형식으로 Windows 인증서 저장소에서 인증서를 내보낼 하 고는 SQLServerColumnEncryptionJavaKeyStoreProvider 함께 사용 하는 수도 있습니다. 내보낸된 인증서 Java 키 저장소에 JKS 키 저장소 형식으로 가져올 수도 있습니다.

Keytool 항목을 만든 후에 키 저장소 공급자 이름 및 키 경로 데이터베이스에 열 마스터 키 메타 데이터를 만듭니다. 열 마스터 키 메타 데이터를 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)합니다. SQLServerColumnEncryptionJavaKeyStoreProvider에 대 한 키 경로의 키의 별칭만 이며는 SQLServerColumnEncryptionJavaKeyStoreProvider 이름은 'MSSQL_JAVA_KEYSTORE'. 또한 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스의 getName() 공용 API를 사용 하 여이 이름을 쿼리할 수 있습니다. 

열 마스터 키를 만들기 위한 T-SQL 구문은 다음과 같습니다.

```
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

'AlwaysEncryptedKey' 위에서 만든에 대 한 열 마스터 키 정의 합니다.

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> 기본 제공 SQL Server management Studio 기능은 Java 키 저장소에 대 한 열 마스터 키 정의 만들 수 없습니다. T-SQL 명령은 프로그래밍 방식으로 사용 되어야 합니다.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Java 키 저장소에 대 한 열 암호화 키 만들기
Java 키 저장소에 열 마스터 키를 사용 하 여 암호화 키 열을 만들려면 SQL Server Management Studio 또는 다른 도구를 사용할 수 없습니다. 클라이언트 응용 프로그램이 프로그래밍 방식으로 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스를 사용 하 여 열 암호화 키를 만들어야 합니다. 자세한 내용은 참조 [열 마스터 키 저장소 공급자를 사용 하 여 프로그래밍 방식으로 키 프로 비전을 위한](#using-column-master-key-store-providers-for-programmatic-key-provisioning)합니다.

### <a name="implementing-a-custom-column-master-key-store-provider"></a>사용자 지정 열 마스터 키 저장소 공급자 구현
기존 공급자에서 지원 되지 않는 키 저장소에 열 마스터 키를 저장 하려는 경우 SQLServerColumnEncryptionKeyStoreProvider 클래스를 확장 하 고 사용 하 여 공급자를 등록 하 여 사용자 지정 공급자를 구현할 수 있습니다는 Sqlserverconnection.registercolumnencryptionkeystoreproviders () 메서드입니다.

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
암호화 된 열에 액세스할 때는 SQL Server 용 Microsoft JDBC Driver 투명 하 게 찾아서 열 암호화 키의 암호를 해독 하려면 오른쪽 열 마스터 키 저장소 공급자를 호출 합니다. 일반적으로 정상적인 응용 프로그램 코드는 열 마스터 키 저장소 공급자를 직접 호출하지 않습니다. 그러나 인스턴스화할 및 프로그래밍 방식으로 프로 비전 하 고 상시 암호화 키 관리 공급자를 호출할 수, 될 수 있습니다. 이 단계에서 암호화 된 열 암호화 키를 생성 하 고 예를 들어 부분 열 마스터 키 회전으로 열 암호화 키를 암호 해독을 수행할 수 있습니다. 자세한 내용은 [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.

사용자 지정 키 저장소 공급자를 사용 하는 경우에 고유한 키 관리 도구를 구현할 필요할 수 있습니다. Windows 인증서 저장소 또는 Azure 키 자격 증명 모음에 저장 된 키를 사용할 때 관리 하 고 키를 프로 비전 할 SQL Server Management Studio 또는 PowerShell과 같은 기존 도구를 사용할 수 있습니다. Java 키 저장소에 저장 된 키를 사용할 때 키를 프로그래밍 방식으로 프로 비전 해야 합니다. 다음 예제에서는 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스를 사용 하 여 Java 키 저장소에 저장 된 키를 사용 하 여 키를 암호화 하는 방법을 보여 줍니다.

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
값을 설정 하 여이 매개 변수 암호화 및 암호화 된 열을 대상으로 하는 쿼리 결과의 암호 해독을 활성화 하는 가장 쉬운 방법은 **columnEncryptionSetting** 연결 문자열 키워드를 **사용** .

다음 연결 문자열은 JDBC 드라이버에서 상시 암호화 사용의 예.

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
```

다음 코드는 SQLServerDataSource 개체를 사용 하는 예제:

```
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

상시 암호화는 개별 쿼리에도 사용할 수 있습니다. 자세한 내용은 참조 [상시 암호화의 성능 영향 제어](#controlling-the-performance-impact-of-always-encrypted)합니다. 상시 암호화 사용 암호화 또는 암호 해독을 위해 충분 하지 않습니다. 다음을 확인해야 합니다.
- 응용 프로그램에는 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 데이터베이스 권한이 있으며 데이터베이스에서 상시 암호화 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 참조 [상시 암호화 (데이터베이스 엔진)에서 사용 권한을](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)합니다.
- 응용 프로그램 쿼리 된 데이터베이스 열을 암호화 하는 열 암호화 키를 보호 하는 열 마스터 키를 액세스할 수 있습니다. Java 키 저장소 공급자를 사용 하려면 연결 문자열에 추가 자격 증명을 제공 해야 합니다. 자세한 내용은 참조 [를 사용 하 여 Java 키 저장소 공급자](#using-java-key-store-provider)합니다.

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Java.sql.Time 값이 서버에 전송 방법 구성
**sendTimeAsDatetime** java.sql.Time 값을 서버에 보내는 방식을 구성할 연결 속성을 사용 합니다. 시간 값을 false로 설정 된 경우 SQL Server 시간 유형으로 전송 됩니다. 날짜/시간 형식으로 값은 전송 된 시간을 true로 설정 하면 됩니다. 시간 열을 암호화는 **sendTimeAsDatetime** 속성 암호화 된 열에 시간 형식으로 날짜/시간 변환 지원 하지 않으므로 false 여야 합니다. 또한 이때가이 속성은 기본값은 true, 되므로 암호화 된 시간 열을 사용 하는 경우 false로 설정 해야 합니다. 그렇지 않은 경우 드라이버는 예외가 throw 됩니다. 드라이버의 버전 6.0 이상에서는 SQLServerConnection 클래스에이 속성의 값을 프로그래밍 방식으로 구성 하려면 두 가지 방법이 있습니다.
 
* public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

이 속성에 대 한 자세한 내용은 참조 하십시오. [구성 방법을 java.sql.Time 값에는 서버에 보내집니다](configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>서버에 문자열 값은 전송 하는 방법을 구성 합니다.
**sendStringParametersAsUnicode** 연결 속성은 문자열 값을 SQL Server로 보내는 방법을 구성 하는 데 사용 합니다. 하면 문자열 매개 변수를 true로 설정 된 서버에 유니코드 형식으로 전송 됩니다. 하면 문자열 매개 변수를 false로 설정 ASCII 또는 유니코드 대신 MBCS 등의 비 유니코드 형식으로 전송 됩니다. 이 속성에 대 한 기본값은 true입니다. 상시 암호화 사용은 시점과 char/varchar/varchar(max) 열이 암호화의 가치 **sendStringParametersAsUnicode** false로 설정 해야 합니다. 이 속성이 true 이면 드라이버 예외가 throw 됩니다 유니코드 문자가 있는 char/varchar/varchar(max) 암호화 된 열에서 데이터를 암호 해독할 때. 이 속성에 대 한 자세한 내용은 참조 하십시오. [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화 된 열에 데이터 검색 및 수정
응용 프로그램 쿼리에 대해 상시 암호화를 설정 하면 암호화 된 데이터베이스 열에 데이터를 검색 하거나 수정할 표준 JDBC Api를 사용할 수 있습니다. 응용 프로그램에 필요한 데이터베이스 권한이 열 마스터 키에 액세스할 수는 경우 드라이버는 암호화 된 열을 대상 및 암호화 된 열에서 검색 된 데이터를 해독 하는 모든 쿼리 매개 변수를 암호화 합니다.

상시 암호화를 사용하지 않는 경우 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패합니다. 여전히 쿼리 쿼리에 암호화 된 열을 대상으로 하는 매개 변수 없이으로 암호화 된 열에서 데이터를 검색할 수 있습니다. 그러나 드라이버에서 암호화 된 열에서 검색 된 값을 해독 하지 않으며 응용 프로그램 (바이트 배열)로 암호화 된 이진 데이터를 받게 됩니다.

다음 표에서 상시 암호화가 사용 여부에 따라 쿼리의 동작을 요약 되어 있습니다.

|쿼리 특성 | 상시 암호화가 설정되고 응용 프로그램에서 키 및 키 메타데이터에 액세스할 수 있는 경우|상시 암호화가 설정되고 응용 프로그램에서 키 또는 키 메타데이터에 액세스할 수 없는 경우 | 상시 암호화를 사용하지 않는 경우|
|:---|:---|:---|:---|
| 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리 | 매개 변수 값이 투명하게 암호화됩니다. | 오류 | 오류|
| 암호화 된 열을 대상으로 하는 매개 변수 없이 암호화 된 열에서 데이터를 검색 하는 쿼리 합니다.| 암호화된 열의 결과가 투명하게 암호 해독됩니다. 응용 프로그램에서 암호화 된 열에 대해 구성 된 SQL Server 형식에 해당 하는 JDBC 데이터 형식을 유니코드로의 일반 텍스트 값을 받습니다. | 오류 | 암호화된 열의 결과가 암호 해독되지 않습니다. 응용 프로그램에서 암호화된 값을 바이트 배열(byte[])로 수신합니다.

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>암호화 된 데이터 예제 삽입 및 검색 
다음 예제에는 암호화된 열에서 데이터를 검색 및 수정하는 방법을 설명합니다. 예제에서는 다음 스키마와 암호화 된 SSN 및 BirthDate 열에 포함 된 대상 테이블을 가정합니다. 명명 된 열 마스터 키를 구성한 경우 "MyCMK" 및 열 암호화 키 (이전 키 저장소 공급자 섹션에서 설명)으로 "MyCEK" 라는 이벤트를이 스크립트를 사용 하 여 테이블을 만들 수 있습니다.

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

각 Java 코드 예제에 대 한 키 저장소 관련 코드가 명시 된 위치에 삽입 해야 합니다.

Azure 키 자격 증명 모음 키 저장소 공급자를 사용할 경우

```
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Windows 인증서 저장소 keystore 공급자 사용 중인 경우:

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

키 저장소 Java keystore 공급자 사용 중인 경우:

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>데이터 예제 삽입
이 예제에서는 Patients 테이블에 행을 삽입합니다. 다음 항목을 note:
- 샘플 코드에는 암호화에 대한 내용이 없습니다. SQL Server 용 Microsoft JDBC 드라이버는 자동으로 검색 하 고 암호화 된 열을 대상으로 하는 매개 변수를 암호화 합니다. 이 통해 암호화 투명 한 응용 프로그램에 있습니다.
- 데이터베이스 열을 포함 하는 암호화 된 열에 삽입 된 값은 SQLServerPreparedStatement를 사용 하 여 매개 변수로 전달 됩니다. 매개 변수를 사용 하 여는 (하지만,이 가장 좋습니다 SQL 주입 공격을 방지할 수 있으므로) 암호화 되지 않은 열에 값을 보낼 때 선택 사항 동안, 암호화 된 열을 대상으로 하는 값에 필요 합니다. 암호화 된 열에 삽입 된 값 쿼리 문에 포함 된 리터럴로 전달 된 경우 드라이버는 암호화 된 대상 열에 값을 확인할 수 없으며 값을 암호화 하지 않으므로 때문에 쿼리가 실패 합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.
- Microsoft JDBC Driver for SQL Server가 암호화 된 열에서 검색 한 데이터를 투명 하 게 암호 해독 하는 대로 프로그램이 인쇄 하는 모든 값에 일반 텍스트로 됩니다.
- WHERE 절을 드라이버 암호화할 수 있도록 투명 하 게 하는 데이터베이스에 보내기 전에 매개 변수로 전달할 수 있어야 하는 WHERE 절에 사용 되는 값을 사용 하 여 조회 수행 하려는 경우 합니다. 다음 예제에서는 ssn 텍스트가 매개 변수로 전달 되 있지만 성 LastName 암호화 되지 않은 처럼 리터럴로 전달 됩니다.
- SSN 열을 대상으로 매개 변수에 사용 된 setter 방법은 setString() char/varchar SQL Server 데이터 형식으로 매핑됩니다. 이 매개 변수를 사용 하는 setter 메서드 있었던 setNString() nchar/nvarchar에 매핑되는 경우 항상 암호화에서는 암호화 된 nchar/nvarchar 값에서 암호화 된 char/varchar 값으로의 변환을 지원 하지 않으므로 쿼리가 실패 합니다.

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

### <a name="retrieving-plaintext-data-example"></a>일반 텍스트 데이터 검색 예
다음 예제에서는 암호화 된 열에서 일반 텍스트 데이터를 검색 하 고 암호화 된 값에 따라 데이터를 필터링 하는 방법을 보여 줍니다. 다음 항목을 note:
- SQL Server 용 Microsoft JDBC Driver 암호화할 수 있도록 투명 하 게 하는 데이터베이스에 보내기 전에 매개 변수로 전달할 필요 SSN 열에서 필터링 할 WHERE 절에 사용 되는 값입니다.
- Microsoft JDBC Driver for SQL Server가 SSN 및 BirthDate 열에서 검색 한 데이터를 투명 하 게 암호 해독 하는 대로 프로그램이 인쇄 하는 모든 값에 일반 텍스트로 됩니다.

> [!NOTE]
> 열은 결정적 암호화를 사용 하 여 암호화, 쿼리에서에 같음 비교를 수행할 수 있습니다. 자세한 내용은 참조 [상시 암호화 (데이터베이스 엔진)에서 선택 하면 결정적 또는 임의 암호화](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)합니다.

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
  
### <a name="retrieving-encrypted-data-example"></a>암호화 된 데이터 검색 예
상시 암호화를 사용하지 않는 경우에도 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없으면 암호화된 열에서 데이터를 검색할 수 있습니다.

다음 예제에서는 암호화 된 열에서 암호화 된 이진 데이터를 검색 하는 방법을 보여 줍니다. 다음 항목을 note:
- 연결 문자열에는 상시 암호화 사용 되지 않는, 하므로 쿼리 (프로그램 값을 문자열로 변환) 하는 바이트 배열로 SSN 및 BirthDate의 암호화 된 값을 반환 합니다.
- 암호화된 열을 대상으로 하는 매개 변수가 없으면 상시 암호화를 사용하지 않고 암호화된 열에서 데이터를 검색하는 쿼리에 매개 변수가 있을 수 있습니다. 데이터베이스에 암호화 되지 않은 lastname을 기준으로 다음 쿼리 필터를 지정 합니다. 쿼리가 SSN 또는 BirthDate를 기준으로 필터링되면 쿼리가 실패합니다.

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
이 섹션에서는 방지 하는 방법에 대 한 몇 가지 지침 및 Java 응용 프로그램에서 암호화 된 열을 쿼리할 때 일반적인 오류 범주를 설명 합니다.

### <a name="unsupported-data-type-conversion-errors"></a>지원되지 않는 데이터 형식 변환 오류
상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 참조 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 자세한 목록은 지원 되는 형식 변환에 대 한 합니다. 데이터 형식 변환 오류를 방지 하기 위해 수행할 수 있는 다음과 같습니다. 사항을 확인 합니다.

- 암호화 된 열을 대상으로 하는 매개 변수에 대 한 값을 전달 하는 경우에 적절 한 setter 메서드를 사용 합니다. SQL Server 데이터 형식의 매개 변수는 대상 열의 형식과 동일 정확 하 게 사용할 수는 매개 변수의 SQL Server 데이터 형식 열의 대상 형식으로 변환 했는지 확인 합니다. API 메서드는 특정 SQL Server 데이터 형식에 해당 하는 매개 변수를 전달할 SQLServerPreparedStatement, SQLServerCallableStatement, 및 SQLServerResultSet 클래스에 추가 되었습니다. 예를 들어, 열 암호화 되지 않은 경우는 datetime2 또는 날짜/시간 열의 매개 변수를 전달할 setTimestamp() 메서드를 사용할 수 있습니다. 하지만 열을 암호화할 때 데이터베이스에 있는 열의 유형을 나타내는 정확 하 게 메서드를 사용 해야 합니다. 예를 들어 setTimestamp()를 사용 하 여 하는 암호화 된 datetime2 열에 값을 전달 하 고 setDateTime()를 사용 하 여 암호화 된 datetime 열에 값을 전달 합니다. 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) 전체 목록은 새로운 Api입니다.
- SQL Server 데이터 형식이 decimal 및 numeric인 열을 대상으로 하는 매개 변수의 정밀도 및 배율이 대상 열에 대해 구성된 정밀도 및 배율과 동일해야 합니다. API 메서드는 전체 자릿수 및 소수 10 진수 및 숫자 데이터 형식을 나타내는 매개 변수/열에 대 한 데이터 값과 함께 수락 하도록 SQLServerPreparedStatement, SQLServerCallableStatement, 및 SQLServerResultSet 클래스에 추가 되었습니다. 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) 오버 로드/새 Api의 전체 목록은 합니다.  
- datetime2, datetimeoffset, 또는 시간 SQL Server 데이터 형식 열을 대상으로 하는 매개 변수의 소수 자릿수 초의 자릿수/소수 대상 열의 값을 수정 하는 쿼리에서 대상 열에 대 한 소수 자릿수 초의 자릿수/소수 보다 크지 않습니다. . API 메서드는 이러한 데이터 형식을 나타내는 매개 변수에 대 한 데이터 값과 함께 소수 자릿수 초의 자릿수/소수를 허용 하도록 SQLServerPreparedStatement, SQLServerCallableStatement, 및 SQLServerResultSet 클래스에 추가 되었습니다. 오버 로드/새 Api의 전체 목록은 참조 하십시오. [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.   

### <a name="errors-due-to-incorrect-connection-properties"></a>잘못 된 연결 속성으로 인해 발생 오류
이 섹션에서는 상시 암호화 데이터를 사용 하 여 적절 하 게 연결 설정을 구성 하는 방법에 설명 합니다. 암호화 된 데이터 형식 제한 변환을 지원 하므로 **sendTimeAsDatetime** 및 **sendStringParametersAsUnicode** 암호화 된 열을 사용 하는 경우 연결 설정에 적절 한 구성이 필요 합니다. 사항을 확인 합니다. 
- [sendTimeAsDatetime](setting-the-connection-properties.md) 시간 열을 암호화 된 데이터를 삽입 하는 경우 연결 설정이 false로 설정 되어 있습니다. 자세한 내용은 참조 [java.sql.Time 값이 서버에 전송 방법 구성](configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.
- [sendStringParametersAsUnicode](setting-the-connection-properties.md) 연결 설정이로 설정 되어 true (또는 기본값으로 유지) 데이터를 삽입 char/varchar/varchar(max) 열을 암호화 하는 경우.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류
암호화된 열을 대상으로 하는 모든 값은 응용 프로그램 내에서 암호화해야 합니다. 삽입/수정 하거나 암호화 된 열에서 일반 텍스트 값으로 필터링 하려면이 다음과 유사한 오류가 발생 합니다.

```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

이러한 오류를 방지하려면 다음을 확인합니다.
- 항상 암호화 (연결 문자열에 대해 또는 특정 쿼리에 대해) 암호화 된 열을 대상으로 하는 응용 프로그램 쿼리에 대해 활성화 됩니다.
- 준비 된 문을 사용 하 고 암호화 된 열을 데이터 대상으로 보낼 매개 변수입니다. 다음 예제에서는 기준으로 잘못 필터링 암호화 된 열 (SSN)에서 리터럴/상수에 리터럴을 매개 변수로 전달 하는 대신 하는 쿼리를 보여 줍니다. 이 쿼리는 실패 합니다.

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>입력된 매개 변수에서 암호화 적용
암호화 적용 기능 상시 암호화를 사용 하는 경우 매개 변수의 암호화를 적용 합니다. 암호화 적용을 사용 하는 경우 SQL Server에 암호화 매개 변수가 필요 하지 않은 드라이버에 알립니다 매개 변수를 사용 하면 쿼리가 실패 합니다. 이 속성은 데이터 노출을 야기할 수 있는 잘못된 암호화 메타데이터를 클라이언트에게 제공하는 손상된 SQL Server를 포함하는 보안 공격에 대한 추가 보호를 제공합니다. SQLServerPreparedStatement 및 SQLServerCallableStatement 클래스 및 업데이트의 집합 * 메서드\* force 암호화 설정을 지정 하려면 부울 인수를 허용 하려면 SQLServerResultSet 클래스의 메서드는 오버 로드 합니다. 이 인수의 값이 false 이면 드라이버는 매개 변수에 대 한 암호화를 요구 하지 않습니다. 암호화 적용 설정 되어 있으면 true, 쿼리를 매개 변수는 경우에 전송 대상 열은 암호화 되 고 문이 또는 연결에서 상시 암호화 사용 합니다. 이 속성을 사용 하는 추가적인 보안을는 드라이버 전송 하지 않습니다 실수로 데이터를 SQL Server 텍스트로 암호화 되도록 예상 되는 경우 확인을 제공 합니다.

Force 암호화 설정으로 오버 로드 된 SQLServerPreparedStatement 및 SQLServerCallableStatement 방법에 자세한 내용은 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어
상시 암호화는 클라이언트 쪽 암호화 기술 이므로 데이터베이스에는 없는 클라이언트 쪽에서 대부분의 성능 오버 헤드가 발견 됩니다. 암호화 및 해독 작업의 비용 외에 다른 소스 클라이언트 쪽 성능 오버 헤드 설정은:
- 쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복
- 열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출

이 섹션에서는 SQL Server와는 위의 두 성능 요소 영향을 제어 하는 방법에 대 한 Microsoft JDBC 드라이버에서 기본 제공 성능 최적화를 설명 합니다.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대한 메타데이터를 검색하기 위한 왕복 제어
상시 암호화를 연결에 사용 하는 경우 기본적으로 드라이버를 호출 합니다 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) 각 매개 변수가 있는 쿼리에 대 한 모든 매개 변수 값) (없이 쿼리 문을 SQL Server에 전달 합니다. [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) 를 찾으려면 매개 변수를 암호화 해야 하는 경우 그리고 있다면 각 하나 반환 매개 변수 값을 암호화 하는 드라이버를 사용 하면 되는 암호화 관련 정보에 대 한 쿼리 문을 분석 하 여 합니다. 이 동작은 클라이언트 응용 프로그램에는 투명도 대 한 높은 수준의 보장합니다. 드라이버에 암호화 된 열을 대상으로 하는 값을 전달할 매개 변수를 사용 하는 응용 프로그램,으로 응용 프로그램 (및 응용 프로그램 개발자) 하지 않아도 어떤 쿼리가 암호화 된 열 액세스에 대해 알아야 합니다.

### <a name="setting-always-encrypted-at-the-query-level"></a>쿼리 수준에서 상시 암호화 설정
매개 변수가 있는 쿼리에 대 한 암호화 메타 데이터 검색의 성능 영향을 제어 하려면 가능 상시 암호화는 연결에 대해 설정 하는 대신 개별 쿼리에 대 한 합니다. 암호화 된 열을 대상으로 하는 매개 변수가 있는 쿼리에 대해서만 sys.sp_describe_parameter_encryption을 보장할 수 있습니다 이러한 방식으로 호출 됩니다. 그러나 암호화의 투명성이 저하 되므로 수행 하 여 있는: 데이터베이스 열의 암호화 속성을 변경 하면 스키마 변경에 맞게 응용 프로그램의 코드를 변경 해야 할 수 있습니다.

개별 쿼리의 상시 암호화 동작을 제어 하려면 SQLServerStatementColumnEncryptionSetting 데이터는 전송 및 읽고 쓸 때 받은 방법을 지정 하는 열거형을 전달 하 여 개별 statement 개체를 구성 해야 암호화 된 열에 대해 특정 설명 합니다. 다음은 몇 가지 유용한 지침입니다.
- 대부분의 쿼리에서 데이터베이스 연결을 통해 전송 되는 클라이언트 응용 프로그램에서 암호화 된 열에 액세스 하는 경우 이러한 지침을 따르세요.
    - 설정의 **columnEncryptionSetting** 연결 문자열 키워드를 **Enabled**합니다.
    - 암호화 된 모든 열을 액세스 하지 않는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.Disabled를 설정 합니다. Sys.sp_describe_parameter_encryption이 호출 될 뿐만 아니라 결과 집합의 값을 해독 하려고 한 경우이 설정을 비활성화 합니다.
    - 암호화를 요구 하는 모든 매개 변수가 없는 없지만 암호화 된 열에서 데이터를 검색 하는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.ResultSet를 설정 합니다. Sys.sp_describe_parameter_encryption 호출 및 매개 변수 암호화가이 설정을 비활성화 합니다. 쿼리가 암호화 열에서 결과를 해독할 수 없습니다.
- 대부분의 쿼리에서 데이터베이스 연결을 통해 전송 되는 클라이언트 응용 프로그램에서 암호화 된 열을 액세스 하지 않을, 이러한 지침을 따르세요.
    - 설정의 **columnEncryptionSetting** 연결 문자열 키워드를 **비활성화**합니다.
    - 암호화 해야 하는 모든 매개 변수가 있는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.Enabled를 설정 합니다. 이 설정은 sys.sp_describe_parameter_encryption이 호출 될 뿐만 아니라 암호화 된 열에서 검색 된 모든 쿼리 결과의 암호를 해독 하면 있습니다.
    - 암호화를 요구 하는 매개 변수가 없지만 암호화 된 열에서 데이터를 검색 하는 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.ResultSet를 설정 합니다. Sys.sp_describe_parameter_encryption 호출 및 매개 변수 암호화가이 설정을 비활성화 합니다. 쿼리가 암호화 열에서 결과를 해독할 수 없습니다.

암호화를 무시 하 고 일반 텍스트 데이터에 액세스 하는 SQLServerStatementColumnEncryptionSetting 설정은 사용할 수 없습니다. 문에서 열 암호화를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.  

다음 예제에서는 항상 암호화 데이터베이스 연결에 대해 비활성화 됩니다. 응용 프로그램 문제에 매개 변수가 암호화 되지 않은 LastName 열을 대상으로 하는 쿼리. 쿼리는 암호화된 SSN 및 BirthDate 열에서 데이터를 검색합니다. 이러한 경우 암호화 메타데이터를 검색할 때 sys.sp_describe_parameter_encryption을 호출하지 않아도 됩니다. 그러나 쿼리 결과의 암호 해독은 응용 프로그램에서 두 암호화 된 열에서 일반 텍스트 값을 받을 수 있도록 사용할 수 있어야 합니다. SQLServerStatementColumnEncryptionSetting.ResultSet 설정이 되도록 사용 됩니다.

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
열 암호화 키를 해독 하는 열 마스터 키 저장소에 대 한 호출의 수를 줄이려면 SQL Server 용 Microsoft JDBC Driver는 메모리에 일반 텍스트 열 암호화 키를 캐시 합니다. 데이터베이스 메타 데이터에서 암호화 된 열 암호화 키 값을 받은 후 드라이버는 먼저 암호화 된 키 값에 해당 하는 일반 텍스트 열 암호화 키를 찾으려고 시도 합니다. 드라이버는 암호화 된 열 암호화 키 값 캐시 찾을 수 없을 경우에 열 마스터 키를 포함 하는 키 저장소를 호출 합니다.

SQLServerConnection 클래스의 setColumnEncryptionKeyCacheTtl(), API를 사용 하 여 캐시에 열 암호화 키 항목에 대 한 활성 시간 값을 구성할 수 있습니다. 열 암호화 키 항목이 캐시에 대 한 기본 활성 시간 값은 두 시간입니다. 캐시를 해제 하려면 값 0 사용 합니다. 모든 활성 시간 값을 설정 하려면 다음 API를 사용 합니다.

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

예를 들어 10 분의 활성 시간 값을 설정 하려면 다음을 사용 합니다.

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

일, 시, 분 또는 초 시간 단위로 사용할 수 있습니다.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>SQLServerBulkCopy를 사용 하 여 암호화 된 데이터를 복사 합니다.
SQLServerBulkCopy를 이미 암호화 되 고 데이터를 해독 하지 않고 다른 테이블에 한 테이블에 저장 된 데이터를 복사할 수 있습니다. 이렇게 하려면 다음을 수행합니다.

- 대상 테이블의 암호화 구성이 원본 테이블의 구성과 일치하는지 확인합니다. 특히 두 테이블 모두 동일한 열 암호화 있고 동일한 암호화 형식 및 동일한 암호화 키를 사용 하 여 열을 암호화 해야 합니다. 모든 대상 열은 해당 원본 열과 다르게 암호화 복사 작업 후 대상 테이블의 데이터를 해독할 수 없습니다. 데이터가 손상됩니다.
- 항상 암호화 하지 않고 테이블에 활성화를 대상 및 원본 테이블에 대 한 데이터베이스 연결을 구성 합니다.
- AllowEncryptedValueModifications 옵션을 설정 합니다. 자세한 내용은 참조 [JDBC 드라이버를 사용 하 여 대량 복사를 사용 하 여](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)합니다.

> [!NOTE]
> 이 옵션은 데이터가 암호화 되었는지 또는 동일한 암호화를 사용 하 여 올바르게 암호화 하는 경우 SQL Server 용 Microsoft JDBC Driver 검사 하지 않기 때문에 데이터베이스를 손상 시킬 수 대로 AllowEncryptedValueModifications를 지정할 때는 주의 형식, 알고리즘 및 키에 대상 열으로 합니다.

## <a name="see-also"></a>관련 항목:
[상시 암호화(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
