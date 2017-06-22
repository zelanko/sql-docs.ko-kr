---
title: "PolyBase 설치 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase, installation
ms.assetid: 3a1e64be-9bfc-4408-accd-35990e1a6b52
caps.latest.revision: 25
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f5b029907f25811131e08d2f7ade1f050e3a18d5
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="polybase-installation"></a>PolyBase 설치
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server 평가판을 설치하려면 [SQL Server 평가](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)로 이동합니다. 
  
## <a name="prerequisites"></a>필수 구성 요소  
  
-   64 비트 SQL Server 평가 버전  
  
-   Microsoft .NET Framework 4.5  
  
-   Oracle Java SE RunTime Environment(JRE) 버전 7.51 이상(64비트)( [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) 또는 [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) 작동). [Java SE 다운로드](http://www.oracle.com/technetwork/java/javase/downloads/index.html)로 이동합니다. JRE가 없으면 설치 관리자가 실패합니다.  
  
-   최소 메모리: 4GB  
  
-   최소 하드 디스크 공간: 2GB  
  
-   TCP/IP 연결을 사용할 수 있어야 합니다. [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)를 참조하세요.  
  
 **참고**  
  
 PolyBase는 컴퓨터당 하나의 SQL Server 인스턴스에만 설치할 수 있습니다.  
  
## <a name="single-node-or-polybase-scaleout-group"></a>단일 노드 또는 PolyBase 확장 그룹
SQL Server 인스턴스에서 PolyBase 설치를 시작하기 전에 단일 노드 설치나 PolyBase 확장 그룹을 원할 경우 계획을 세우는 것이 좋습니다. PolyBase 확장 그룹의 경우 다음 사항을 확인해야 합니다. 
- 모든 컴퓨터가 같은 도메인에 있습니다.
- 설치하는 동안 동일한 서비스 계정 및 암호를 사용합니다.
- SQL Server 인스턴스가 네트워크를 통해 서로 통신할 수 있습니다.

PolyBase를 독립 실행형으로 또는 확장 그룹에 설치한 후에는 변경할 수 없습니다. 이 설정을 변경하려면 기능을 제거 후 다시 설치해야 합니다.

## <a name="install-using-the-installation-wizard"></a>설치 마법사를 사용하여 설치  
  
1.  **SQL Server 설치 센터**를 실행합니다. SQL Server 설치 미디어를 넣고 **Setup.exe**를 두 번 클릭합니다.  
  
2.  **설치**를 클릭한 후 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
3.  기능 선택 페이지에서 **외부 데이터용 PolyBase 쿼리 서비스**를 선택합니다.  
  
4.  서버 구성 페이지에서 **SQL Server PolyBase 엔진 서비스** 및 SQL Server PolyBase 데이터 이동 서비스를 구성하여 동일한 계정 하에서 실행합니다.  
  
    > **중요!!** PolyBase 규모 확장 그룹에서 모든 노드의 PolyBase 엔진 및 PolyBase 데이터 이동 서비스를 동일한 도메인 계정 하에서 실행해야 합니다.  
    > PolyBase 규모 확장 참조  
  
5.  **PolyBase 구성 페이지**에서 다음 옵션 중 하나를 선택합니다. 자세한 내용은 [PolyBase 확장 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md) 을 참조하세요.  
  
    -   SQL Server 인스턴스를 독립 실행형 PolyBase 사용 인스턴스로 사용합니다.  
  
         이 SQL Server 인스턴스를 독립 실행형 헤드 노드로 사용하려면 이 옵션을 선택합니다.  
  
    -   SQL Server 인스턴스를 PolyBase 규모 확장 그룹의 일부로 사용합니다.  SQL Server 데이터베이스 엔진, SQL Server PolyBase 엔진, SQL Server PolyBase 데이터 이동 서비스, SQL Browser에 대한 들어오는 연결을 허용하도록 방화벽이 열립니다. 방화벽은 PolyBase 규모 확장 그룹의 다른 노드에서 들어오는 연결을 허용하도록 열립니다.  
  
         이 옵션을 선택하면 MSDTC(Microsoft Distributed Transaction Coordinator) 방화벽 연결을 사용하게 되고 MSDTC 레지스트리 설정이 수정됩니다.  
  
6.  **PolyBase 구성 페이지**에서 6개 이상의 포트로 포트 범위를 지정합니다. SQL Server 설치 프로그램이 해당 범위의 앞쪽에서 사용할 수 있는 6개의 포트를 할당합니다.  
  
##  <a name="installing"></a> 명령 프롬프트를 사용하여 설치  
 이 테이블의 값을 사용하여 설치 스크립트를 만듭니다. 두 개의 서비스, 즉 **SQL Server PolyBase 엔진** 및 **SQL Server PolyBase 데이터 이동 서비스** 를 동일한 계정 하에서 실행해야 합니다. PolyBase 규모 확장 그룹에서 모든 노드의 양쪽 PolyBase 서비스는 동일한 도메인 계정 하에서 실행해야 합니다.  
  
|SQL Server 구성 요소(SQL Server component)|매개 변수 및 값|설명|  
|--------------------------|--------------------------|-----------------|  
|SQL Server 설치 컨트롤|**필수**<br /><br /> /FEATURES=PolyBase|PolyBase 기능을 선택합니다.|  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCACCOUNT|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE**입니다.|  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCPASSWORD|엔진 서비스 계정의 암호를 지정합니다.|  
|SQL Server PolyBase 엔진|**선택 사항**<br /><br /> /PBENGSVCSTARTUPTYPE|자동(기본) , 사용 안 함, 수동 중에서 PolyBase 엔진 서비스의 시작 모드를 지정합니다.|  
|SQL Server PolyBase 데이터 이동 서비스|**선택 사항**<br /><br /> /PBDMSSVCACCOUNT|데이터 이동 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE**입니다.|  
|SQL Server PolyBase 데이터 이동 서비스|**선택 사항**<br /><br /> /PBDMSSVCPASSWORD|데이터 이동 계정의 암호를 지정합니다.|  
|SQL Server PolyBase 데이터 이동 서비스|**선택 사항**<br /><br /> /PBDMSSVCSTARTUPTYPE|자동(기본) , 사용 안 함, 수동 중에서 데이터 이동 서비스의 시작 모드를 지정합니다.|  
|PolyBase|**선택 사항**<br /><br /> /PBSCALEOUT|SQL Server 인스턴스가 PolyBase 규모 확장 계산 그룹의 일부로 사용될지를 지정합니다. <br />지원되는 값: **True**, **False**|  
|PolyBase|**선택 사항**<br /><br /> /PBPORTRANGE|PolyBase 서비스용 6개 이상의 포트로 포트 범위를 지정합니다. 예:<br /><br /> `/PBPORTRANGE=16450-16460`|  
  
 **예제**  
  
 설치 스크립트 예제를 보여줍니다.  
  
```  
  
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,Polybase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
  
```  
  
## <a name="post-installation-notes"></a>설치 후 참고 사항  
 PolyBase는 세 개의 사용자 데이터베이스, DWConfiguration, DWDiagnostics, 및 DWQueue를 설치합니다.   이러한 사용자 데이터베이스는 PolyBase에서 사용되며 변경하거나 삭제해서는 안 됩니다.  
  
### <a name="how-to-confirm-installation"></a>설치 확인 방법  
 다음 명령을 실행합니다. PolyBase가 설치된 경우 1을 반환 합니다. 그렇지 않으면 0이 반환됩니다.  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
### <a name="firewall-rules"></a>방화벽 규칙  
 SQL Server PolyBase 설치는 컴퓨터에 다음과 같은 방화벽 규칙을 만듭니다.  
  
-   SQL Server PolyBase – 데이터베이스 엔진 - \<SQLServerInstanceName>(TCP-In)  
  
-   SQL Server PolyBase – PolyBase 서비스 - \<SQLServerInstanceName>(TCP-In)  
  
-   SQL Server PolyBase - SQL Browser - (UDP-In)  
  
 설치 시, SQL Server 서버를 PolyBase 규모 확장 그룹의 일부로 사용하도록 선택하면, 이 규칙이 활성화되며 SQL Server 데이터베이스 엔진, SQL Server PolyBase 엔진, SQL Server PolyBase 데이터 이동 서비스 및 SQL Browser에 대해 들어오는 연결을 허용하도록 방화벽이 열립니다. 하지만 설치하는 동안 컴퓨터에 방화벽 서비스가 실행되고 있지 않으면 SQL Server 설치가 이 규칙을 활성화하지 못합니다. 이런 경우 설치 후에 컴퓨터에서 방화벽 서비스를 시작하고 규칙을 활성화해야 합니다.  
  
#### <a name="to-enable-the-firewall-rules"></a>방화벽 규칙을 사용하려면  
  
-   **제어판**을 엽니다.  
  
-   **시스템 및 보안**을 클릭하고 **Windows 방화벽**을 클릭합니다.  
  
-   **고급 설정**, **인바운드 규칙**을 차례로 클릭합니다.  
  
-   비활성화된 규칙을 마우스 오른쪽 단추로 클릭한 후 **규칙 사용**을 클릭합니다.  
  
### <a name="polybase-service-accounts"></a>PolyBase 서비스 계정
PolyBase 엔진 및 PolyBase 데이터 이동 서비스에 대한 서비스 계정을 변경하려면 PolyBase 기능을 제거하고 다시 설치합니다.
   
## <a name="next-steps"></a>다음 단계  
 [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md)을 참조하세요.  
  
  

