---
title: "PolyBase Kerberos 연결 문제 해결 | Microsoft Docs"
description: 
services: 
documentationcenter: 
author: alazad-msft
manager: 
editor: 
tags: 
ms.assetid: 
ms.service: 
ms.component: polybase
ms.suite: sql
ms.custom: 
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 07/19/2017"
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.author: alazad
ms.openlocfilehash: cbbc687cf4c3a5edf769ab973879bc81f8db8406
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="troubleshoot-polybase-kerberos-connectivity"></a>PolyBase Kerberos 연결 문제 해결
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
PolyBase에 기본 제공된 대화형 진단 도구를 사용하면 Kerberos 보안 Hadoop 클러스터에 대해 PolyBase를 사용할 때 인증 문제를 해결할 수 있습니다. 

이 문서는 이 도구를 활용하여 이러한 문제의 디버깅 프로세스를 살펴보기 위한 가이드입니다.

## <a name="prerequisites"></a>사전 요구 사항

1. PolyBase가 설치된 SQL Server 2016 RTM CU6/SQL Server 2016 SP1 CU3/SQL Server 2017 이상
1. Kerberos(Active Directory 또는 MIT)로 보호된 Hadoop 클러스터(Cloudera 또는 Hortonworks)

## <a name="introduction"></a>소개
먼저 Kerberos 프로토콜을 개략적으로 이해할 수 있도록 도와드립니다. 관련된 행위자는 다음 세 가지입니다.
1. Kerberos 클라이언트(SQL Server)
1. 보안 리소스(HDFS, MR2, YARN, 작업 기록 등)
1. 키 배포 센터(Active Directory에서는 도메인 컨트롤러라고 함)

Hadoop 보안 리소스의 각 리소스는 Hadoop 클러스터의 Kerberization 프로세스의 일환으로 고유한 **SPN(서비스 사용자 이름)**을 사용하여 **KDC(키 배포 센터)**에 등록됩니다. 목표는 클라이언트가 임시 사용자 티켓인 **TGT(허용 티켓)**를 얻어, 액세스하려는 특정 SPN에 대해 또 다른 임시 티켓인 **ST(서비스 티켓)**를 KDC에서 요청하는 것입니다.  
PolyBase에서 Kerberos 보안 리소스에 대해 인증이 요청되면 다음과 같은 4번 왕복 핸드셰이크가 수행됩니다.
1. SQL Server가 KDC에 연결하고 사용자의 TGT를 가져옵니다. TGT는 KDC의 개인 키를 사용하여 암호화됩니다.
1. SQL Server가 Hadoop 보안 리소스(예: HDFS)를 호출하고 ST가 필요한 SPN을 결정합니다.
1. SQL Server가 KDC로 돌아가고, TGT를 다시 전달하고, ST를 요청하여 해당하는 특정 보안 리소스에 액세스합니다. ST는 보안 서비스의 개인 키를 사용하여 암호화됩니다.
1. SQL Server가 ST를 Hadoop에 전달하고 인증되어 해당 서비스에 대해 세션이 만들어집니다.

![](./media/polybase-sqlserver.png)

인증 관련 문제는 위 4단계 중 하나 이상에 속합니다. 더 빠르게 디버그할 수 있도록 PolyBase에서는 실패 지점을 식별하는 데 도움이 되는 통합 진단 도구를 도입했습니다.

## <a name="troubleshooting"></a>문제 해결
PolyBase에는 Hadoop 클러스터의 속성이 포함된 여러 구성 XML이 있습니다. 즉, 다음과 같은 파일입니다.
- core-site.xml
- hdfs-site.xml
- hive-site.xml
- jaas.conf
- mapred-site.xml
- yarn-site.xml

이러한 파일은 다음 위치에 있습니다.

\\[시스템 드라이브\\]:{설치 경로}\\{인스턴스}\\{이름}\\MSSQL\\Binn\\Polybase\\Hadoop\\conf

예를 들어 SQL Server 2016의 기본값은 “C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\MSSQL\\Binn\\Polybase\\Hadoop\\conf”입니다.

PolyBase 구성 파일 중 하나인 **core-site.xml**에서 아래 세 속성의 값을 환경에 따라 값을 설정하여 업데이트합니다.
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
나중에 푸시다운 작업이 필요한 경우 다른 XML도 업데이트해야 하지만 이 파일만 구성해도 HDFS 파일 시스템에 액세스할 수는 있습니다.

이 도구는 SQL Server와 독립적으로 실행되므로 SQL Server가 실행되고 있지 않아도 되고 구성 XML을 업데이트하더라도 SQL Server를 다시 시작하지 않아도 됩니다. 이 도구를 실행하려면 SQL Server가 설치된 호스트에서 다음 명령을 실행합니다.

```
> cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase  
> java -classpath ".\Hadoop\conf;.\Hadoop\*;.\Hadoop\HDP2_2\*" com.microsoft.polybase.client.HdfsBridge {Name Node Address} {Name Node Port} {Service Principal} {Filepath containing Service Principal's Password} {Remote HDFS file path (optional)}
```

## <a name="arguments"></a>인수
| 인수 | Description|
| --- | --- |
| Name Node Address | 이름 노드의 IP 또는 FQDN입니다. 이 인수는 CREATE EXTERNAL DATA SOURCE T-SQL의 “LOCATION” 인수를 참조합니다.|
| Name Node Port | 이름 노드의 포트입니다. 이 인수는 CREATE EXTERNAL DATA SOURCE T-SQL의 “LOCATION” 인수를 참조합니다. 일반적으로 8020입니다. |
| Service Principal | KDC의 관리 서비스 사용자입니다. CREATE DATABASE SCOPED CREDENTIAL T-SQL에서 “IDENTITY” 인수로 사용하는 내용과 일치해야 합니다.|
| Service Password | 암호를 콘솔에 입력하는 대신 파일에 저장하고 여기에 파일 경로를 전달합니다. 파일의 내용이 CREATE DATABASE SCOPED CREDENTIAL T-SQL에서 “SECRET” 인수로 사용하는 내용과 일치해야 합니다. |
| *원격 HDFS 파일 경로(선택 사항) * | 액세스할 기존 파일의 경로입니다. 지정하지 않으면 루트 “/”가 사용됩니다. |

## <a name="example"></a>예제
```dos
java -classpath ".\Hadoop\conf;.\Hadoop\*;.\Hadoop\HDP2_2\*" com.microsoft.polybase.client.HdfsBridge 10.193.27.232 8020 admin_user C:\temp\kerberos_pass.txt
```
출력에는 향상된 디버깅을 위해 자세한 정보가 포함되어 있지만, MIT 또는 AD 중 무엇을 사용하든 네 개의 기본 검사점만 살펴보면 됩니다. 이들 검사점은 위에서 설명한 4개 단계에 해당합니다. 

다음은 MIT KDC 출력의 일부입니다. MIT 및 AD의 전체 샘플 출력은 이 문서 끝에 있는 참조에서 확인할 수 있습니다.

## <a name="checkpoint-1"></a>검사점 1
서버 보안 주체가 krbtgt/*MYREALM.COM@MYREALM.COM*인 티켓의 16진수 덤프가 있어야 합니다. 이는 KDC에 인증되고 TGT를 받은 SQL Server를 나타냅니다. 이 덤프가 없으면 Hadoop이 아니라 SQL Server와 KDC 사이에서만 문제를 찾을 수 있습니다.

PolyBase는 AD와 MIT 간의 트러스트 관계를 지원하지 **않으며** Hadoop 클러스터에 구성된 동일한 KDC에 대해 구성해야 합니다. 이러한 환경에서는 해당 KDC에 서비스 계정을 수동으로 만들고 해당 계정을 사용하여 인증을 수행하면 됩니다.
```dos
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
 *[…Condensed…]* 
 0140: 67 6D F6 41 6C EB E0 C3 3A B2 BD B1 gm.Al...:... 
 Client Principal = admin_user@CONTOSO.COM 
 Server Principal = krbtgt/CONTOSO.COM@CONTOSO.COM 
 *[…Condensed…]* 
 [2017-04-25 21:34:34,500] INFO 1639[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1579) - Successfully authenticated against KDC server. 
```
## <a name="checkpoint-2"></a>검사점 2
PolyBase가 HDFS에 액세스하려고 시도하며 요청에 필요한 서비스 티켓이 포함되어 있지 않으므로 액세스에 실패합니다.
```dos
 [2017-04-25 21:34:34,501] INFO 1640[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1584) - Attempting to access external filesystem at URI: hdfs://10.193.27.232:8020 
 Found ticket for admin_user@CONTOSO.COM to go to krbtgt/CONTOSO.COM@CONTOSO.COM expiring on Wed Apr 26 21:34:33 UTC 2017 
 Entered Krb5Context.initSecContext with state=STATE_NEW 
 Found ticket for admin_user@CONTOSO.COM to go to krbtgt/CONTOSO.COM@CONTOSO.COM expiring on Wed Apr 26 21:34:33 UTC 2017 
 Service ticket not found in the subject 
```
## <a name="checkpoint-3"></a>검사점 3
두 번째 16진수 덤프는 SQL Server가 TGT를 사용하여 KDC에서 이름 노드 SPN에 적용되는 서비스 티켓을 가져왔음을 나타냅니다.
```dos
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
 *[…Condensed…]* 
 0240: 03 E3 68 72 C4 D2 8D C2 8A 63 52 1F AE 26 B6 88 ..hr.....cR..&.. 
 0250: C4 . 
```
## <a name="checkpoint-4"></a>검사점 4
마지막으로 대상 경로의 파일 속성이 확인 메시지와 함께 출력되어야 합니다. 이는 SQL Server가 ST를 사용하여 Hadoop에서 인증되었고 보안 리소스에 대한 액세스 권한이 세션에 부여되었음을 나타냅니다.

이 지점에 도달하면 (i) 세 행위자가 제대로 통신할 수 있고, (ii) core-site.xml과 jaas.conf가 적절하며, (iii) KDC가 자격 증명을 인식했음을 나타냅니다.
```dos
 [2017-04-25 21:34:35,096] INFO 2235[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1586) - File properties for "/": FileStatus{path=hdfs://10.193.27.232:8020/; isDirectory=true; modification_time=1492028259862; access_time=0; owner=hdfs; group=hdfs; permission=rwxr-xr-x; isSymlink=false} 
 [2017-04-25 21:34:35,098] INFO 2237[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1587) - Successfully accessed the external file system. 
```
## <a name="common-errors"></a>일반 오류
도구가 실행되고 대상 경로의 파일 속성이 출력되지 *않은* 경우(검사점 4), 중간에 예외가 throw되었을 수 있습니다. 이 예외를 검토하고 검토 4단계 흐름에서 이 예외가 발생한 상황을 고려하세요. 발생할 수 있는 다음의 일반 오류를 순서대로 고려하세요.
| 예외 및 메시지 | 원인 | 
| --- | --- |
| org.apache.hadoop.security.AccessControlException<br>단순 인증을 사용할 수 없습니다. 사용 가능:[TOKEN, KERBEROS] | core-site.xml에서 hadoop.security.authentication 속성이 “KERBEROS”로 설정되어 있지 않습니다.|
|javax.security.auth.login.LoginException<br>Kerberos 데이터베이스에서 클라이언트를 찾을 수 없음  (6) - CLIENT_NOT_FOUND |    지정된 관리 서비스 사용자가 core-site.xml에 지정된 영역에 없습니다.|
| javax.security.auth.login.LoginException<br> 체크섬 실패 |    관리 서비스 사용자가 있지만 암호가 잘못되었습니다. |
| 기본 구성 이름: C:\Windows\krb5.ini<br>기본 구성에서 로드됨 | 예외는 아니지만 Java의 krb5LoginModule이 컴퓨터에서 사용자 지정 클라이언트 구성을 검색했음을 나타냅니다. 문제를 일으킬 수 있는 사용자 지정 클라이언트 설정을 확인합니다. |
| javax.security.auth.login.LoginException<br>java.lang.IllegalArgumentException<br>잘못된 사용자 이름 admin_user@CONTOSO.COM: org.apache.hadoop.security.authentication.util.KerberosName$NoMatchingRule: admin_user@CONTOSO.COM에 적용된 규칙 없음 | Hadoop 클러스터별로 적절한 규칙이 포함된 “hadoop.security.auth_to_local” 속성을 core-site.xml에 추가합니다. |
| java.net.ConnectException<br>다음 URI의 외부 파일 시스템에 액세스하려는 중: hdfs://10.193.27.230:8020<br>IAAS16981207/10.107.0.245에서 10.193.27.230:8020 사이의 호출이 연결 예외로 실패 | KDC에 대한 인증에 성공했지만 Hadoop 이름 노드에 액세스하지 못했습니다. 이름 노드 IP 및 포트를 확인합니다. Hadoop에서 방화벽이 사용되지 않는지 확인합니다. |
| java.io.FileNotFoundException<br>파일이 없음: /test/data.csv |    인증에 성공했지만 지정한 위치가 없습니다. 경로를 확인하거나 먼저 루트 “/”를 사용하여 테스트합니다. |
## <a name="debugging-tips"></a>디버깅 팁
### <a name="mit-kdc"></a>MIT KDC  
관리자를 포함하여 KDC에 등록된 모든 SPN은 KDC 호스트나 구성된 KDC 클라이언트에서 **kadmin.local** > (관리자 로그인) > **listprincs**를 실행하여 확인할 수 있습니다. Hadoop 클러스터가 제대로 Kerberize되었다면 클러스터에서 사용 가능한 각 서비스(예: nn, dn, rm, yarn, spnego 등)에 SPN이 하나씩 있어야 합니다. 해당 keytab 파일(암호 대체)은 기본적으로 **/etc/security/keytabs**에서 볼 수 있습니다. 이 파일은 KDC의 개인 키를 사용하여 암호화됩니다.  

[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html) 도구를 사용하여 KDC에서 로컬로 관리자 자격 증명을 확인하는 것도 좋습니다. 사용 예: *kinit identity@MYREALM.COM*. 암호를 묻는 메시지가 표시되면 ID가 있는 것입니다.  
KDC 로그는 기본적으로 **/var/log/krb5kdc.log**에서 확인할 수 있으며, 이 로그에는 모든 티켓 요청과 요청한 클라이언트 IP가 포함되어 있습니다. 도구가 실행된 SQL Server 컴퓨터 IP에서 보낸 요청이 두 개 있어야 합니다. 먼저 인증 서버에서 보낸 TGT 요청이 **AS\_REQ**로 표시되고, 그다음에 허용 티켓 서버에서 보낸 ST 요청이 **TGS\_REQ**로 표시됩니다.
```bash
 [root@MY-KDC log]# tail -2 /var/log/krb5kdc.log 
 May 09 09:48:26 MY-KDC.local krb5kdc[2547](info): **AS_REQ** (3 etypes {17 16 23}) 10.107.0.245: ISSUE: authtime 1494348506, etypes {rep=16 tkt=16 ses=16}, admin_user@CONTOSO.COM for **krbtgt/CONTOSO.COM@CONTOSO.COM** 
 May 09 09:48:29 MY-KDC.local krb5kdc[2547](info): **TGS_REQ** (3 etypes {17 16 23}) 10.107.0.245: ISSUE: authtime 1494348506, etypes {rep=16 tkt=16 ses=16}, admin_user@CONTOSO.COM for **nn/hadoop-hdp25-00.local@CONTOSO.COM** 
```
### <a name="active-directory"></a>Active Directory 
Active Directory에서는 [제어판] > [Active Directory 사용자 및 컴퓨터] > *MyRealm* > *MyOrganizationalUnit*으로 이동하여 SPN을 확인할 수 있습니다. Hadoop 클러스터가 제대로 Kerberize되었다면 사용 가능한 각 서비스(예: nn, dn, rm, yarn, spnego 등)에 SPN이 하나씩 있어야 합니다.

## <a name="see-also"></a>관련 항목:
[Integrating PolyBase with Cloudera using Active Directory Authentication](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/10/17/integrating-polybase-with-cloudera-using-active-directory-authentication)(Active Directory 인증을 사용하여 PolyBase와 Cloudera 통합)  
[Cloudera’s Guide to setting up Kerberos for CDH](https://www.cloudera.com/documentation/enterprise/5-6-x/topics/cm_sg_principal_keytab.html)(CDH의 Kerberos 설정에 대한 Cloudera 가이드)  
[Hortonworks’ Guide to Setting up Kerberos for HDP](https://docs.hortonworks.com/HDPDocuments/Ambari-2.2.0.0/bk_Ambari_Security_Guide/content/ch_configuring_amb_hdp_for_kerberos.html)(HDP의 Kerberos 설정에 대한 Hortonworks 가이드)  
[PolyBase 문제 해결](polybase-troubleshooting.md)


