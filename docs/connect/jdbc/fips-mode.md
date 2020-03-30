---
title: JDBC에서의 FIPS 모드 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
manager: kenvh
ms.openlocfilehash: 63681ee474d4993e248bf02dcabd9065317ffa39
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028062"
---
# <a name="fips-mode"></a>FIPS 모드

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server용 Microsoft JDBC 드라이버는 *FIPS 140을 준수*하도록 구성된 JVM에서 실행을 지원합니다.

#### <a name="prerequisites"></a>사전 요구 사항

- FIPS 구성 JVM
- 적절한 SSL 인증서
- 적절한 정책 파일
- 적절한 구성 매개 변수

## <a name="fips-configured-jvm"></a>FIPS 구성 JVM

일반적으로 애플리케이션은 FIPS 준수 암호화 공급자를 사용하도록 `java.security` 파일을 구성할 수 있습니다. FIPS 140 준수 구성 방법에 대해서는 JVM 관련 설명서를 참조하세요.

FIPS 구성에 대해 승인된 모듈은 [암호화 모듈 유효성 검사 프로그램의 유효성 검사 완료 모듈](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules)에서 확인하실 수 있습니다.

공급업체는 FIPS로 JVM을 구성하기 위해 몇 가지 추가 단계를 밟아야 할 수 있습니다.

## <a name="appropriate-ssl-certificate"></a>적절한 SSL 인증서
FIPS 모드에서 SQL Server에 연결하려면 유효한 SSL 인증서가 필요합니다. FIPS가 사용 설정된 클라이언트 컴퓨터(JVM)의 Java 키 저장소에 이 인증서를 설치하거나 가져옵니다.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Java 키 저장소에서 SSL 인증서 가져오기
FIPS의 경우 PKCS 또는 공급자별 형식으로 인증서(.cert)를 가져와야 할 가능성이 높습니다.
다음 코드 조각을 사용하여 SSL 인증서를 가져온 다음 적절한 키 저장소 형식의 작업 디렉터리에 저장합니다. Java 키 저장소의 암호는 _TRUST\_STORE\_PASSWORD_입니다.

```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```

다음 예제에서는 BouncyCastle 공급자를 사용하여 PKCS12 형식의 Azure SSL 인증서를 가져옵니다. 인증서는 다음 코드 조각을 사용하여 _MyTrustStore\_PKCS12_이라는 작업 디렉터리에서 가져옵니다.

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>적절한 정책 파일
일부 FIPS 공급자에게는 무제한 정책 jar이 필요합니다. 이와 같은 상황에서는 Sun/Oracle의 경우 [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) 또는 [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)용 JCE(Java Cryptography Extension) Unlimited Strength Jurisdiction Policy Files를 다운로드합니다. 

## <a name="appropriate-configuration-parameters"></a>적절한 구성 매개 변수
FIPS 준수 모드에서 JDBC 드라이버를 실행하려면 연결 속성을 다음 표와 같이 구성합니다. 

#### <a name="properties"></a>속성 

|속성|Type|기본값|Description|메모|
|---|---|---|---|---|
|encrypt|부울 ["true / false"]|"false"|FIPS가 사용 설정된 JVM의 경우 암호화 속성이 **true**여야 합니다.||
|TrustServerCertificate|부울 ["true / false"]|"false"|FIPS의 경우 사용자의 인증서 체인 유효성 검사가 필요하므로 사용자가 이 속성에 대해 **"false"** 값을 사용해야 합니다. ||
|trustStore|String|null|인증서를 가져온 Java 키 저장소 파일 경로입니다. 시스템에 인증서를 설치하는 경우에는 아무것도 전달할 필요가 없습니다. 드라이버에서는 cacerts 또는 jssecacerts 파일을 사용합니다.||
|trustStorePassword|String|null|trustStore 데이터의 무결성을 검사하는 데 사용되는 암호입니다.||
|fips|부울 ["true / false"]|"false"|FIPS가 사용 설정된 JVM의 경우 이 속성이 **true**여야 합니다.|6\.1.4에 추가됨(안정적 릴리스는 6.2.2)||
|fipsProvider|String|null|JVM에서 구성된 FIPS 공급자입니다. BCFIPS 또는 SunPKCS11-NSS를 예로 들 수 있습니다. |6\.1.2에 추가되었고(안정적 릴리스는 6.2.2) 6.4.0에서는 사용되지 않습니다. 자세한 내용은 [여기](https://github.com/Microsoft/mssql-jdbc/pull/460)를 참조하세요.|
|trustStoreType|String|JKS|FIPS 모드 설정 신뢰 저장소 유형으로는 PKCS12나 FIPS 공급자에 의해 정의된 유형이 있습니다. |6\.1.2에 추가됨(안정적 릴리스는 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
