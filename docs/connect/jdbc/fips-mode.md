---
title: FIPS 모드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
ms.assetid: ''
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.openlocfilehash: fb8e6d19ef4359ebc16ed1089561c23724d7a34b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="fips-mode"></a>FIPS 모드
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server 용 Microsoft JDBC Driver 지원 *FIPS 140 규격 모드*합니다. Oracle에 대 한 참조 Sun JVM /는 [SunJSSE에 대 한 FIPS 140 규격 모드](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html) FIPS를 구성 하는 Oracle에서 제공 하는 섹션 JVM을 사용 하도록 설정 합니다. 

**필수 구성 요소**:
* 구성 된 JVM FIPS
* 적절 한 SSL 인증서입니다.
* 적절 한 정책 파일입니다. 
* 적절 한 구성 매개 변수입니다. 


## <a name="fips-configured-jvm"></a>구성 된 JVM FIPS

FIPS 구성에 대 한 승인 된 모듈을 참조 하려면 참조는 [FIPS 140-1 유효성을 검사 하 고 FIPS 140-2 암호화 모듈](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm)합니다. 

공급 업체는 FIPS와 JVM을 구성 하려면 몇 가지 추가 단계가 있을 수 있습니다.

### <a name="ensure-your-jvm-is-in-fips-mode"></a>FIPS 모드에서 JVM을 사용자가 확인
프로그램 JVM가 FIPS를 사용 하도록 설정 하려면 다음 코드를 실행 합니다. 

````
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
````

## <a name="appropriate-ssl-certificate"></a>적절 한 SSL 인증서
FIPS 모드에서 SQL Server를 연결 하려면 유효한 SSL 인증서가 필요 합니다. 설치 하거나 가져와서 Java 키 저장소에 클라이언트 컴퓨터 (JVM)에서 FIPS 사용 하도록 설정 합니다. 가져오기 / 적절 한 인증서를 설치 하지 않은 상태로 보안 연결을 만들 수 없는 SQL Server에 연결할 수 수 있습니다.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Java KeyStore에 SSL 인증서 가져오기
FIPS, 대개 해야 (여.cert) 인증서를 가져오려면 또는 공급자별 형식 중 하나가 PKCS를 합니다. 다음 코드 조각은 사용 하 여 SSL 인증서를 가져오고 적절 한 키 저장소 형식으로 작업 디렉터리에 저장 합니다. _TRUST_STORE_PASSWORD_ 는 Java KeyStore에 대 한 암호입니다. 

````
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

````


다음 예제는 BouncyCastle 공급자와 Azure SSL 인증서 PKCS12 형식의 가져오는 중입니다. 명명 된 작업 디렉터리에 인증서를 가져오는 _MyTrustStore_PKCS12_ 다음 코드 조각을 사용 하 여:

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>적절 한 정책 파일
일부 FIPS 공급자에 대 한 무제한 정책 jar 필요 합니다. 이러한 경우, Sun / Oracle는 Java Cryptography Extension (JCE) 무제한 Strength Jurisdiction Policy Files에 대 한 다운로드 [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) 또는 [JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)합니다. 

## <a name="appropriate-configuration-parameters"></a>적절 한 구성 매개 변수
JDBC 드라이버 FIPS 규격 모드에서를 실행 하려면 다음 표에 나와 있는 것 처럼 연결 속성을 구성 합니다. 

**속성**: 

|속성|형식|기본값|Description|참고|
|---|---|---|---|---|
|encrypt|부울 값을 ["true / false"]|"false"|JVM 암호화 속성 FIPS 사용할 수 있으면 해야 **true**||
|TrustServerCertificate|부울 값을 ["true / false"]|"false"|FIPS에 대 한 사용자는 사용자를 사용 해야 하므로 인증서 체인의 유효성을 검사 해야 **"false"** 이 속성에 대 한 값입니다. ||
|trustStore|문자열|null|인증서를 가져온 사용자 Java Keystore 파일 경로입니다. 인증서를 설치 하면에 시스템에 다음 아무 것도 전달할 필요가 없습니다. 드라이버는 cacerts 또는 jssecacerts 파일을 사용합니다.||
|trustStorePassword|문자열|null|trustStore 데이터의 무결성을 검사하는 데 사용되는 암호입니다.||
|fips|부울 값을 ["true / false"]|"false"|이 속성은 같아야 fips JVM을 사용 하도록 설정 된 **true**|6.1.4에 추가 (안정적인 6.2.2 릴리스)||
|fipsProvider|문자열|null|JVM에 구성 된 FIPS 공급자입니다. 예를 들어 BCFIPS 또는 SunPKCS11 NSS |6.1.2에 추가 (안정적인 6.2.2 해제), 세부 정보를 보려면 6.4.0-에서 사용 되지 않는 [여기](https://github.com/Microsoft/mssql-jdbc/pull/460)합니다.|
|trustStoreType|문자열|JKS|FIPS 모드 집합 트러스트 저장소 형식에 대 한 PKCS12 또는 유형 중 하나에 정의 된 FIPS 공급자 |6.1.2에 추가 (안정적인 6.2.2 릴리스)||



  
