---
title: 가용성 복제본 추가 또는 수정 시 끝점 URL 지정 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- endpoints [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], endpoint
- Endpoint URLs (HADR)
ms.assetid: d7520c13-a8ee-4ddc-9e9a-54cd3d27ef1c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: da1eb2bacd4d5a2f7d0b2a623343f62b5e89597d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936402"
---
# <a name="specify-the-endpoint-url-when-adding-or-modifying-an-availability-replica-sql-server"></a>가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정(SQL Server)
  가용성 그룹에 대한 가용성 복제본을 호스팅하려면 서버 인스턴스에서 데이터베이스 미러링 엔드포인트를 처리해야 합니다. 서버 인스턴스는 이 엔드포인트를 사용하여 다른 서버 인스턴스에서 호스팅하는 가용성 복제본의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 메시지를 수신합니다. 가용성 그룹에 대한 가용성 복제본을 정의하려면 복제본을 호스팅하는 서버 인스턴스의 엔드포인트 URL을 지정해야 합니다. *끝점 URL* 은 데이터베이스 미러링 끝점의 전송 프로토콜인 TCP, 서버 인스턴스의 시스템 주소, 끝점과 연결 된 포트 번호를 식별 합니다.  
  
> [!NOTE]  
>  "엔드포인트 URL"이라는 용어는 데이터베이스 미러링 사용자 인터페이스 및 설명서에서 사용하는 "서버 네트워크 주소"라는 용어와 동의어입니다.  
  
-   [끝점 URL의 구문](#SyntaxOfURL)  
  
-   [시스템의 정규화된 도메인 이름 찾기](#Finding_FQDN)  
  
-   [관련 작업](#RelatedTasks)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="syntax-for-an-endpoint-url"></a><a name="SyntaxOfURL"></a> 엔드포인트 URL의 구문  
 엔드포인트 URL의 구문은 다음 형식을 사용합니다.  
  
 TCP:<strong>//</strong> *\<system-address>* <strong>:</strong>*\<port>*  
  
 라는 설치 관리자 실행 파일에 포함됩니다. 여기서  
  
-   *\<system-address>* 는 대상 컴퓨터 시스템을 명확 하 게 식별 하는 문자열입니다. 일반적으로 서버 주소는 시스템 이름(시스템이 같은 도메인에 있는 경우), 정규화된 도메인 이름 또는 IP 주소입니다.  
  
    -   WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드는 같은 도메인에 있으므로 컴퓨터 시스템의 이름(예: `SYSTEM46`)을 사용할 수 있습니다.  
  
    -   IP 주소를 사용하려면 환경에서 고유한 주소여야 합니다. 정적인 경우에만 IP 주소를 사용하는 것이 좋습니다. IP 주소는 IP 버전 4(IPv4) 또는 IP 버전 6(IPv6)일 수 있습니다. IPv6 주소는 대괄호로 묶어야 합니다 (예: **[** _<IPv6_address>_ **])**.  
  
         시스템의 IP 주소를 확인하려면 Windows 명령 프롬프트에서 **ipconfig** 명령을 입력합니다.  
  
    -   정규화된 도메인 이름을 사용하는 것이 좋습니다. 이 주소 문자열은 로컬로 정의되므로 위치에 따라 형식이 달라집니다. 항상은 아니지만 정규화된 도메인 이름은 컴퓨터 이름과 마침표로 구분된 일련의 도메인 세그먼트를 다음 형식으로 포함하는 복합 이름입니다.  
  
         _computer_name_ **.** _domain_segment_[...**.**_domain_segment_]  
  
         여기에서 *computer_name*은 서버 인스턴스를 실행하는 컴퓨터의 네트워크 이름이고 *domain_segment*[...**.**_domain_segment_]는 서버의 나머지 도메인 정보입니다(예: `localinfo.corp.Adventure-Works.com`).  
  
         도메인 세그먼트의 내용과 개수는 회사 또는 조직 내에서 결정됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [정규화된 도메인 이름 찾기](#Finding_FQDN)를 참조하세요.  
  
-   *\<port>* 파트너 서버 인스턴스의 미러링 끝점에서 사용 하는 포트 번호입니다.  
  
     데이터베이스 미러링 엔드포인트는 컴퓨터 시스템에서 사용 가능한 모든 포트를 사용할 수 있습니다. 각 포트 번호는 하나의 엔드포인트에만 연결되어야 하고 각 엔드포인트는 단일 서버 인스턴스와 연결되므로 같은 서버의 서로 다른 서버 인스턴스는 서로 다른 포트의 각 엔드포인트에서 수신합니다. 따라서 가용성 복제본을 지정할 때 엔드포인트 URL에서 지정하는 포트는 항상 들어오는 메시지를 엔드포인트가 해당 포트와 연결된 서버 인스턴스로 지정합니다.  
  
     엔드포인트 URL에서는 포트 번호를 통해서만 대상 컴퓨터에서 미러링 엔드포인트와 연결되는 서버 인스턴스가 식별됩니다. 다음 그림에서는 단일 컴퓨터에 있는 두 서버 인스턴스의 엔드포인트 URL을 보여 줍니다. 기본 인스턴스는 포트 `7022` 를 사용하고 명명된 인스턴스는 포트 `7033`을 사용합니다. 이러한 두 서버 인스턴스에 대한 엔드포인트 URL은 각각 `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` 및 `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`입니다. 주소에는 서버 인스턴스 이름이 포함되지 않습니다.  
  
     ![기본 인스턴스의 서버 네트워크 주소](../../media/dbm-2-instances-ports-1-system.gif "기본 인스턴스의 서버 네트워크 주소")  
  
     서버 인스턴스의 데이터베이스 미러링 엔드포인트와 현재 연결된 포트를 식별하려면 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```sql
    SELECT type_desc, port FROM sys.TCP_endpoints  
    ```  
  
     **type_desc** 값이 "DATABASE_MIRRORING"인 행을 찾아 해당 포트 번호를 사용합니다.  
  
### <a name="examples"></a>예  
  
#### <a name="a-using-a-system-name"></a>A. 시스템 이름 사용  
 다음 엔드포인트 URL은 시스템 이름 `SYSTEM46` 및 포트 `7022`를 지정합니다.  
  
 `TCP://SYSTEM46:7022`  
  
#### <a name="b-using-a-fully-qualified-domain-name"></a>B. 정규화된 도메인 이름 사용  
 다음 엔드포인트 URL은 정규화된 도메인 이름 `DBSERVER8.manufacturing.Adventure-Works.com` 및 포트 `7024`를 지정합니다.  
  
 `TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024`  
  
#### <a name="c-using-ipv4"></a>C. IPv4 사용  
 다음 엔드포인트 URL은 IPv4 주소 `10.193.9.134` 및 포트 `7023`을 지정합니다.  
  
 `TCP://10.193.9.134:7023`  
  
#### <a name="d-using-ipv6"></a>D. IPv6 사용  
 다음 엔드포인트 URL에는 IPv6 주소 `2001:4898:23:1002:20f:1fff:feff:b3a3` 및 포트 `7022`가 포함되어 있습니다.  
  
 `TCP://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022`  
  
##  <a name="finding-the-fully-qualified-domain-name-of-a-system"></a><a name="Finding_FQDN"></a>시스템의 정규화 된 도메인 이름 찾기  
 시스템의 정규화된 도메인 이름을 찾으려면 해당 시스템의 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
 **IPCONFIG /ALL**  
  
 정규화된 도메인 이름을 구성하려면 *<host_name>* 및 *<Primary_Dns_Suffix>* 의 값을 다음과 같이 연결해야 합니다.  
  
 _<host_name>_ **.** _<Primary_Dns_Suffix>_  
  
 예를 들어 다음 IP 구성은  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 다음 정규화된 도메인 이름과 같습니다.  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
> [!NOTE]  
>  정규화된 도메인 이름에 대한 자세한 내용은 시스템 관리자에게 문의하세요.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
 **데이터베이스 미러링 엔드포인트를 구성하려면**  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server PowerShell에 대 한 데이터베이스 미러링 끝점을 만듭니다&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [데이터베이스 미러링 엔드포인트의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [삭제&#41;SQL Server AlwaysOn 가용성 그룹 구성 &#40;문제 해결](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
 **데이터베이스 미러링 엔드포인트에 대한 정보를 보려면**  
  
-   [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **가용성 복제본을 추가하려면**  
  
-   [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server AlwaysOn 솔루션 가이드](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>참고 항목  
 [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
