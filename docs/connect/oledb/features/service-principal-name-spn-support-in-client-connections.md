---
title: 클라이언트 연결의 서비스 사용자 이름 (SPN) 지원 | Microsoft Docs
description: 클라이언트 연결의 이름 SPN (서비스 사용자) 지원
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, SPNs
- OLE DB, SPNs
- SPNs [SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 802d8593c671ecef58f5a0eea8439e2f16898de1
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612328"
---
# <a name="service-principal-name-spn-support-in-client-connections"></a>클라이언트 연결의 SPN(서비스 사용자 이름) 지원 
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  부터는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], 모든 프로토콜에서 상호 인증을 사용 하도록 서비스 사용자 이름 (Spn)에 대 한 지원이 확장 되었습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Spn 대해서만 지원 되었습니다 Kerberos TCP를 통한 때 기본에 대 한 SPN의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Active Directory에 등록 된 인스턴스가 있습니다.  
  
 Spn을 사용 하는 인증 프로토콜에 의해 결정 되는 계정을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 실행 합니다. 인스턴스 계정이 알려진 경우 Kerberos 인증을 사용하여 클라이언트와 서버에 의한 상호 인증을 제공할 수 있습니다. 인스턴스 계정이 알려지지 않은 경우 서버에 의한 클라이언트 인증만 제공하는 NTLM 인증이 사용됩니다. 현재 OLE DB Driver for SQL Server는 인스턴스 이름과 네트워크 연결 속성에서 SPN을 파생 시켜 인증 조회를 수행 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스는 시작 시 Spn 등록을 시도 하거나 수동으로 등록할 수 있습니다. SPN을 등록하려고 시도하는 계정에 액세스 권한이 충분하지 않은 경우 등록은 실패하게 됩니다.  
  
 도메인 및 컴퓨터 계정은 Active Directory에 자동으로 등록됩니다. 이러한 계정을 SPN으로 사용할 수 있고 관리자가 직접 자신의 SPN을 정의할 수도 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보안 인증의 좀 더 관리 및 신뢰할 수 있는 클라이언트가 사용할 SPN을 직접 지정 하도록 허용 하 여 만듭니다.  
  
> [!NOTE]  
>  클라이언트 응용 프로그램에서 지정한 SPN은 Windows 통합 보안으로 연결이 설정되는 경우에만 사용됩니다.  
  
> [!TIP]  
>  **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Kerberos 구성 관리자**는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]과의 Kerberos 관련 연결 문제를 해결하는 진단 도구입니다. 자세한 내용은 [SQL Server용 Microsoft Kerberos 구성 관리자](http://www.microsoft.com/download/details.aspx?id=39046)를 참조하십시오.  
  
 Kerberos에 대한 자세한 내용은 다음 문서를 참조하십시오.  
  
-   [Windows 용 Kerberos 기술 보충 자료](http://go.microsoft.com/fwlink/?LinkId=101449)  
  
-   [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758)  
  
## <a name="usage"></a>사용법  
 다음 표에서는 클라이언트 응용 프로그램이 보안 인증을 사용할 수 있는 가장 일반적인 시나리오에 대해 설명합니다.  
  
|시나리오|Description|  
|--------------|-----------------|  
|레거시 응용 프로그램이 SPN을 지정하지 않습니다.|이 호환성 시나리오는 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용으로 개발된 응용 프로그램의 동작에 변화가 없을 것임을 보장합니다.  지정된 SPN이 없으면 해당 응용 프로그램은 생성된 SPN에 의존하며, 어떤 인증 방법이 사용되는지 알 수 없습니다.|  
|현재 버전의 OLE DB 드라이버를 사용 하 여 SQL Server에 대 한 클라이언트 응용 프로그램 도메인 사용자 또는 컴퓨터 계정으로, 인스턴스별 SPN으로 또는 사용자 정의 문자열로 연결 문자열에 SPN을 지정 합니다.|공급자, 초기화 또는 연결 문자열에서 **ServerSPN** 키워드를 사용하여 다음을 수행할 수 있습니다.<br /><br /> -에서 사용할 계정을 지정 하십시오.는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 연결에 대 한 합니다. 이를 통해 Kerberos 인증에 대한 액세스가 간소화됩니다. Kerberos KDC(키 배포 센터)가 있고 올바른 계정이 지정된 경우 NTLM보다 Kerberos 인증이 사용될 가능성이 더 높습니다. KDC는 일반적으로 도메인 컨트롤러와 동일한 컴퓨터에 위치합니다.<br /><br /> --서비스 계정에 대 한를 조회 하는 SPN을 지정 하는 중는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스. 에 대 한 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를이 용도로 사용할 수 있는 두 개의 기본 Spn이 생성 됩니다. 그러나 키가 Active Directory에 있다는 보장은 없으므로 이 경우 Kerberos 인증이 보장되지는 않습니다.<br /><br /> -에 대 한 서비스 계정을 조회에 사용할 SPN을 지정 합니다.는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스. 이는 서비스 계정에 매핑되는 사용자 정의 문자열일 수 있습니다. 이 경우 키는 KDC에 수동으로 등록해야 하며 사용자 정의 SPN에 대한 규칙을 충족해야 합니다.<br /><br /> **FailoverPartnerSPN** 키워드를 사용하여 장애 조치(Failover) 파트너 서버에 대한 SPN을 지정할 수 있습니다. 계정 및 Active Directory 키 값의 범위는 주 서버에 지정할 수 있는 값과 동일합니다.|  
|OLE DB 응용 프로그램이 주 서버 또는 장애 조치 파트너 서버에 대한 데이터 원본 초기화 속성으로 SPN을 지정합니다.|**SSPROP_INIT_SERVER_SPN** 속성 집합의 **DBPROPSET_SQLSERVERDBINIT** 연결 속성을 사용하여 연결에 대한 SPN을 지정할 수 있습니다.<br /><br /> **SSPROP_INIT_FAILOVER_PARTNER_SPN** 의 **DBPROPSET_SQLSERVERDBINIT** 연결 속성을 사용하여 장애 조치 파트너 서버에 대한 SPN을 지정할 수 있습니다.|   
|사용자가 OLE DB **데이터 연결** 또는 **로그인** 대화 상자에 서버 또는 장애 조치 파트너 서버에 대한 SPN을 지정합니다.|SPN은 **데이터 연결** 또는 **로그인** 대화 상자에 지정할 수 있습니다.|   
|OLE DB 응용 프로그램이 연결을 설정하는 데 사용된 인증 방법을 확인합니다.|연결이 성공적으로 열리면 응용 프로그램은 **SSPROP_AUTHENTICATION_METHOD** 속성 집합의 **DBPROPSET_SQLSERVERDATASOURCEINFO** 연결 속성을 쿼리하여 사용된 인증 방법을 확인할 수 있습니다. 값에는 **NTLM** , **Kerberos**등이 포함됩니다.|  
  
## <a name="failover"></a>장애 조치  
 SPN이 장애 조치 캐시에 저장되지 않아 연결 간에 전달될 수 없습니다. 연결 문자열 또는 연결 특성에 SPN이 지정되면 주 서버 및 파트너 서버에 대한 모든 연결 시도에 SPN이 사용됩니다.  
  
## <a name="connection-pooling"></a>연결 풀링  
 응용 프로그램에서는 전체 문자열이 아닌 일부에 SPN을 지정하면 풀 조각화가 발생할 수 있음을 인식해야 합니다.  
  
 응용 프로그램은 연결 문자열 키워드를 지정하는 대신 프로그래밍 방식으로 SPN을 연결 특성으로 지정할 수 있습니다. 이렇게 하면 연결 풀 조각화를 보다 용이하게 관리할 수 있습니다.  
  
 응용 프로그램에서는 해당 연결 특성을 설정하여 연결 문자열의 SPN을 재정의할 수 있지만 연결 풀링에 사용되는 연결 문자열은 풀링을 위해 연결 문자열 값을 사용한다는 점을 인식해야 합니다.   
  
## <a name="down-level-server-behavior"></a>하위 수준 서버 동작  
 새 연결 동작은 클라이언트에 의해 구현되므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 특정 버전에 국한되지 않습니다.   
  
## <a name="linked-servers-and-delegation"></a>연결된 서버 및 위임  
 연결 된 서버를 만들면는 **@provstr** 의 매개 변수 [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 서버 및 장애 조치 파트너 Spn 지정 데 사용할 수 있습니다. 이렇게 하는 경우의 장점은 클라이언트 연결 문자열에 SPN을 지정하는 경우와 동일합니다. Kerberos 인증을 사용하는 연결을 설정하는 것이 더 쉽고 안정적입니다.  
  
 연결된 서버를 사용한 위임에는 Kerberos 인증이 필요합니다.  
  
## <a name="management-aspects-of-spns-specified-by-applications"></a>응용 프로그램에서 지정하는 SPN의 관리 측면  
 응용 프로그램에서 연결 문자열을 통해 SPN을 지정할지, 또는 기본 공급자가 생성한 SPN을 사용하지 않고 연결 속성을 통해 프로그래밍 방식으로 SPN을 지정할지 선택할 때는 다음 사항을 고려해야 합니다.  
  
-   보안: 지정된 SPN이 보호되는 정보를 노출하나요?  
  
-   안정성: 기본 Spn 사용을 사용 하려면 서비스는 계정에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 실행 되는 KDC에 Active Directory를 업데이트할 수 있는 권한이 있어야 합니다.  
  
-   편의성 및 위치 투명성: 다른 데이터베이스를 이동 하는 경우 영향을 받습니까 응용 프로그램의 Spn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스? 데이터베이스 미러링을 사용하는 경우 이는 주 서버 및 해당 장애 조치 파트너 모두에 적용됩니다. 서버 변경 시 SPN도 변경해야 한다면 응용 프로그램은 어떤 영향을 받습니까? 변경 내용은 관리됩니까?  
  
## <a name="specifying-the-spn"></a>SPN 지정  
 대화 상자 또는 코드에서 SPN을 지정할 수 있습니다. 이 섹션에서는 SPN을 지정하는 방법에 대해 설명합니다.  
  
 SPN의 최대 길이는 260자입니다.  
  
 SPN이 연결 문자열 또는 연결 특성에서 사용하는 구문은 다음과 같습니다.  
  
|구문|Description|  
|------------|-----------------|  
|MSSQLSvc/*fqdn*|TCP 이외의 프로토콜이 사용될 때 기본 인스턴스에 대해 공급자가 생성하는 기본 SPN입니다.<br /><br /> *fqdn* 은 정규화된 도메인 이름입니다.|  
|MSSQLSvc/*fqdn*:*port*|TCP가 사용될 때 공급자가 생성하는 기본 SPN입니다.<br /><br /> *port* 는 TCP 포트 번호입니다.|  
|MSSQLSvc/*fqdn*:*InstanceName*|TCP 이외의 프로토콜이 사용될 때 명명된 인스턴스에 대해 공급자가 생성하는 기본 SPN입니다.<br /><br /> *InstanceName* 는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.|  
|HOST/*fqdn*<br /><br /> HOST/*MachineName*|Windows에서 자동으로 등록되는 기본 제공 컴퓨터 계정에 매핑되는 SPN입니다.|  
|*Username*@*Domain*|도메인 계정 직접 지정입니다.<br /><br /> *Username* 은 Windows 사용자 계정 이름입니다.<br /><br /> *Domain* 은 Windows 도메인 이름 또는 정규화된 도메인 이름입니다.|  
|*MachineName*$@*Domain*|컴퓨터 계정 직접 지정입니다.<br /><br /> 연결 중인 서버가 LOCAL SYSTEM 또는 NETWORK SERVICE 계정으로 실행되는 경우 **ServerSPN** 을 *MachineName*$@*Domain* 형식으로 사용하여 Kerberos 인증을 받을 수 있습니다.|  
|*KDCKey*/*MachineName*|사용자가 지정한 SPN<br /><br /> *KDCKey* 는 KDC 키에 대한 규칙을 따르는 영숫자 문자열입니다.|  
  
## <a name="ole-db-syntax-supporting-spns"></a>OLE DB 구문 지 원하는 Spn  
 구문별 정보는 다음 항목을 참조하십시오.  
  
-   [서비스 사용자 이름 &#40;Spn&#41; 클라이언트 연결의 &#40;OLE DB&#41;](../../oledb/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
 이 기능을 보여 주는 예제 응용 프로그램에 대한 자세한 내용은 [SQL Server 데이터 프로그래밍 기능 예제](http://msftdpprodsamples.codeplex.com/)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB Driver for SQL Server 기능](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [Kerberos 연결의 서비스 사용자 이름 등록](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
