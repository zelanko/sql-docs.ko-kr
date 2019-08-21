---
title: JDBC에서 FIPS 모드 | Microsoft Docs
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
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028062"
---
# <a name="fips-mode"></a>FIPS 모드

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server 용 Microsoft JDBC Driver는 *FIPS 140 규격*으로 구성 된 jvm에서의 실행을 지원 합니다.

#### <a name="prerequisites"></a>사전 요구 사항

- FIPS 구성 JVM
- 적절 한 SSL 인증서
- 적절 한 정책 파일
- 적절 한 구성 매개 변수

## <a name="fips-configured-jvm"></a>FIPS 구성 JVM

일반적으로 응용 프로그램은 `java.security` FIPS 호환 암호화 공급자를 사용 하도록 파일을 구성할 수 있습니다. FIPS 140 준수를 구성 하는 방법에 대 한 JVM 관련 설명서를 참조 하세요.

FIPS 구성에 대해 승인 된 모듈을 보려면 [암호화 모듈 유효성 검사 프로그램의 검증 된 모듈](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules)을 참조 하세요.

공급 업체에는 FIPS를 사용 하 여 JVM을 구성 하기 위한 몇 가지 추가 단계가 있을 수 있습니다.

## <a name="appropriate-ssl-certificate"></a>적절 한 SSL 인증서
FIPS 모드에서 SQL Server에 연결 하려면 유효한 SSL 인증서가 필요 합니다. FIPS를 사용 하도록 설정 된 클라이언트 컴퓨터 (JVM)의 Java 키 저장소에 설치 하거나 가져옵니다.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Java 키 저장소에서 SSL 인증서 가져오기
FIPS의 경우 PKCS 또는 공급자별 형식으로 인증서 (cert)를 가져와야 할 가능성이 높습니다.
다음 코드 조각을 사용 하 여 SSL 인증서를 가져온 다음 적절 한 키 저장소 형식의 작업 디렉터리에 저장 합니다. _신뢰\_저장소\_암호_ 는 Java 키 저장소의 암호입니다.

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

다음 예제에서는 BouncyCastle 공급자를 사용 하 여 PKCS12 형식의 Azure SSL 인증서를 가져옵니다. 다음 코드 조각을 사용 하 여 _MyTrustStore\_PKCS12_ 이라는 작업 디렉터리에서 인증서를 가져옵니다.

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>적절 한 정책 파일
일부 FIPS 공급자의 경우 무제한 정책 jar 필요 합니다. 이러한 경우 Sun/Oracle의 경우 [jre 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) 또는 [jre 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)에 대 한 JCE (Java Cryptography Extension) 무제한 수준 관할지 정책 파일을 다운로드 합니다. 

## <a name="appropriate-configuration-parameters"></a>적절 한 구성 매개 변수
다음 표와 같이 FIPS 규격 모드에서 JDBC 드라이버를 실행 하려면 연결 속성을 구성 합니다. 

#### <a name="properties"></a>속성 

|속성|형식|Default|설명|참고|
|---|---|---|---|---|
|encrypt|부울 ["true / false"]|"false"|FIPS를 사용 하는 JVM 암호화 속성은 **true** 여야 합니다.||
|TrustServerCertificate|부울 ["true / false"]|"false"|FIPS의 경우 사용자는 인증서 체인의 유효성을 검사 해야 하므로 사용자는이 속성에 대해 **"false"** 값을 사용 해야 합니다. ||
|trustStore|String|null|인증서를 가져온 Java 키 저장소 파일 경로입니다. 시스템에 인증서를 설치 하는 경우 아무 것도 전달할 필요가 없습니다. 드라이버에서 cacerts 또는 jssecacerts 파일을 사용 합니다.||
|trustStorePassword|String|null|trustStore 데이터의 무결성을 검사하는 데 사용되는 암호입니다.||
|fips|부울 ["true / false"]|"false"|FIPS를 사용 하는 JVM의 경우이 속성은 **true** 여야 합니다.|6\.1.4 (안정적인 릴리스 6.2.2)에 추가 됨||
|fipsProvider|String|null|JVM에서 구성 된 FIPS 공급자. 예: BCFIPS 또는 SunPKCS11-NSS |6\.1.2 (안정적인 릴리스 6.2.2)에서 추가 되었으며 v6.4.0에서 사용 되지 않습니다. 자세한 내용은 [여기](https://github.com/Microsoft/mssql-jdbc/pull/460)를 참조 하세요.|
|trustStoreType|String|JKS|FIPS 모드 설정 신뢰 저장소 유형에는 FIPS 공급자에 의해 정의 된 PKCS12 또는 유형 중 하나가 있습니다. |6\.1.2 (안정적인 릴리스 6.2.2)에 추가 됨||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
