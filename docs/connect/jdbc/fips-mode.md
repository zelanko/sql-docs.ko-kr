---
title: FIPS 모드 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.openlocfilehash: 792d843a2c11c7bde016aec513df9c8724b366b4
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278854"
---
# <a name="fips-mode"></a>FIPS 모드
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server 용 Microsoft JDBC Driver 지원 *FIPS 140 규격 모드*합니다. Oracle에 대 한 Sun JVM 참조 / 합니다 [SunJSSE에 대 한 FIPS 140 규격 모드](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html) FIPS를 구성 하는 Oracle에서 제공 하는 섹션 JVM을 사용 하도록 설정 합니다. 

**필수 조건**:
* 구성 된 JVM FIPS
* 적절 한 SSL 인증서입니다.
* 적절 한 정책 파일입니다. 
* 적절 한 구성 매개 변수입니다. 


## <a name="fips-configured-jvm"></a>구성 된 JVM FIPS

FIPS 구성에 대 한 승인 된 모듈 참조에 [유효성이 검사 FIPS 140-1 및 FIPS 140-2 암호화 모듈](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm)합니다. 

공급 업체는 FIPS를 사용 하 여 JVM을 구성 하려면 몇 가지 추가 단계가 있을 수 있습니다.

### <a name="ensure-your-jvm-is-in-fips-mode"></a>FIPS 모드에서 프로그램 JVM을 확인 합니다.
에 JVM은 FIPS 사용을 위해 다음 코드 조각을 실행 합니다. 

```java
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
```

## <a name="appropriate-ssl-certificate"></a>적절 한 SSL 인증서
FIPS 모드에서 SQL Server에 연결 하려면 유효한 SSL 인증서가 필요 합니다. 설치 또는 Java 키 저장소 (JVM) 클라이언트 컴퓨터에서 FIPS가 활성화 하는 위치에서 가져옵니다.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Java KeyStore에서 SSL 인증서 가져오기
FIPS를 대부분 해야 (.cert) 인증서를 가져오려면 두 PKCS 또는 공급자별 형식으로 합니다. 다음 조각을 사용 하 여 SSL 인증서를 가져오고 적절 한 키 저장소 형식으로 작업 디렉터리에 저장 합니다. _TRUST_STORE_PASSWORD_ Java KeyStore 암호입니다. 

```java
    public void saveGenericKeyStore(String provider, String trustStoreType, String certName, String certPath) throws KeyStoreException, CertificateException, NoSuchAlgorithmException, NoSuchProviderException, IOException {
        KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
        FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
        ks.load(null, null);
        ks.setCertificateEntry(certName, getCertificate(certPath));
        ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
        os.flush();
        os.close();
    }

    private Certificate getCertificate(String pathName) throws FileNotFoundException, CertificateException {
        FileInputStream fis = new FileInputStream(pathName);
        CertificateFactory cf = CertificateFactory.getInstance("X.509");
        return cf.generateCertificate(fis);
    }

```


다음 예제에서는 BouncyCastle 공급자를 사용 하 여 PKCS12 형식의 Azure SSL 인증서를 가져오는 중입니다. 명명 된 작업 디렉터리에 인증서를 가져올 _MyTrustStore_PKCS12_ 다음 조각을 사용 하 여:

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>적절 한 정책 파일
일부 FIPS 공급자 무제한 정책 jar가 필요 합니다. 이러한 경우, Sun / Oracle는 Java Cryptography Extension (JCE) 무제한 Strength Jurisdiction Policy Files에 대 한 다운로드 [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) 또는 [JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)합니다. 

## <a name="appropriate-configuration-parameters"></a>적절 한 구성 매개 변수
JDBC 드라이버를 FIPS 규격 모드에서 실행 하려면 다음 표에 나와 있는 것 처럼 연결 속성을 구성 합니다. 

**속성**: 

|속성|형식|Default|설명|참고|
|---|---|---|---|---|
|encrypt|부울 ["true / false"]|"false"|FIPS 사용 JVM 속성을 암호화 해야 **true**||
|TrustServerCertificate|부울 ["true / false"]|"false"|FIPS에 대 한 사용자는 사용자가 사용 해야 하므로 인증서 체인의 유효성을 검사 해야 **"false"** 이 속성의 값입니다. ||
|trustStore|String|null|인증서를 가져온 위치에 Java Keystore 파일 경로입니다. 인증서에서 시스템을 무엇이 든 전달할 필요가 없습니다 설치 하는 경우. 드라이버는 cacerts 또는 jssecacerts 파일을 사용합니다.||
|trustStorePassword|String|null|trustStore 데이터의 무결성을 검사하는 데 사용되는 암호입니다.||
|fips|부울 ["true / false"]|"false"|이 속성은 같아야 FIPS 사용 JVM **true**|6.1.4에 추가 (안정적인 6.2.2 릴리스)||
|fipsProvider|String|null|JVM에 구성 된 FIPS 공급자입니다. 예를 들어 BCFIPS 또는 SunPKCS11 NSS |6.1.2에 추가 (안정적인 6.2.2 릴리스), 세부 정보를 보려면 6.4.0-에서 사용 되지 않음 [여기](https://github.com/Microsoft/mssql-jdbc/pull/460)합니다.|
|trustStoreType|String|JKS|FIPS 모드 집합 신뢰 저장소 형식에 대 한 PKCS12 또는 형식 공급자가 정의한 FIPS |6.1.2에 추가 (안정적인 6.2.2 릴리스)||



  
