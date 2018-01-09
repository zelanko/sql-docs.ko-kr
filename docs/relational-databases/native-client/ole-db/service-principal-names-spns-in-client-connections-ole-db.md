---
title: "클라이언트 연결 (OLE DB)의 서비스 사용자 이름 (Spn) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e212010e-a5b6-4ad1-a3c0-575327d3ffd3
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2f4140619a98798e057c8e4ae85c1e99c58e68a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>클라이언트 연결의 SPN(서비스 사용자 이름)(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  이 항목에서는 클라이언트 응용 프로그램의 SPN(서비스 사용자 이름)을 지원하는 OLE DB 속성 및 멤버 함수에 대해 설명합니다. 클라이언트 응용 프로그램의 Spn에 대 한 자세한 내용은 참조 [서비스 사용자 이름 &#40; SPN &#41; 클라이언트 연결의 지원](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)합니다. 샘플을 보려면 [통합 Kerberos 인증 &#40; OLE db&#41;](../../../relational-databases/native-client-ole-db-how-to/integrated-kerberos-authentication-ole-db.md)합니다.  
  
## <a name="provider-initialization-string-keywords"></a>공급자 초기화 문자열 키워드  
 다음과 같은 공급자 초기화 문자열 키워드가 OLE DB 응용 프로그램에서 SPN을 지원합니다. 다음 표에서 키워드 열의 값 idbinitialize:: Initialize의 공급자 문자열에 사용 됩니다. 설명 열에 값은 ADO 또는 idatainitialize:: Getdatasource를 사용 하 여 연결할 때 초기화 문자열에 사용 됩니다.  
  
|키워드|Description|값|  
|-------------|-----------------|-----------|  
|ServerSPN|서버 SPN|서버의 SPN입니다. 기본값인 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|FailoverPartnerSPN|장애 조치(Failover) 파트너 SPN|장애 조치(failover) 파트너의 SPN입니다. 기본값인 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
  
## <a name="data-source-initialization-properties"></a>데이터 원본 초기화 속성  
 다음 속성은 **DBPROPSET_SQLSERVERDBINIT** 속성 집합에는 응용 프로그램이 Spn을 지정할 수 있도록 합니다.  
  
|속성|형식|사용법|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR, 읽기/쓰기|서버의 SPN을 지정합니다. 기본값인 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR, 읽기/쓰기|장애 조치(Failover) 파트너의 SPN을 지정합니다. 기본값인 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
  
## <a name="data-source-properties"></a>데이터 원본 속성  
 다음 속성은 **DBPROPSET_SQLSERVERDATASOURCEINFO** 속성 집합에는 응용 프로그램에서 인증 방법을 검색할 수 있도록 합니다.  
  
|속성|형식|사용법|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR, 읽기 전용|연결에 사용된 인증 방법을 반환합니다. 응용 프로그램에 반환되는 값은 Windows에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에 반환하는 값입니다. 다음은 가능한 값입니다. <br />NTLM 인증을 사용하여 연결을 열 때 반환되는 "NTLM"<br />Kerberos 인증을 사용하여 연결을 열 때 반환되는 "Kerberos"<br /><br /> 연결이 열려 있지만 인증 방법을 확인할 수 없는 경우에는 VT_EMPTY가 반환됩니다.<br /><br /> 이 속성은 데이터 원본이 초기화된 경우에만 읽을 수 있습니다. 경우에 데이터 원본이 초기화 되기 전에 속성을 읽을 하려고 하면 IDBProperties::GetProperies 반환 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED가 적절 하 게 하 고 DBPROPSET_PROPERTIESINERROR에 DBPROPSTATUS_NOTSUPPORTED가 설정 됩니다. 이 속성입니다. 이 동작은 OLE DB 핵심 사양을 따르는 것입니다.|  
|SSPROP_MUTUALLYAUTHENICATED|VT_BOOL, 읽기 전용|연결의 서버가 상호 인증되었으면 VARIANT_TRUE가 반환되고, 그렇지 않으면 VARIANT_FALSE가 반환됩니다.<br /><br /> 이 속성은 데이터 원본이 초기화된 경우에만 읽을 수 있습니다. 속성을 읽을 데이터 원본이 초기화 되기 전에 시도가 경우 IDBProperties::GetProperies은 반환 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED가 적절 하 게 하 고 DBPROPSET_에 DBPROPSTATUS_NOTSUPPORTED가 설정 이 속성에 대 한 PROPERTIESINERROR 합니다. 이 동작은 OLE DB 핵심 사양을 따르는 것입니다.<br /><br /> Windows 인증을 사용하지 않은 연결에 대해 이 특성을 쿼리하면 VARIANT_FALSE가 반환됩니다.|  
  
## <a name="ole-db-api-support-for-spns"></a>SPN에 대한 OLE DB API 지원  
 다음 표에서는 클라이언트 연결에서 SPN을 지원하는 OLE DB 멤버 함수에 대해 설명합니다.  
  
|멤버 함수|Description|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString* 새로운 키워드를 포함할 수 있습니다 **ServerSPN** 및 **FailoverPartnerSPN**합니다.|  
|IDataInitialize::GetInitializationString|SSPROP_INIT_SERVERSPN 및 SSPROP_INIT_FAILOVERPARTNERSPN에 기본이 아닌 값이 있으면 이러한에 포함될지를 통해 초기화 문자열 *ppwszInitString* 키워드 값에 대해 **ServerSPN**및 **FailoverPartnerSPN**합니다. 기본값인 경우에는 초기화 문자열에 포함되지 않습니다.|  
|IDBInitialize::Initialize|데이터 원본 초기화 속성에서 DBPROP_INIT_PROMPT를 설정하여 프롬프트를 활성화한 경우 OLE DB 로그인 대화 상자가 표시됩니다. 이를 통해 주 서버 및 해당 장애 조치(Failover) 파트너 모두에 대한 SPN이 입력되도록 할 수 있습니다.<br /><br /> 경우 DPPROP_INIT_PROVIDERSTRING에 공급자 문자열이 설정, 새로운 키워드를 인식 하 게 **ServerSPN** 및 **FailoverPartnerSPN** SSPROP_INIT_SERVER_를 초기화할 수 있는 경우 해당 값을 사용 합니다. SPN 및 ssprop_init_failover_partner_spn을 초기화 합니다.<br /><br /> Idbinitialize:: Initialize를 호출 하기 전에 여 SSPROP_INIT_SERVER_SPN 및 SSPROP_INIT_FAILOVER_PARTNER_SPN 속성을 설정 하려면 idbproperties:: Setproperties는 호출할 수 있습니다. 이 방법을 공급자 문자열 대신 사용할 수 있습니다.<br /><br /> 두 곳 이상에서 속성이 설정된 경우 프로그래밍 방식으로 설정된 값이 공급자 문자열에 설정된 값보다 우선적으로 적용됩니다. 초기화 문자열에 설정된 값은 로그인 대화 상자에서 설정된 값보다 우선적으로 적용됩니다.<br /><br /> 공급자 문자열에서 동일한 키워드가 여러 번 나타나는 경우 가장 먼저 발견된 값이 우선적으로 적용됩니다.|  
|IDBProperties::GetProperties|새 데이터 원본 속성 SSPROP_AUTHENTICATIONMETHOD 및 SSPROP_ 및 새 데이터 원본 초기화 속성 SSPROP_INIT_SERVERSPN 및 SSPROP_INIT_FAILOVERPARTNERSPN의 값을 가져오는 IDBProperties::GetProperties는 호출할 수 있습니다. MUTUALLYAUTHENTICATED 합니다.|  
|Idbproperties:: Getpropertyinfo|Idbproperties:: Getpropertyinfo 새 데이터 원본 초기화 속성 SSPROP_INIT_SERVERSPN 및 SSPROP_INIT_FAILOVERPARTNERSPN 또는 새 데이터 원본 속성 SSPROP_AUTHENTICATION_METHOD 및 ssprop_mutuallyauthenticated가 포함 됩니다.|  
|IDBProperties::SetProperties|값을 설정할 새 데이터 원본 초기화 속성 SSPROP_INITSERVERSPN 및 SSPROP_INIT_FAILOVERPARTNERSPN idbproperties:: Setproperties는 호출할 수 있습니다.<br /><br /> 언제 든 지 이러한 속성을 설정할 수 있지만 데이터 원본이 열려 이미 있으면 다음 오류가 반환 됩니다: DB_E_ERRORSOCCURRED, "작업을 여러 단계 OLE DB 오류가 발생 했습니다. 각 OLE DB 상태 값이 있으면 확인해 보십시오. 완료된 작업이 없습니다.""라는 오류가 반환됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
