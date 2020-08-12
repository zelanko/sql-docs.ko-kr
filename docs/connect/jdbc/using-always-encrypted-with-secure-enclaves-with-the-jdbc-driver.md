---
title: 보안 Enclave를 사용한 Always Encrypted와 JDBC 드라이버 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: reneye
ms.author: v-reye
ms.openlocfilehash: 8933d01f8c1bb0e028927b1c0f97f064a369bb8e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758288"
---
# <a name="using-always-encrypted-with-secure-enclaves-with-the-jdbc-driver"></a>보안 Enclave를 사용한 Always Encrypted와 JDBC 드라이버 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 페이지에서는 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) 및 SQL Server용 Microsoft JDBC Driver 8.2 이상을 사용하여 Java 애플리케이션을 개발하는 방법을 설명합니다.

보안 Enclave는 기존의 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능에 추가된 기능입니다. 보안 Enclave의 목적은 Always Encrypted 데이터로 작업할 때 제한을 해결하는 것입니다. 이전에는 사용자가 Always Encrypted 데이터에 대한 같음 비교만 수행할 수 있었으며, 다른 작업을 하려면 데이터를 검색하고 암호 해독해야 했습니다. 보안 Enclave는 서버 쪽의 보안 Enclave 내에서 일반 텍스트 데이터에 대한 계산을 허용하여 이 제한을 해결합니다. 보안 Enclave는 SQL Server 프로세스 내의 보호된 메모리 영역으로, SQL Server 엔진 내에서 중요한 데이터를 처리하기 위한 신뢰할 수 있는 실행 환경으로 사용됩니다. 보안 Enclave는 SQL Server의 나머지 부분 및 호스팅 컴퓨터의 다른 프로세스에서 검은색 상자로 표시됩니다. 디버거를 사용하더라도 외부에서 Enclave 내의 데이터나 코드를 볼 수 없습니다.

## <a name="prerequisites"></a>필수 구성 요소
- SQL Server용 Microsoft JDBC Driver 8.2 이상이 개발 머신에 설치되어 있는지 확인합니다.
- DLL, 키 저장소 등의 환경 종속성이 올바른 경로에 있는지 확인합니다. 보안 Enclave를 사용한 Always Encrypted는 기존 [Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md) 기능의 추가 항목이며 비슷한 필수 구성 요소를 공유합니다.

> [!Note]
> JDK 8의 이전 버전을 사용하는 경우 Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files를 다운로드하여 설치해야 할 수 있습니다. zip 파일에 포함된 추가 정보에서 설치 지침 및 가능한 내보내기/가져오기 문제와 관련된 자세한 내용을 읽어야 합니다.  
>
> [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)에서 정책 파일을 다운로드할 수 있습니다.

## <a name="setting-up-secure-enclaves"></a>보안 Enclave 설정
보안 Enclave를 시작하려면 이 [자습서](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)를 따르세요. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.

## <a name="connection-string-properties"></a>연결 문자열 속성
**enclaveAttestationUrl:** 증명 서비스의 엔드포인트 URL.

**enclaveAttestationProtocol:** 증명 서비스의 프로토콜. 현재 유일하게 지원되는 값은 **HGS**(호스트 보호 서비스)입니다.

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서 보안 Enclave를 사용한 Always Encrypted를 사용하도록 설정하려면 사용자는 **columnEncryptionSetting**을 사용하도록 설정하고 위의 연결 문자열 속성 **모두**를 올바르게 설정해야 합니다.

## <a name="working-with-secure-enclaves"></a>보안 Enclave 작업
Enclave 연결 속성이 제대로 설정되면 이 기능이 투명하게 작동합니다. 이 드라이버는 쿼리가 보안 Enclave의 사용을 자동으로 요구할지 여부를 결정합니다. Enclave 계산을 트리거하는 쿼리의 예는 다음과 같습니다. [Always Encrypted Enclave 시작하기](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)에서 데이터베이스 및 테이블 설정을 찾을 수 있습니다.

다양한 쿼리는 Enclave 계산을 트리거합니다.
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL)) {
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SSN LIKE ?")) {
        p.setString(1, "%6818");
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
    
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SALARY > ?")) {
        ((SQLServerPreparedStatement) p).setMoney(1, new BigDecimal(0));
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
}
```

열에 대해 암호화를 전환하면 Enclave 계산이 트리거됩니다.
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL);Statement s = c.createStatement()) {
    s.executeUpdate("ALTER TABLE Employees ALTER COLUMN SSN CHAR(11) NULL WITH (ONLINE = ON)");
}
```

## <a name="java-8-users"></a>Java 8 사용자
이 기능을 사용하려면 RSASSA-PSA 서명 알고리즘이 필요합니다. 이 알고리즘은 JDK 11에서 추가되었지만 JDK 8에 다시 이식할 수 없습니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]의 JDK 8 버전에서 이 기능을 사용하려는 사용자는 RSASSA-PSA 서명 알고리즘을 지원하는 자체 공급자를 로드하거나 선택적인 BouncyCastleProvider 종속성을 포함해야 합니다. JDK 8이 서명 알고리즘을 백포트하거나 JDK 8의 지원 수명 주기가 종료되면 나중에 종속성이 제거됩니다.

## <a name="see-also"></a>참고 항목
[Always Encrypted와 JDBC 드라이버 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  