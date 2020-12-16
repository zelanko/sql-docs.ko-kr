---
title: PolyBase Kerberos 연결 문제 해결 | Microsoft Docs
description: Kerberos 보안 Hadoop 클러스터를 사용하여 PolyBase 인증 문제를 해결할 때는 PolyBase에서 기본 제공하는 대화형 진단을 사용할 수 있습니다.
author: alazad-msft
ms.author: alazad
ms.reviewer: mikeray
ms.technology: polybase
ms.devlang: ''
ms.topic: conceptual
ms.date: 10/02/2019
ms.prod: sql
ms.prod_service: polybase, sql-data-warehouse, pdw
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: edf0b261b6046d63e037e601ab9e92dd13d8728e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464784"
---
# <a name="troubleshoot-polybase-kerberos-connectivity"></a>PolyBase Kerberos 연결 문제 해결

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

PolyBase에 기본 제공된 대화형 진단을 사용하면 Kerberos 보안 Hadoop 클러스터에 대해 PolyBase를 사용할 때 인증 문제를 해결할 수 있습니다. 

이 문서는 기본 제공 진단을 활용하여 이러한 문제의 디버깅 프로세스를 살펴보기 위한 가이드입니다.

> [!TIP]
> 이 가이드의 단계를 수행하는 대신, Kerberos 보안 HDFS 클러스터에 외부 테이블을 만드는 중 HDFS Kerberos 오류가 발생할 경우 PolyBase에 대한 HDFS Kerberos 연결 문제를 해결하기 위해 [HDFS Kerberos 테스터](https://github.com/microsoft/sql-server-samples/tree/master/samples/manage/hdfs-kerberos-tester)를 실행하도록 선택할 수 있습니다. .
> 이 도구는 HDFS Kerberos 설정 문제, 즉 사용자 이름/암호의 잘못된 구성과 클러스터 Kerberos 설정의 잘못된 구성 확인에 집중할 수 있도록 SQL Server 이외의 문제를 제외하는 데 도움이 됩니다.      
> 이 도구는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와는 독립적입니다. Jupyter Notebook으로 제공되며, Azure Data Studio가 필요합니다.

## <a name="prerequisites"></a>필수 구성 요소

1. PolyBase가 설치된 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM CU6/[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU3/[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 이상
1. Kerberos(Active Directory 또는 MIT)로 보호된 Hadoop 클러스터(Cloudera 또는 Hortonworks)

## <a name="introduction"></a>소개
먼저 Kerberos 프로토콜을 개략적으로 이해할 수 있도록 도와드립니다. 관련된 행위자는 다음 세 가지입니다.

1. Kerberos 클라이언트(SQL Server)
1. 보안 리소스(HDFS, MR2, YARN, 작업 기록 등)
1. 키 배포 센터(Active Directory에서는 도메인 컨트롤러라고 함)

Kerberos가 Hadoop 클러스터에서 구성되면 각 Hadoop 보안 리소스는 고유한 **SPN(서비스 사용자 이름)** 을 사용하여 **KDC(키 배포 센터)** 에 등록됩니다. 목표는 클라이언트가 임시 사용자 티켓인 **TGT(허용 티켓)** 를 얻어, 액세스하려는 특정 SPN에 대해 또 다른 임시 티켓인 **ST(서비스 티켓)** 를 KDC에서 요청하는 것입니다.  

PolyBase에서 Kerberos 보안 리소스에 대해 인증이 요청되면 다음과 같은 4번 왕복 핸드셰이크가 수행됩니다.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 KDC에 연결하고 사용자의 TGT를 가져옵니다. TGT는 KDC 프라이빗 키를 사용하여 암호화됩니다.
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 Hadoop 보안 리소스인 HDFS를 호출하고 ST가 필요한 SPN을 확인합니다.
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 KDC로 돌아가고, TGT를 다시 전달하고, ST를 요청하여 해당하는 특정 보안 리소스에 액세스합니다. ST는 보안 서비스의 프라이빗 키를 사용하여 암호화됩니다.
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 ST를 Hadoop에 전달하고 인증되어 해당 서비스에 대해 세션이 만들어집니다.

![PolyBase SQL Server](./media/polybase-sqlserver.png)

인증 관련 문제는 위 4단계 중 하나 이상에 속합니다. 더 빠르게 디버그할 수 있도록 PolyBase에서는 실패 지점을 식별하는 데 도움이 되는 통합 진단 도구를 도입했습니다.

## <a name="troubleshooting"></a>문제 해결

PolyBase에는 Hadoop 클러스터의 속성이 포함된 다음과 같은 구성 XML 파일이 있습니다.

- core-site.xml
- hdfs-site.xml
- hive-site.xml
- jaas.conf
- mapred-site.xml
- yarn-site.xml

이러한 파일은 다음 위치에 있습니다.

`\[System Drive\]:{install path}\{MSSQL##.INSTANCENAME}\MSSQL\Binn\PolyBase\Hadoop\conf`

예를 들어 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 기본값은 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\PolyBase\Hadoop\conf`입니다.

**core-site.xml** 을 업데이트하고 아래 세 가지 속성을 추가합니다. 환경에 따라 값을 설정합니다.

```xml
<property>
    <name>polybase.kerberos.realm</name>
    <value>CONTOSO.COM</value>
</property>
<property>
    <name>polybase.kerberos.kdchost</name>
    <value>kerberos.contoso.com</value>
</property>
<property>
    <name>hadoop.security.authentication</name>
    <value>KERBEROS</value>
</property>
```
> [!NOTE]
> `polybase.kerberos.realm` 속성 값은 모두 대문자여야 합니다.

나중에 푸시다운 작업이 필요한 경우 다른 XML도 업데이트해야 하지만 이 파일만 구성해도 HDFS 파일 시스템에 액세스할 수는 있습니다.

이 도구는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 독립적으로 실행되므로, SQL Server가 실행되고 있지 않아도 되고 구성 XML을 업데이트하는 경우 SQL Server를 다시 시작하지 않아도 됩니다. 이 도구를 실행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치된 호스트에서 다음 명령을 실행합니다.

```cmd
> cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\PolyBase  
> java -classpath ".\Hadoop\conf;.\Hadoop\*;.\Hadoop\HDP2_2\*" com.microsoft.polybase.client.HdfsBridge {Name Node Address} {Name Node Port} {Service Principal} {Filepath containing Service Principal's Password} {Remote HDFS file path (optional)}
```

## <a name="arguments"></a>인수

| 인수 | Description|
| --- | --- |
| Name Node Address | 이름 노드의 IP 또는 FQDN입니다. CREATE EXTERNAL DATA SOURCE T-SQL의 "LOCATION" 인수를 가리킵니다. 참고: SQL Server 2019 버전의 도구를 사용하려면 *hdfs:\/\/* 가 IP 또는 FQDN 앞에 와야 합니다.|
| Name Node Port | 이름 노드의 포트입니다. CREATE EXTERNAL DATA SOURCE T-SQL의 "LOCATION" 인수를 가리킵니다. 예: 8020 |
| Service Principal | KDC의 관리 서비스 사용자입니다. `CREATE DATABASE SCOPED CREDENTIAL` T-SQL에서 "IDENTITY" 인수와 일치합니다.|
| Service Password | 암호를 콘솔에 입력하는 대신 파일에 저장하고 여기에 파일 경로를 전달합니다. 파일의 내용이 `CREATE DATABASE SCOPED CREDENTIAL` T-SQL에서 "SECRET" 인수로 사용하는 내용과 일치해야 합니다. |
| *원격 HDFS 파일 경로(선택 사항)* | 액세스할 기존 파일의 경로입니다. 지정하지 않으면 루트 “/”가 사용됩니다. |

## <a name="example"></a>예제

```cmd
java -classpath ".\Hadoop\conf;.\Hadoop\*;.\Hadoop\HDP2_2\*" com.microsoft.polybase.client.HdfsBridge 10.193.27.232 8020 admin_user C:\temp\kerberos_pass.txt
```

출력에는 향상된 디버깅을 위해 자세한 정보가 포함되어 있지만, MIT 또는 AD 중 무엇을 사용하든 네 개의 기본 검사점만 살펴보면 됩니다. 이들 검사점은 위에서 설명한 4개 단계에 해당합니다. 

다음은 MIT KDC 출력의 일부입니다. MIT 및 AD의 전체 샘플 출력은 이 문서 끝에 있는 참조에서 확인할 수 있습니다.

## <a name="checkpoint-1"></a>검사점 1
`Server Principal = krbtgt/MYREALM.COM@MYREALM.COM`인 티켓의 16진수 덤프여야 합니다. KDC에 인증되고 TGT를 받은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 나타냅니다. 이 덤프가 없으면 Hadoop이 아닌 KDC와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에 문제가 있습니다.

PolyBase는 AD와 MIT 간의 트러스트 관계를 지원하지 **않으며** Hadoop 클러스터에 구성된 동일한 KDC에 대해 구성해야 합니다. 이러한 환경에서는 해당 KDC에 서비스 계정을 수동으로 만들고 해당 계정을 사용하여 인증을 수행하면 됩니다.

```cmd
|>>> KrbAsReq creating message 
 >>> KrbKdcReq send: kdc=kerberos.contoso.com UDP:88, timeout=30000, number of retries =3, #bytes=143 
 >>> KDCCommunication: kdc=kerberos.contoso.com UDP:88, timeout=30000,Attempt =1, #bytes=143 
 >>> KrbKdcReq send: #bytes read=646 
 >>> KdcAccessibility: remove kerberos.contoso.com 
 >>> EType: sun.security.krb5.internal.crypto.Des3CbcHmacSha1KdEType 
 >>> KrbAsRep cons in KrbAsReq.getReply myuser 
 [2017-04-25 21:34:33,548] INFO 687[main] - com.microsoft.polybase.client.KerberosSecureLogin.secureLogin(KerberosSecureLogin.java:97) - Subject: 
 Principal: admin_user@CONTOSO.COM 
 Private Credential: Ticket (hex) = 
 0000: 61 82 01 48 30 82 01 44 A0 03 02 01 05 A1 0E 1B a..H0..D........ 
 0010: 0C 41 50 53 48 44 50 4D 53 2E 43 4F 4D A2 21 30 .CONTOSO.COM.!0 
 0020: 1F A0 03 02 01 02 A1 18 30 16 1B 06 6B 72 62 74 ........0...krbt 
 0030: 67 74 1B 0C 41 50 53 48 44 50 4D 53 2E 43 4F 4D gt..CONTOSO.COM 
 0040: A3 82 01 08 30 82 01 04 A0 03 02 01 10 A1 03 02 ....0........... 
 *[...Condensed...]* 
 0140: 67 6D F6 41 6C EB E0 C3 3A B2 BD B1 gm.Al...:... 
 Client Principal = admin_user@CONTOSO.COM 
 Server Principal = krbtgt/CONTOSO.COM@CONTOSO.COM 
 *[...Condensed...]* 
 [2017-04-25 21:34:34,500] INFO 1639[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1579) - Successfully authenticated against KDC server. 
```

## <a name="checkpoint-2"></a>검사점 2
PolyBase가 HDFS에 액세스하려고 시도하며 요청에 필요한 서비스 티켓이 포함되어 있지 않으므로 액세스에 실패합니다.

```cmd
 [2017-04-25 21:34:34,501] INFO 1640[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1584) - Attempting to access external filesystem at URI: hdfs://10.193.27.232:8020 
 Found ticket for admin_user@CONTOSO.COM to go to krbtgt/CONTOSO.COM@CONTOSO.COM expiring on Wed Apr 26 21:34:33 UTC 2017 
 Entered Krb5Context.initSecContext with state=STATE_NEW 
 Found ticket for admin_user@CONTOSO.COM to go to krbtgt/CONTOSO.COM@CONTOSO.COM expiring on Wed Apr 26 21:34:33 UTC 2017 
 Service ticket not found in the subject 
```

## <a name="checkpoint-3"></a>검사점 3
두 번째 16진수 덤프는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 TGT를 사용하여 KDC에서 이름 노드 SPN에 적용되는 서비스 티켓을 가져왔음을 나타냅니다.

```cmd
 >>> KrbKdcReq send: kdc=kerberos.contoso.com UDP:88, timeout=30000, number of retries =3, #bytes=664 
 >>> KDCCommunication: kdc=kerberos.contoso.com UDP:88, timeout=30000,Attempt =1, #bytes=664 
 >>> KrbKdcReq send: #bytes read=669 
 >>> KdcAccessibility: remove kerberos.contoso.com 
 >>> EType: sun.security.krb5.internal.crypto.Des3CbcHmacSha1KdEType 
 >>> KrbApReq: APOptions are 00100000 00000000 00000000 00000000 
 >>> EType: sun.security.krb5.internal.crypto.Des3CbcHmacSha1KdEType 
 Krb5Context setting mySeqNumber to: 1033039363 
 Created InitSecContextToken: 
 0000: 01 00 6E 82 02 4B 30 82 02 47 A0 03 02 01 05 A1 ..n..K0..G...... 
 0010: 03 02 01 0E A2 07 03 05 00 20 00 00 00 A3 82 01 ......... ...... 
 0020: 63 61 82 01 5F 30 82 01 5B A0 03 02 01 05 A1 0E ca.._0..[....... 
 0030: 1B 0C 41 50 53 48 44 50 4D 53 2E 43 4F 4D A2 26 ..CONTOSO.COM.& 
 0040: 30 24 A0 03 02 01 00 A1 1D 30 1B 1B 02 6E 6E 1B 0$.......0...nn. 
 0050: 15 73 68 61 73 74 61 2D 68 64 70 32 35 2D 30 30 .hadoop-hdp25-00 
 0060: 2E 6C 6F 63 61 6C A3 82 01 1A 30 82 01 16 A0 03 .local....0..... 
 0070: 02 01 10 A1 03 02 01 01 A2 82 01 08 04 82 01 04 ................ 
 *[...Condensed...]* 
 0240: 03 E3 68 72 C4 D2 8D C2 8A 63 52 1F AE 26 B6 88 ..hr.....cR..&.. 
 0250: C4 . 
```

## <a name="checkpoint-4"></a>검사점 4
마지막으로 대상 경로의 파일 속성이 확인 메시지와 함께 출력되어야 합니다. 이 파일 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 ST를 사용하여 Hadoop에서 인증되었고 보안 리소스에 대한 액세스 권한이 세션에 부여되었음을 확인합니다.

이 지점에 도달하면 (i) 세 행위자가 제대로 통신할 수 있고, (ii) core-site.xml과 jaas.conf가 적절하며, (iii) KDC가 자격 증명을 인식했음을 나타냅니다.

```cmd
 [2017-04-25 21:34:35,096] INFO 2235[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1586) - File properties for "/": FileStatus{path=hdfs://10.193.27.232:8020/; isDirectory=true; modification_time=1492028259862; access_time=0; owner=hdfs; group=hdfs; permission=rwxr-xr-x; isSymlink=false} 
 [2017-04-25 21:34:35,098] INFO 2237[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1587) - Successfully accessed the external file system. 
```

## <a name="common-errors"></a>일반 오류
도구가 실행되고 대상 경로의 파일 속성이 출력되지 *않은* 경우(검사점 4), 중간에 예외가 throw되었을 수 있습니다. 이 예외를 검토하고 검토 4단계 흐름에서 이 예외가 발생한 상황을 고려하세요. 발생할 수 있는 다음의 일반 오류를 순서대로 고려하세요.

| 예외 및 메시지 | 원인 | 
| --- | --- |
| org.apache.hadoop.security.AccessControlException<br>단순 인증을 사용할 수 없습니다. 사용 가능:[TOKEN, KERBEROS] | core-site.xml에서 hadoop.security.authentication 속성이 “KERBEROS”로 설정되어 있지 않습니다.|
|javax.security.auth.login.LoginException<br>Kerberos 데이터베이스에서 클라이언트를 찾을 수 없음  (6) - CLIENT_NOT_FOUND |    지정된 관리 서비스 사용자가 core-site.xml에 지정된 영역에 없습니다.|
| javax.security.auth.login.LoginException<br> 체크섬 실패 |관리 서비스 사용자가 있지만 암호가 잘못되었습니다. |
| 네이티브 구성 이름: C:\Windows\krb5.ini<br>기본 구성에서 로드됨 | 이 메시지는 Java의 krb5LoginModule이 머신에서 사용자 지정 클라이언트 구성을 검색했음을 나타냅니다. 문제를 일으킬 수 있는 사용자 지정 클라이언트 설정을 확인합니다. |
| javax.security.auth.login.LoginException<br>java.lang.IllegalArgumentException<br>잘못된 사용자 이름 admin_user@CONTOSO.COM: org.apache.hadoop.security.authentication.util.KerberosName$NoMatchingRule: admin_user@CONTOSO.COM에 적용된 규칙 없음 | Hadoop 클러스터당 적절한 규칙을 사용하여 “hadoop.security.auth_to_local” 속성을 core-site.xml에 추가합니다. |
| java.net.ConnectException<br>다음 URI의 외부 파일 시스템에 액세스하려는 중: hdfs://10.193.27.230:8020<br>IAAS16981207/10.107.0.245에서 10.193.27.230:8020 사이의 호출이 연결 예외로 실패 | KDC에 대한 인증에 성공했지만 Hadoop 이름 노드에 액세스하지 못했습니다. 이름 노드 IP 및 포트를 확인합니다. Hadoop에서 방화벽이 사용되지 않는지 확인합니다. |
| java.io.FileNotFoundException<br>파일이 없음: /test/data.csv |    인증에 성공했지만 지정한 위치가 없습니다. 경로를 확인하거나 먼저 루트 “/”를 사용하여 테스트합니다. |

## <a name="debugging-tips"></a>디버깅 팁

### <a name="mit-kdc"></a>MIT KDC  
관리자를 포함하여 KDC에 등록된 모든 SPN은 KDC 호스트나 구성된 KDC 클라이언트에서 **kadmin.local** > (관리자 로그인) > **listprincs** 를 실행하여 확인할 수 있습니다. Kerberos가 Hadoop 클러스터에서 제대로 구성되면 클러스터에서 사용 가능한 각 서비스(예: `nn`, `dn`, `rm`, `yarn`, `spnego` 등)에 SPN이 하나씩 있어야 합니다. 해당 keytab 파일(암호 대체)은 기본적으로 **/etc/security/keytabs** 에서 볼 수 있습니다. 이 파일은 KDC 프라이빗 키를 사용하여 암호화됩니다.  

[`kinit`](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)를 사용하여 KDC에서 로컬로 관리자 자격 증명을 확인하는 것도 좋습니다. 예제 사용량은 `kinit identity@MYREALM.COM`입니다. 암호를 묻는 메시지가 표시되면 ID가 있는 것입니다.  
KDC 로그는 기본적으로 **/var/log/krb5kdc.log** 에서 확인할 수 있으며, 이 로그에는 모든 티켓 요청과 요청한 클라이언트 IP가 포함되어 있습니다. 도구가 실행된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 머신 IP에서 보낸 요청이 두 개 있어야 합니다. 먼저 인증 서버에서 보낸 TGT 요청이 **AS\_REQ** 로 표시되고, 그다음에 허용 티켓 서버에서 보낸 ST 요청이 **TGS\_REQ** 로 표시됩니다.

```bash
 [root@MY-KDC log]# tail -2 /var/log/krb5kdc.log 
 May 09 09:48:26 MY-KDC.local krb5kdc[2547](info): **AS_REQ** (3 etypes {17 16 23}) 10.107.0.245: ISSUE: authtime 1494348506, etypes {rep=16 tkt=16 ses=16}, admin_user@CONTOSO.COM for **krbtgt/CONTOSO.COM@CONTOSO.COM** 
 May 09 09:48:29 MY-KDC.local krb5kdc[2547](info): **TGS_REQ** (3 etypes {17 16 23}) 10.107.0.245: ISSUE: authtime 1494348506, etypes {rep=16 tkt=16 ses=16}, admin_user@CONTOSO.COM for **nn/hadoop-hdp25-00.local@CONTOSO.COM** 
```

### <a name="active-directory"></a>Active Directory 
Active Directory에서는 [제어판] > [Active Directory 사용자 및 컴퓨터] > *MyRealm* > *MyOrganizationalUnit* 으로 이동하여 SPN을 확인할 수 있습니다. Kerberos가 Hadoop 클러스터에서 제대로 구성되면 각각의 서비스(예: `nn`, `dn`, `rm`, `yarn`, `spnego` 등)에 사용할 수 있는 SPN이 하나씩 있습니다.

### <a name="general-debugging-tips"></a>일반 디버깅 팁
SQL Server PolyBase 기능과 독립적으로 Java 환경을 통해 로그를 살펴보고 Kerberos 문제를 디버그하는 데 유용합니다.

Kerberos를 액세스하는 문제가 여전히 발생하는 경우 아래 단계를 수행하여 디버그하세요.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부에서 Kerberos HDFS 데이터에 액세스할 수 있는지 확인합니다. 다음 작업 중 하나를 수행할 수 있습니다. 

    - 고유한 Java 프로그램을 작성하거나
    - PolyBase 설치 폴더에서 `HdfsBridge` 클래스를 사용하세요. 예를 들면 다음과 같습니다.

      ```java
      -classpath ".\Hadoop\conf;.\Hadoop\*;.\Hadoop\HDP2_2\*" com.microsoft.polybase.client.HdfsBridge 10.193.27.232 8020 admin_user C:\temp\kerberos_pass.txt
      ```

     위의 예제에서 `admin_user`는 도메인 파트가 아닌 사용자 이름만 포함합니다.

2. PolyBase 외부에서 Kerberos HDFS 데이터에 액세스할 수 없는 경우:
    - Kerberos 인증에는 Active Directory Kerberos 인증 및 MIT Kerberos 인증이라는 두 가지 종류가 있습니다.
    - 사용자가 도메인 계정에 있고 HDFS에 액세스하는 동안 동일한 사용자 계정을 사용하는지 확인합니다.

3. Active Directory Kerberos의 경우 Windows에서 `klist` 명령을 사용하여 캐시된 티켓을 볼 수 있는지 확인합니다.
    - PolyBase 머신에 로그인하고 명령 프롬프트에서 `klist` 및 `klist tgt`를 실행하여 KDC, 사용자 이름 및 암호화 형식이 올바른지 확인합니다.

4. KDC에서 AES256을 지원할 수 있는 경우 [JCE 정책 파일](http://www.oracle.com/technetwork/java/javase/downloads/index.html)을 설치했는지 확인합니다.

## <a name="see-also"></a>참고 항목
[Integrating PolyBase with Cloudera using Active Directory Authentication](/archive/blogs/microsoftrservertigerteam/integrating-polybase-with-cloudera-using-active-directory-authentication)(Active Directory 인증을 사용하여 PolyBase와 Cloudera 통합)  
[Cloudera’s Guide to setting up Kerberos for CDH](https://www.cloudera.com/documentation/enterprise/5-6-x/topics/cm_sg_principal_keytab.html)(CDH의 Kerberos 설정에 대한 Cloudera 가이드)  
[Hortonworks’ Guide to Setting up Kerberos for HDP](https://docs.hortonworks.com/HDPDocuments/Ambari-2.2.0.0/bk_Ambari_Security_Guide/content/ch_configuring_amb_hdp_for_kerberos.html)(HDP의 Kerberos 설정에 대한 Hortonworks 가이드)  
[PolyBase 문제 해결](polybase-troubleshooting.md)