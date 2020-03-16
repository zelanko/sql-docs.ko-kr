---
title: Windows에 PolyBase 설치 | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
helpviewer_keywords:
- PolyBase, installation
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 007719c2407f6e193b8612ef51944ccbfd3238d3
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288477"
---
# <a name="install-polybase-on-windows"></a>Windows에 PolyBase 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 평가판을 설치하려면 [SQL Server 평가](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)로 이동합니다. 
   
## <a name="prerequisites"></a>사전 요구 사항  
   
- 64비트 SQL Server 평가 버전.  
   
- Microsoft .NET Framework 4.5  

- 최소 메모리: 4GB. 
   
- 최소 하드 디스크 공간: 2GB.
  
- 권장: 최소 16GB의 RAM.
   
- PolyBase가 제대로 작동하려면 TCP/IP를 사용하도록 설정해야 합니다. Developer 및 Express SQL Server 버전을 제외하고 모든 버전의 SQL Server에서 TCP/IP는 기본적으로 사용하도록 설정되어 있습니다. Developer 및 Express 버전에서 PolyBase가 제대로 작동하기 위해서는 TCP/IP 연결을 사용하도록 설정해야 합니다. [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)를 참조하세요.


>[!NOTE] 
> PolyBase는 컴퓨터당 하나의 SQL Server 인스턴스에만 설치할 수 있습니다.


>[!NOTE]
>PolyBase를 사용하려면 데이터베이스에 대한 sysadmin 또는 CONTROL SERVER 수준 사용 권한이 있어야 합니다.

>[!IMPORTANT]
>Hadoop에 대해 계산 푸시 다운 기능을 사용하려면 대상 Hadoop 클러스터에 HDFS, YARN 및 MapReduce의 핵심 구성 요소가 있어야 하며 작업 기록 서버가 활성화되어 있어야 합니다. PolyBase는 MapReduce를 통해 푸시다운 쿼리를 제출하고 작업 기록 서버에서 상태를 가져옵니다. 두 구성 요소가 없으면 쿼리가 실패합니다.
  
## <a name="single-node-or-polybase-scale-out-group"></a>단일 노드 또는 PolyBase 스케일 아웃 그룹

SQL Server 인스턴스에 PolyBase를 설치하기 전에 단일 노드 설치 또는 [PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md) 중 원하는 것을 결정합니다.

PolyBase 스케일 아웃 그룹의 경우 다음 사항을 확인합니다.

- 모든 머신이 같은 도메인에 있습니다.
- PolyBase를 설치하는 동안 동일한 서비스 계정 및 암호를 사용합니다.
- SQL Server 인스턴스가 네트워크를 통해 서로 통신할 수 있습니다.
- SQL Server 인스턴스는 모두 동일한 버전의 SQL Server입니다.

PolyBase를 독립 실행형 또는 스케일 아웃 그룹에 설치한 후에는 변경할 수 없습니다. 이 설정을 변경하려면 기능을 제거하고 다시 설치해야 합니다.

## <a name="use-the-installation-wizard"></a>설치 마법사 사용
   
1. SQL Server setup.exe를 실행합니다.   
   
2. **설치**를 선택한 다음, **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 선택합니다.  
   
3. 기능 선택 페이지에서 **외부 데이터용 PolyBase 쿼리 서비스**를 선택합니다.  

   ![PolyBase 서비스](../../relational-databases/polybase/media/install-wizard.png "PolyBase 서비스")  
   
   >[!NOTE]
   >SQL Server 2019 PolyBase에는 추가적인 **HDFS 데이터 원본용 Java 커넥터** 옵션이 포함되어 있습니다. 이 기능에 대한 자세한 내용은 [SQL Server 미리 보기 기능](https://cloudblogs.microsoft.com/sqlserver/2019/04/24/sql-server-2019-community-technology-preview-2-5-is-now-available/)을 참조하세요.
   
4. 서버 구성 페이지에서 **SQL Server PolyBase 엔진 서비스** 및 **SQL Server PolyBase 데이터 이동 서비스**를 구성하여 동일한 도메인 계정 하에서 실행합니다.  

   >[!IMPORTANT]
   >PolyBase 스케일 아웃 그룹에서 모든 노드의 PolyBase 엔진 및 PolyBase 데이터 이동 서비스는 동일한 도메인 계정으로 실행되어야 합니다. [PolyBase 스케일 아웃 그룹](#enable)을 참조하세요

5. PolyBase 구성 페이지에서 두 옵션 중 하나를 선택합니다. 자세한 내용은 [PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)을 참조하세요.  
   
   - SQL Server 인스턴스를 독립 실행형 PolyBase 사용 인스턴스로 사용합니다.  
   
     SQL Server 인스턴스를 독립 실행형 헤드 노드로 사용하려면 이 옵션을 선택합니다.  
   
   - SQL Server 인스턴스를 PolyBase 스케일 아웃 그룹의 일부로 사용합니다. 이 옵션은 들어오는 연결을 허용하도록 방화벽을 엽니다. SQL Server 데이터베이스 엔진, SQL Server PolyBase 엔진, SQL Server PolyBase 데이터 이동 서비스 및 SQL Browser에 연결할 수 있습니다. 또한 방화벽은 PolyBase 스케일 아웃 그룹의 다른 노드로부터 들어오는 연결을 허용합니다.  
   
     또한 이 옵션은 MSDTC(Microsoft Distributed Transaction Coordinator) 방화벽 연결을 사용하도록 설정하고 MSDTC 레지스트리 설정을 수정합니다.  
   
6. PolyBase 구성 페이지에서 6개 이상의 포트로 포트 범위를 지정합니다. SQL Server 설치 프로그램은 범위에서 처음 6개의 사용 가능한 포트를 할당합니다.  

   >[!IMPORTANT]
   > 설치 후 [PolyBase 기능을 사용하도록 설정](#enable)해야 합니다.


##  <a name="installing"></a> 명령 프롬프트 사용

이 테이블의 값을 사용하여 설치 스크립트를 만듭니다. SQL Server PolyBase 엔진 및 SQL Server PolyBase 데이터 이동 서비스는 동일한 계정 하에서 실행되어야 합니다. PolyBase 스케일 아웃 그룹에서 모든 노드의 양쪽 PolyBase 서비스는 동일한 도메인 계정 하에서 실행해야 합니다.  
   
<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017"

|SQL Server 구성 요소(SQL Server component)|매개 변수 및 값|Description|  
|--------------------------|--------------------------|-----------------|  
|SQL Server 설치 컨트롤|**필수**<br /><br /> /FEATURES=PolyBase|PolyBase 기능을 선택합니다.|  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCACCOUNT|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE**입니다.|  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCPASSWORD|엔진 서비스 계정의 암호를 지정합니다.|  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCSTARTUPTYPE|PolyBase 엔진의 시작 모드를 지정합니다. 자동(기본값), 비활성화 및 수동.|  
|SQL Server PolyBase 데이터 이동 |**선택 사항**<br /><br /> /PBDMSSVCACCOUNT|데이터 이동 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE**입니다.|  
|SQL Server PolyBase 데이터 이동 |**선택 사항**<br /><br /> /PBDMSSVCPASSWORD|데이터 이동 계정의 암호를 지정합니다.|  
|SQL Server PolyBase 데이터 이동 |**선택 사항**<br /><br /> /PBDMSSVCSTARTUPTYPE|데이터 이동 서비스의 시작 모드를 지정합니다. 자동(기본값), 비활성화 및 수동.|  
|PolyBase|**선택 사항**<br /><br /> /PBSCALEOUT|SQL Server 인스턴스가 PolyBase 스케일 아웃 계산 그룹의 일부로 사용되는지 여부를 지정합니다. <br />지원되는 값: True, False).|  
|PolyBase|**선택 사항**<br /><br /> /PBPORTRANGE|PolyBase 서비스에 대해 6개 이상의 포트가 있는 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

|SQL Server 구성 요소(SQL Server component)|매개 변수 및 값|Description|  
|--------------------------|--------------------------|-----------------|  
|SQL Server 설치 컨트롤|**필수**<br /><br /> /FEATURES=PolyBaseCore, PolyBaseJava, PolyBase | PolyBaseCore는 Hadoop 연결을 제외한 모든 PolyBase 기능에 대한 지원을 설치합니다. PolyBaseJava는 Hadoop 연결을 지원합니다. PolyBase는 두 기능을 모두 설치합니다. |  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCACCOUNT|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE**입니다.|  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCPASSWORD|엔진 서비스 계정의 암호를 지정합니다.|  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCSTARTUPTYPE|PolyBase 엔진의 시작 모드를 지정합니다. 자동(기본값), 비활성화 및 수동.|  
|SQL Server PolyBase 데이터 이동 |**선택 사항**<br /><br /> /PBDMSSVCACCOUNT|데이터 이동 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE**입니다.|  
|SQL Server PolyBase 데이터 이동 |**선택 사항**<br /><br /> /PBDMSSVCPASSWORD|데이터 이동 계정의 암호를 지정합니다.|  
|SQL Server PolyBase 데이터 이동 |**선택 사항**<br /><br /> /PBDMSSVCSTARTUPTYPE|데이터 이동 서비스의 시작 모드를 지정합니다. 자동(기본값), 비활성화 및 수동.|  
|PolyBase|**선택 사항**<br /><br /> /PBSCALEOUT|SQL Server 인스턴스가 PolyBase 스케일 아웃 계산 그룹의 일부로 사용되는지 여부를 지정합니다. <br />지원되는 값: True, False).|  
|PolyBase|**선택 사항**<br /><br /> /PBPORTRANGE|PolyBase 서비스에 대해 6개 이상의 포트가 있는 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end

설치 후 [PolyBase 기능을 사용하도록 설정](#enable)해야 합니다.



**예제**

이 예제는 설치 스크립트를 보여줍니다.  

```cmd
   
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,PolyBase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
   
```  

## <a id="enable"></a> PolyBase 사용

설치 후 PolyBase를 활성화하여 해당 기능에 액세스해야 합니다. 다음 Transact-SQL 명령을 사용합니다. 빅 데이터 클러스터 설치 중에 배포된 SQL 2019 인스턴스에는 이 설정이 기본적으로 사용하도록 지정되어 있습니다.


```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE;
```


## <a name="post-installation-notes"></a>설치 후 참고 사항  

PolyBase는 세 개의 사용자 데이터베이스, DWConfiguration, DWDiagnostics, 및 DWQueue를 설치합니다. 이러한 데이터베이스는 PolyBase용으로 사용됩니다. 변경하거나 삭제하지 마세요.  
   
### <a id="confirminstall"></a> 설치 확인 방법  

다음 명령을 실행합니다. PolyBase가 설치된 경우 1을 반환합니다. 그렇지 않으면 0을 반환합니다.  

```sql  
SELECT SERVERPROPERTY ('IsPolyBaseInstalled') AS IsPolyBaseInstalled;  
```  

### <a name="firewall-rules"></a>방화벽 규칙  

SQL Server PolyBase 설치는 머신에 다음과 같은 방화벽 규칙을 만듭니다.  
   
- SQL Server PolyBase – 데이터베이스 엔진 - \<SQLServerInstanceName>(TCP-In)  
   
- SQL Server PolyBase – PolyBase 서비스 - \<SQLServerInstanceName>(TCP-In)  

- SQL Server PolyBase - SQL Browser - (UDP-In)  
   
설치 시 SQL Server 인스턴스를 PolyBase 스케일 아웃 그룹의 일부로 사용하면 이러한 규칙이 설정됩니다. 들어오는 연결을 허용하도록 방화벽이 열립니다. SQL Server 데이터베이스 엔진, SQL Server PolyBase 엔진, SQL Server PolyBase 데이터 이동 서비스 및 SQL Browser에 사용할 수 있습니다. 설치 중에 머신의 방화벽 서비스가 실행되고 있지 않으면 SQL Server 설치에서 이러한 규칙을 사용할 수 없습니다. 이 경우 머신에서 방화벽 서비스를 시작하고 설치 후에 이러한 규칙을 활성화합니다.  
   
#### <a name="to-enable-the-firewall-rules"></a>방화벽 규칙을 사용하려면  

1. **제어판**을 엽니다.  

2. **시스템 및 보안**을 선택하고 **Windows 방화벽**을 선택합니다.  
   
3. **고급 설정**을 선택하고 **인바운드 규칙**을 선택합니다.  
   
4. 비활성화된 규칙을 마우스 오른쪽 단추로 클릭한 다음, **규칙 활성화**를 선택합니다.  
   
### <a name="polybase-service-accounts"></a>PolyBase 서비스 계정

PolyBase 엔진 및 PolyBase 데이터 이동 서비스에 대한 서비스 계정을 변경하려면 PolyBase 기능을 제거하고 다시 설치합니다.

## <a name="next-steps"></a>다음 단계  

[PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md)을 참조하세요.
