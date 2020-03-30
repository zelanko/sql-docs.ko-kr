---
title: 클라이언트 연결의 SPN(서비스 사용자 이름) 지원 | Microsoft Docs
description: 클라이언트 연결의 SPN(서비스 사용자 이름) 지원
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, SPNs
- OLE DB, SPNs
- SPNs [SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: e7b61536b335d6cbbcdc78e77e0ebbeb18618a22
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74056676"
---
# <a name="service-principal-name-spn-support-in-client-connections"></a>클라이언트 연결의 SPN(서비스 사용자 이름) 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]부터는 모든 프로토콜에서 상호 인증을 지원하도록 SPN(서비스 사용자 이름)이 확장되었습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 SPN은 Active Directory에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 기본 SPN이 등록된 경우 TCP를 사용하는 Kerberos에 대해서만 지원되었습니다.  
  
 SPN은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 실행되는 계정을 확인하기 위해 인증 프로토콜에 의해 사용됩니다. 인스턴스 계정이 알려진 경우 Kerberos 인증을 사용하여 클라이언트와 서버에 의한 상호 인증을 제공할 수 있습니다. 인스턴스 계정이 알려지지 않은 경우 서버에 의한 클라이언트 인증만 제공하는 NTLM 인증이 사용됩니다. 현재 SQL Server용 OLE DB 드라이버는 인스턴스 이름과 네트워크 연결 속성에서 SPN을 파생시켜 인증 조회를 수행합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스는 시작 시에 SPN 등록을 시도하며 또는 수동으로 등록할 수도 있습니다. SPN을 등록하려고 시도하는 계정에 액세스 권한이 충분하지 않은 경우 등록은 실패하게 됩니다.  
  
 도메인 및 컴퓨터 계정은 Active Directory에 자동으로 등록됩니다. 이러한 계정을 SPN으로 사용할 수 있고 관리자가 직접 자신의 SPN을 정의할 수도 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 클라이언트에서 사용할 SPN을 직접 지정하도록 허용하여 보안 인증의 관리성과 안정성을 더 높여 줍니다.  
  
> [!NOTE]  
>  클라이언트 애플리케이션에서 지정한 SPN은 Windows 통합 보안으로 연결이 설정되는 경우에만 사용됩니다.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../../includes/msconame-md.md)]용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Kerberos 구성 관리자**는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]과의 Kerberos 관련 연결 문제를 해결하는 진단 도구입니다. 자세한 내용은 [SQL Server용 Microsoft Kerberos 구성 관리자](https://www.microsoft.com/download/details.aspx?id=39046)를 참조하십시오.  
  
 Kerberos에 대한 자세한 내용은 다음 문서를 참조하십시오.  
  
-   [Windows용 Kerberos 기술 보충 자료](https://go.microsoft.com/fwlink/?LinkId=101449)  
  
-   [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)  
  
## <a name="usage"></a>사용  
 다음 표에서는 클라이언트 애플리케이션이 보안 인증을 사용할 수 있는 가장 일반적인 시나리오에 대해 설명합니다.  
  
|시나리오|Description|  
|--------------|-----------------|  
|레거시 애플리케이션이 SPN을 지정하지 않습니다.|이 호환성 시나리오는 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용으로 개발된 애플리케이션의 동작에 변화가 없을 것임을 보장합니다. 지정된 SPN이 없으면 해당 애플리케이션은 생성된 SPN에 의존하며, 어떤 인증 방법이 사용되는지 알 수 없습니다.|  
|현재 버전의 SQL Server용 OLE DB 드라이버를 사용하는 클라이언트 애플리케이션이 연결 문자열의 SPN을 도메인 사용자 또는 컴퓨터 계정으로, 인스턴스별 SPN으로, 또는 사용자 정의 문자열로 지정합니다.|공급자, 초기화 또는 연결 문자열에서 **ServerSPN** 키워드를 사용하여 다음을 수행할 수 있습니다.<br /><br /> -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 연결에 사용하는 계정을 지정합니다. 이를 통해 Kerberos 인증에 대한 액세스가 간소화됩니다. Kerberos KDC(키 배포 센터)가 있고 올바른 계정이 지정된 경우 NTLM보다 Kerberos 인증이 사용될 가능성이 더 높습니다. KDC는 일반적으로 도메인 컨트롤러와 동일한 컴퓨터에 위치합니다.<br /><br /> -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 서비스 계정을 조회하기 위해 SPN을 지정합니다. 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대해 이 용도로 사용할 수 있는 두 개의 기본 SPN이 생성됩니다. 그러나 키가 Active Directory에 있다는 보장은 없으므로 이 경우 Kerberos 인증이 보장되지는 않습니다.<br /><br /> -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 서비스 계정을 조회하는 데 사용될 SPN을 지정합니다. 이는 서비스 계정에 매핑되는 사용자 정의 문자열일 수 있습니다. 이 경우 키는 KDC에 수동으로 등록해야 하며 사용자 정의 SPN에 대한 규칙을 충족해야 합니다.<br /><br /> **FailoverPartnerSPN** 키워드를 사용하여 장애 조치(Failover) 파트너 서버에 대한 SPN을 지정할 수 있습니다. 계정 및 Active Directory 키 값의 범위는 주 서버에 지정할 수 있는 값과 동일합니다.|  
|OLE DB 애플리케이션이 주 서버 또는 장애 조치 파트너 서버에 대한 데이터 원본 초기화 속성으로 SPN을 지정합니다.|**SSPROP_INIT_SERVER_SPN** 속성 집합의 **DBPROPSET_SQLSERVERDBINIT** 연결 속성을 사용하여 연결에 대한 SPN을 지정할 수 있습니다.<br /><br /> **SSPROP_INIT_FAILOVER_PARTNER_SPN** 의 **DBPROPSET_SQLSERVERDBINIT** 연결 속성을 사용하여 장애 조치 파트너 서버에 대한 SPN을 지정할 수 있습니다.|   
|사용자가 OLE DB **데이터 연결** 또는 **로그인** 대화 상자에 서버 또는 장애 조치 파트너 서버에 대한 SPN을 지정합니다.|SPN은 **데이터 연결** 또는 **로그인** 대화 상자에 지정할 수 있습니다.|   
|OLE DB 애플리케이션이 연결을 설정하는 데 사용된 인증 방법을 확인합니다.|연결이 성공적으로 열리면 애플리케이션은 **SSPROP_AUTHENTICATION_METHOD** 속성 집합의 **DBPROPSET_SQLSERVERDATASOURCEINFO** 연결 속성을 쿼리하여 사용된 인증 방법을 확인할 수 있습니다. 값에는 **NTLM** , **Kerberos**등이 포함됩니다.|  
  
## <a name="failover"></a>장애 조치  
 SPN이 장애 조치 캐시에 저장되지 않아 연결 간에 전달될 수 없습니다. 연결 문자열 또는 연결 특성에 SPN이 지정되면 주 서버 및 파트너 서버에 대한 모든 연결 시도에 SPN이 사용됩니다.  
  
## <a name="connection-pooling"></a>연결 풀링  
 애플리케이션에서는 전체 문자열이 아닌 일부에 SPN을 지정하면 풀 조각화가 발생할 수 있음을 인식해야 합니다.  
  
 애플리케이션은 연결 문자열 키워드를 지정하는 대신 프로그래밍 방식으로 SPN을 연결 특성으로 지정할 수 있습니다. 이렇게 하면 연결 풀 조각화를 보다 용이하게 관리할 수 있습니다.  
  
 애플리케이션에서는 해당 연결 특성을 설정하여 연결 문자열의 SPN을 재정의할 수 있지만 연결 풀링에 사용되는 연결 문자열은 풀링을 위해 연결 문자열 값을 사용한다는 점을 인식해야 합니다.  
  
## <a name="down-level-server-behavior"></a>하위 수준 서버 동작  
 새 연결 동작은 클라이언트에 의해 구현되므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 특정 버전에 국한되지 않습니다.  
  
## <a name="linked-servers-and-delegation"></a>연결된 서버 및 위임  
 연결된 서버가 만들어질 때 **sp_addlinkedserver\@ 의** [provstr](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 매개 변수를 사용하여 서버 및 장애 조치 파트너 SPN을 지정할 수 있습니다. 이렇게 하는 경우의 이점은 클라이언트 연결 문자열에 SPN을 지정하는 경우와 동일합니다. Kerberos 인증을 사용하는 연결을 설정하는 것이 더 쉽고 안정적입니다.  
  
 연결된 서버를 사용한 위임에는 Kerberos 인증이 필요합니다.  
  
## <a name="management-aspects-of-spns-specified-by-applications"></a>애플리케이션에서 지정하는 SPN의 관리 측면  
 애플리케이션에서 연결 문자열을 통해 SPN을 지정할지, 또는 기본 공급자가 생성한 SPN을 사용하지 않고 연결 속성을 통해 프로그래밍 방식으로 SPN을 지정할지 선택할 때는 다음 사항을 고려해야 합니다.  
  
-   보안: 지정된 SPN이 보호되는 정보를 노출하나요?  
  
-   안정성: 기본 SPN 사용을 활성화하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 실행되는 서비스 계정에 KDC의 Active Directory를 업데이트할 수 있는 권한이 있어야 합니다.  
  
-   편의성 및 위치 투명성: 데이터베이스가 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스로 이동되는 경우 애플리케이션의 SPN에 어떤 영향이 있나요? 데이터베이스 미러링을 사용하는 경우 이는 주 서버 및 해당 장애 조치 파트너 모두에 적용됩니다. 서버 변경 시 SPN도 변경해야 한다면 애플리케이션은 어떤 영향을 받습니까? 변경 내용은 관리됩니까?  
  
## <a name="specifying-the-spn"></a>SPN 지정  
 대화 상자 또는 코드에서 SPN을 지정할 수 있습니다. 이 섹션에서는 SPN을 지정하는 방법에 대해 설명합니다.  
  
 SPN의 최대 길이는 260자입니다.  
  
 SPN이 연결 문자열 또는 연결 특성에서 사용하는 구문은 다음과 같습니다.  
  
|구문|Description|  
|------------|-----------------|  
|MSSQLSvc/*fqdn*|TCP 이외의 프로토콜이 사용될 때 기본 인스턴스에 대해 공급자가 생성하는 기본 SPN입니다.<br /><br /> *fqdn* 은 정규화된 도메인 이름입니다.|  
|MSSQLSvc/*fqdn*:*port*|TCP가 사용될 때 공급자가 생성하는 기본 SPN입니다.<br /><br /> *port* 는 TCP 포트 번호입니다.|  
|MSSQLSvc/*fqdn*:*InstanceName*|TCP 이외의 프로토콜이 사용될 때 명명된 인스턴스에 대해 공급자가 생성하는 기본 SPN입니다.<br /><br /> *InstanceName*은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.|  
|HOST/*fqdn*<br /><br /> HOST/*MachineName*|Windows에서 자동으로 등록되는 기본 제공 컴퓨터 계정에 매핑되는 SPN입니다.|  
|*Username*@*Domain*|도메인 계정 직접 지정입니다.<br /><br /> *Username* 은 Windows 사용자 계정 이름입니다.<br /><br /> *Domain* 은 Windows 도메인 이름 또는 정규화된 도메인 이름입니다.|  
|*MachineName*$@*Domain*|컴퓨터 계정 직접 지정입니다.<br /><br /> 연결 중인 서버가 LOCAL SYSTEM 또는 NETWORK SERVICE 계정으로 실행되는 경우 **ServerSPN** 을 *MachineName*$@*Domain* 형식으로 사용하여 Kerberos 인증을 받을 수 있습니다.|  
|*KDCKey*/*MachineName*|사용자가 지정한 SPN<br /><br /> *KDCKey* 는 KDC 키에 대한 규칙을 따르는 영숫자 문자열입니다.|  
  
## <a name="ole-db-syntax-supporting-spns"></a>SPN을 지원하는 OLE DB 구문  
 구문별 정보는 다음 항목을 참조하십시오.  
  
-   [클라이언트 연결&#40;OLE DB&#41;의 SPN&#40;서비스 사용자 이름&#41;](../../oledb/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
 이 기능을 보여 주는 예제 애플리케이션에 대한 자세한 내용은 [SQL Server 데이터 프로그래밍 기능 예제](https://msftdpprodsamples.codeplex.com/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [Kerberos 연결의 서비스 사용자 이름 등록](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
