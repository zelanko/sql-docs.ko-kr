---
title: Hadoop 연결 관리자 - SQL Server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d0f00f507a7347e729a6531261c963cdeae41b62
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="hadoop-connection-manager"></a>Hadoop 연결 관리자
  SSIS(SQL Server Integration Services) 패키지는 Hadoop 연결 관리자를 통해 속성에 대해 지정된 값을 사용하여 Hadoop 클러스터에 연결할 수 있습니다.  
  
## <a name="configure-the-hadoop-connection-manager"></a>Hadoop 연결 관리자 구성  
  
1.  **SSIS 연결 관리자 추가** 대화 상자에서 **Hadoop** > **추가**를 선택합니다. **Hadoop 연결 관리자 편집기** 대화 상자가 열립니다.  
  
2.  관련 Hadoop 클러스터 정보를 구성하려면 왼쪽 창에서 **WebHCat** 또는 **WebHDFS** 탭을 선택합니다.
  
3.  Hadoop에서 하이브 또는 Pig 작업을 호출하기 위해 **WebHCat** 옵션을 사용하도록 설정하는 경우에는 다음 단계를 수행합니다. 
  
    1.  **WebHCat 호스트**에는 WebHCat 서비스를 호스트하는 서버를 입력합니다.  
  
    2.  **WebHCat 포트**에는 WebHCat 서비스의 포트(기본값: 50111)를 입력합니다.  
  
    3.  WebHCat 서비스에 액세스하는 데 사용할 **인증** 방법을 선택합니다. 사용 가능한 값은 **기본** 및 **Kerberos**입니다.  
  
         ![기본 인증을 사용하는 Hadoop 연결 관리자 편집기의 스크린샷](../../integration-services/connection-manager/media/hadoop-cm-basic.png "기본 인증을 사용하는 Hadoop 연결 관리자 편집기")  
  
         ![Kerberos 인증을 사용하는 Hadoop 연결 관리자 편집기의 스크린샷](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "Kerberos 인증을 사용하는 Hadoop 연결 관리자 편집기")  
  
    4.  **WebHCat 사용자**에는 WebHCat 액세스 권한이 있는 **사용자** 를 입력합니다.  
  
    5.  **Kerberos** 인증을 선택하는 경우 사용자의 **암호** 및 **도메인**을 입력합니다.  
  
4.  HDFS에서/HDFS로 데이터를 복사하기 위해 **WebHDFS** 옵션을 사용하도록 설정하는 경우에는 다음 단계를 수행합니다. 
  
    1.  **WebHDFS 호스트**에는 WebHDFS 서비스를 호스트하는 서버를 입력합니다.  
  
    2.  **WebHDFS 포트**에는 WebHDFS 서비스의 포트(기본값: 50070)를 입력합니다.  
  
    3.  WebHDFS 서비스에 액세스하는 데 사용할 **인증** 방법을 선택합니다. 사용 가능한 값은 **기본** 및 **Kerberos**입니다.  
  
    4.  **WebHDFS 사용자**에는 HDFS 액세스 권한이 있는 사용자를 입력합니다.  
  
    5.  **Kerberos** 인증을 선택하는 경우 사용자의 **암호** 및 **도메인**을 입력합니다.  
  
5.  **연결 테스트**를 선택합니다. 사용하도록 설정한 연결만 테스트합니다.  
  
6.  **확인**을 선택하여 대화 상자를 닫습니다.  

## <a name="connect-with-kerberos-authentication"></a>Kerberos 인증을 사용하여 연결
Hadoop 연결 관리자에 Kerberos 인증을 사용할 수 있도록 온-프레미스 환경을 설정하는 옵션은 두 가지이며, 상황에 더 적합한 옵션을 선택하면 됩니다.
-   옵션 1: [Kerberos 영역에 SSIS 컴퓨터 조인](#kerberos-join-realm)
-   옵션 2: [Windows 도메인과 Kerberos 영역 간의 상호 신뢰 사용](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>옵션 1: Kerberos 영역에 SSIS 컴퓨터 조인

#### <a name="requirements"></a>요구 사항:

-   게이트웨이 컴퓨터가 Kerberos 영역을 조인해야 하며 Windows 도메인은 조인할 수 없습니다.

#### <a name="how-to-configure"></a>구성 방법:

SSIS 컴퓨터에서 다음을 수행합니다.

1.  **Ksetup** 유틸리티를 실행하여 KDC(Kerberos 키 배포 센터) 서버 및 영역을 구성합니다.

    Kerberos 영역은 Windows 도메인과 다르므로 컴퓨터가 작업 그룹의 구성원으로 구성되어 있어야 합니다. 다음 예제와 같이 Kerberos 영역을 설정하고 KDC 서버를 추가합니다. 필요에 따라 `REALM.COM`을 해당하는 고유한 영역으로 바꿉니다.

    ```    
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    ```

    이러한 명령을 실행한 후 컴퓨터를 다시 시작합니다.

2.  **Ksetup** 명령으로 구성을 확인합니다. 출력이 다음 샘플과 같아야 합니다.

    ```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
    ```

### <a name="kerberos-mutual-trust"> </a>옵션 2: Windows 도메인과 Kerberos 영역 간의 상호 신뢰 사용

#### <a name="requirements"></a>요구 사항:
-   게이트웨이 컴퓨터가 Windows 도메인을 조인해야 합니다.
-   도메인 컨트롤러의 설정을 업데이트할 수 있는 권한이 필요합니다.

#### <a name="how-to-configure"></a>구성 방법:

> [!NOTE]
> 필요에 따라 다음 자습서의 `REALM.COM` 및 `AD.COM`을 해당하는 고유한 영역 및 도메인 컨트롤러로 바꿉니다.

KDC 서버에서 다음을 수행합니다.

1.  **krb5.conf** 파일에서 KDC 구성을 편집합니다. 다음 구성 템플릿을 참조하여 KDC가 Windows 도메인을 신뢰하도록 허용합니다. 기본적으로 이 구성은 **/etc/krb5.conf**에 있습니다.

    ```
    [logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

    [libdefaults]
    default_realm = REALM.COM
    dns_lookup_realm = false
    dns_lookup_kdc = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true

    [realms]
    REALM.COM = {
        kdc = node.REALM.COM
        admin_server = node.REALM.COM
        }
    AD.COM = {
        kdc = windc.ad.com
        admin_server = windc.ad.com
        }

    [domain_realm]
    .REALM.COM = REALM.COM
    REALM.COM = REALM.COM
    .ad.com = AD.COM
    ad.com = AD.COM

    [capaths]
    AD.COM = {
        REALM.COM = .
        }
    ```

    구성 후 KDC 서비스를 다시 시작합니다.

2.  KDC 서버에서 **krbtgt/REALM.COM@AD.COM**이라는 보안 주체를 준비합니다. 다음 명령을 사용합니다.

    `Kadmin> addprinc krbtgt/REALM.COM@AD.COM`

3.  **hadoop.security.auth_to_local** HDFS 서비스 구성 파일에 `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`를 추가합니다.

도메인 컨트롤러에서 다음을 수행합니다.

1.  다음 **Ksetup** 명령을 실행하여 영역 항목을 추가합니다.

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

2.  Windows 도메인과 Kerberos 영역 간의 신뢰를 설정합니다. 다음 예제에서 `[password]`는 보안 주체 **krbtgt/REALM.COM@AD.COM**의 암호입니다.

    `C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /password:[password]`

3.  Kerberos에 사용할 암호화 알고리즘을 선택합니다.

    1. **서버 관리자** > **그룹 정책 관리** > **도메인**으로 이동합니다. 여기에서 **그룹 정책 개체** > **Default or Active Domain Policy**(기본값 또는 활성 도메인 정책) > **편집**으로 이동합니다.

    2. **그룹 정책 관리 편집기** 팝업 창에서 **컴퓨터 구성** > **정책** > **Windows 설정**으로 이동합니다. 여기에서 **보안 설정** > **로컬 정책** > **보안 옵션**으로 이동합니다. **네트워크 보안: Kerberos에 허용된 암호화 유형 구성**을 구성합니다.

    3. KDC에 연결하는 데 사용할 암호화 알고리즘을 선택합니다. 일반적으로 모든 옵션을 선택할 수 있습니다.

        ![Kerberos에 대한 암호화 유형의 스크린샷](media/hadoop-connection-manager/config-encryption-types-for-kerberos.png)

    4. **Ksetup** 명령을 사용하여 특정 영역에서 사용할 암호화 알고리즘을 지정합니다.

        `C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96`

4.  Windows 도메인에서 Kerberos 주체를 사용하려면 도메인 계정과 Kerberos 주체 사이의 매핑을 만듭니다.

    1. **관리 도구** > **Active Directory 사용자 및 컴퓨터**로 이동합니다.

    2. **보기** > **고급 기능**을 선택하여 고급 기능을 구성합니다.

    3. 매핑을 만들 계정을 찾고 마우스 오른쪽 단추를 클릭하여 **이름 매핑**을 표시한 다음, **Kerberos 이름** 탭을 선택합니다.

    4. 영역에서 보안 주체를 추가합니다.

        ![보안 식별자 매핑 대화 상자의 스크린샷](media/hadoop-connection-manager/map-security-identity.png)

게이트웨이 컴퓨터에서 다음을 수행합니다.

다음 **Ksetup** 명령을 실행하여 영역 항목을 추가합니다.

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

## <a name="see-also"></a>관련 항목:  
 [Hadoop 하이브 태스크](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Hadoop Pig 태스크](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Hadoop 파일 시스템 태스크](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
