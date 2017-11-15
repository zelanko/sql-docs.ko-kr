---
title: "서버 네트워크 주소 지정(데이터베이스 미러링) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- database mirroring [SQL Server], endpoint
- endpoints [SQL Server], database mirroring
- server network addresses [SQL Server]
ms.assetid: a64d4b6b-9016-4f1e-a310-b1df181dd0c6
caps.latest.revision: "60"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 933d557bed780358dd9ac24edc244a734a03e7bb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="specify-a-server-network-address-database-mirroring"></a>서버 네트워크 주소 지정(데이터베이스 미러링)
  데이터베이스 미러링 세션을 설정하려면 각 서버 인스턴스에 대한 서버 네트워크 주소가 필요합니다. 서버 인스턴스의 서버 네트워크 주소는 시스템 주소와 인스턴스가 수신하는 포트 번호를 제공하여 인스턴스를 명확하게 식별해야 합니다.  
  
 서버 인스턴스에 데이터베이스 미러링 끝점이 있어야만 서버 네트워크 주소에 포트를 지정할 수 있습니다. 자세한 내용은 [Windows 인증에 대한 데이터베이스 미러링 끝점 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)를 참조하세요.  
  
  
##  <a name="Syntax"></a> 서버 네트워크 주소 구문  
 서버 네트워크 주소 구문은 다음 형식을 사용합니다.  
  
 TCP**://***\<system-address>***:***\<port>*  
  
 여기서  
  
-   *\<system-address>*는 대상 컴퓨터 시스템을 명확하게 식별하는 문자열입니다. 일반적으로 서버 주소는 시스템 이름(시스템이 같은 도메인에 있는 경우), 정규화된 도메인 이름 또는 IP 주소입니다.  
  
    -   시스템이 같은 도메인에 있는 경우 `SYSTEM46`과 같이 컴퓨터 시스템의 이름을 사용할 수 있습니다.  
  
    -   IP 주소를 사용하려면 환경에서 고유한 주소여야 합니다. 정적인 경우에만 IP 주소를 사용하는 것이 좋습니다. IP 주소는 IP 버전 4(IPv4) 또는 IP 버전 6(IPv6)일 수 있습니다. IPv6 주소는 대괄호로 묶어야 합니다(예: **[***<IPv6_address>***]**).  
  
         시스템의 IP 주소를 확인하려면 Windows 명령 프롬프트에서 **ipconfig** 명령을 입력합니다.  
  
    -   정규화된 도메인 이름을 사용하는 것이 좋습니다. 이 주소 문자열은 로컬로 정의되므로 위치에 따라 형식이 달라집니다. 항상은 아니지만 정규화된 도메인 이름은 컴퓨터 이름과 마침표로 구분된 일련의 도메인 세그먼트를 다음 형식으로 포함하는 복합 이름입니다.  
  
         *computer_name* **)을 사용할 수 있습니다.** *domain_segment*[...**.***domain_segment*]  
  
         여기에서 *computer_name*은 서버 인스턴스를 실행하는 컴퓨터의 네트워크 이름이고 *domain_segment*[...**.***domain_segment*]는 서버의 나머지 도메인 정보입니다(예: `localinfo.corp.Adventure-Works.com`).  
  
         도메인 세그먼트의 내용과 개수는 회사 또는 조직 내에서 결정됩니다. 서버의 정규화된 도메인 이름을 모르는 경우 시스템 관리자에게 문의하세요.  
  
        > [!NOTE]  
        >  정규화된 도메인 이름을 찾는 방법은 이 항목의 뒷부분에 나오는 "정규화된 도메인 이름 찾기"를 참조하세요.  
  
-   *\<포트>*는 파트너 서버 인스턴스의 미러링 끝점에서 사용하는 포트 번호입니다. 끝점 지정에 대한 자세한 내용은 [Windows 인증에 대한 데이터베이스 미러링 끝점 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)를 참조하세요.  
  
     데이터베이스 미러링 끝점은 컴퓨터 시스템에서 사용 가능한 모든 포트를 사용할 수 있습니다. 컴퓨터 시스템의 각 포트 번호는 하나의 끝점에만 연결되어야 하고 각 끝점은 단일 서버 인스턴스와 연결되므로 같은 서버의 서로 다른 서버 인스턴스는 서로 다른 포트의 각 끝점에서 수신합니다. 따라서 데이터베이스 미러링 세션을 설정할 때 서버 네트워크 주소에 지정하는 포트는 항상 끝점이 해당 포트와 연결된 서버 인스턴스로 세션을 지정합니다.  
  
     서버 인스턴스의 서버 네트워크 주소에서 미러링 끝점과 연결된 포트 번호만이 해당 인스턴스를 컴퓨터의 다른 인스턴스와 구분해 줍니다. 다음 그림에서는 단일 컴퓨터에 있는 두 서버 인스턴스의 서버 네트워크 주소를 보여 줍니다. 기본 인스턴스는 포트 `7022` 를 사용하고 명명된 인스턴스는 포트 `7033`을 사용합니다. 이러한 두 서버 인스턴스에 대한 서버 네트워크 주소는 `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` 및 `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`입니다. 주소에는 서버 인스턴스 이름이 포함되지 않습니다.  
  
     ![기본 인스턴스의 서버 네트워크 주소](../../database-engine/availability-groups/windows/media/dbm-2-instances-ports-1-system.gif "기본 인스턴스의 서버 네트워크 주소")  
  
     서버 인스턴스의 데이터베이스 미러링 끝점과 현재 연결된 포트를 식별하려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT type_desc, port FROM sys.tcp_endpoints  
    ```  
  
     **type_desc** 값이 "DATABASE_MIRRORING"인 행을 찾아 해당 포트 번호를 사용합니다.  
  
### <a name="examples"></a>예  
  
#### <a name="a-using-a-system-name"></a>1. 시스템 이름 사용  
 다음 서버 네트워크 주소는 시스템 이름 `SYSTEM46`및 포트 `7022`를 지정합니다.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://SYSTEM46:7022';  
```  
  
#### <a name="b-using-a-fully-qualified-domain-name"></a>2. 정규화된 도메인 이름 사용  
 다음 서버 네트워크 주소는 정규화된 도메인 이름 `DBSERVER8.manufacturing.Adventure-Works.com`및 포트 `7024`를 지정합니다.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://DBSERVER8.manufacturing.Adventure-Works.com:7024';  
```  
  
#### <a name="c-using-ipv4"></a>3. IPv4 사용  
 다음 서버 네트워크 주소는 IPv4 주소 `10.193.9.134`및 포트 `7023`을 지정합니다.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://10.193.9.134:7023';  
```  
  
#### <a name="d-using-ipv6"></a>4. IPv6 사용  
 다음 서버 네트워크 주소에는 IPv6 주소 `2001:4898:23:1002:20f:1fff:feff:b3a3`및 포트 `7022`가 포함되어 있습니다.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022';  
```  
  
## <a name="finding-the-fully-qualified-domain-name"></a>정규화된 도메인 이름 찾기  
 시스템의 정규화된 도메인 이름을 찾으려면 해당 시스템의 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
 **IPCONFIG /ALL**  
  
 정규화된 도메인 이름을 구성하려면 *<host_name>* 및 *<Primary_Dns_Suffix>*의 값을 다음과 같이 연결해야 합니다.  
  
 *<host_name>* **.** *<Primary_Dns_Suffix>*  
  
 예를 들어 다음 IP 구성은  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 다음 정규화된 도메인 이름과 같습니다.  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
##  <a name="Examples"></a> 예  
 다음 예에서는 다른 도메인에 있는 `REMOTESYSTEM3` 이라는 컴퓨터 시스템의 서버 인스턴스에 대한 서버 네트워크 주소를 보여 줍니다. 도메인 정보는 `NORTHWEST.ADVENTURE-WORKS.COM`이고 데이터베이스 미러링 끝점의 포트는 `7025`입니다. 이러한 예제 구성 요소가 지정되면 서버 네트워크 주소는 다음과 같습니다.  
  
 `TCP://REMOTESYSTEM3.NORTHWEST.ADVENTURE-WORKS.COM:7025`  
  
 다음 예에서는 `DBSERVER1`이라는 컴퓨터 시스템의 서버 인스턴스에 대한 서버 네트워크 주소를 보여 줍니다. 이 시스템은 로컬 도메인에 있으며 해당 시스템 이름으로 명확하게 식별됩니다. 데이터베이스 미러링 끝점의 포트는 `7022`입니다.  
  
 `TCP://DBSERVER1:7022`  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [Windows 인증에 대한 데이터베이스 미러링 끝점 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 끝점&#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
