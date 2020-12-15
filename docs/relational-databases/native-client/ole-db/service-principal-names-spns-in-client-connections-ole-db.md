---
description: 클라이언트 연결의 SPN(서비스 사용자 이름)(OLE DB)
title: OLE DB 서비스 사용자 이름 연결
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e212010e-a5b6-4ad1-a3c0-575327d3ffd3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 46829a2b33ee00aa986f73126a9ab2f4cf1a896d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467544"
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>클라이언트 연결의 SPN(서비스 사용자 이름)(OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  이 항목에서는 클라이언트 애플리케이션의 SPN(서비스 사용자 이름)을 지원하는 OLE DB 속성 및 멤버 함수에 대해 설명합니다. 클라이언트 애플리케이션에서 SPN에 대한 자세한 내용은 [클라이언트 연결에서 &#40;SPN&#41;(서비스 사용자 이름) 지원](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)을 참조하세요. 샘플은 [통합 Kerberos 인증&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/integrated-kerberos-authentication-ole-db.md)을 참조하세요.  
  
## <a name="provider-initialization-string-keywords"></a>공급자 초기화 문자열 키워드  
 다음과 같은 공급자 초기화 문자열 키워드가 OLE DB 애플리케이션에서 SPN을 지원합니다. 다음 표에서 키워드 열의 값은 IDBInitialize::Initialize의 공급자 문자열에 사용됩니다. 설명 열의 값은 ADO 또는 IDataInitialize::GetDataSource를 사용하여 연결할 때 초기화 문자열에 사용됩니다.  
  
|키워드|Description|값|  
|-------------|-----------------|-----------|  
|ServerSPN|서버 SPN|서버의 SPN입니다. 기본값인 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|FailoverPartnerSPN|장애 조치(Failover) 파트너 SPN|장애 조치(failover) 파트너의 SPN입니다. 기본값인 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
  
## <a name="data-source-initialization-properties"></a>데이터 원본 초기화 속성  
 **DBPROPSET_SQLSERVERDBINIT** 속성 집합의 다음 속성을 사용하면 애플리케이션에서 SPN을 지정할 수 있습니다.  
  
|속성|Type|사용|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR, 읽기/쓰기|서버의 SPN을 지정합니다. 기본값인 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR, 읽기/쓰기|장애 조치(Failover) 파트너의 SPN을 지정합니다. 기본값인 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
  
## <a name="data-source-properties"></a>데이터 원본 속성  
 **DBPROPSET_SQLSERVERDATASOURCEINFO** 속성 집합의 다음 속성을 사용하면 애플리케이션에서 인증 방법을 검색할 수 있습니다.  
  
|속성|Type|사용|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR, 읽기 전용|연결에 사용된 인증 방법을 반환합니다. 애플리케이션으로 반환되는 값은 Windows에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client로 반환하는 값입니다. 다음은 가능한 값입니다. <br />NTLM 인증을 사용하여 연결을 열 때 반환되는 "NTLM"<br />Kerberos 인증을 사용하여 연결을 열 때 반환되는 "Kerberos"<br /><br /> 연결이 열려 있지만 인증 방법을 확인할 수 없는 경우에는 VT_EMPTY가 반환됩니다.<br /><br /> 이 속성은 데이터 원본이 초기화된 경우에만 읽을 수 있습니다. 데이터 원본이 초기화되기 전에 이 속성을 읽으려고 하면 IDBProperties::GetProperies에서 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED가 반환되고 이 속성의 DBPROPSET_PROPERTIESINERROR에 DBPROPSTATUS_NOTSUPPORTED가 설정됩니다. 이 동작은 OLE DB 핵심 사양을 따르는 것입니다.|  
|SSPROP_MUTUALLYAUTHENICATED|VT_BOOL, 읽기 전용|연결의 서버가 상호 인증되었으면 VARIANT_TRUE가 반환되고, 그렇지 않으면 VARIANT_FALSE가 반환됩니다.<br /><br /> 이 속성은 데이터 원본이 초기화된 경우에만 읽을 수 있습니다. 데이터 원본이 초기화되기 전에 이 속성을 읽으려고 하면 IDBProperties::GetProperies에서 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED가 반환되고 이 속성의 DBPROPSET_PROPERTIESINERROR에 DBPROPSTATUS_NOTSUPPORTED가 설정됩니다. 이 동작은 OLE DB 핵심 사양을 따르는 것입니다.<br /><br /> Windows 인증을 사용하지 않은 연결에 대해 이 특성을 쿼리하면 VARIANT_FALSE가 반환됩니다.|  
  
## <a name="ole-db-api-support-for-spns"></a>SPN에 대한 OLE DB API 지원  
 다음 표에서는 클라이언트 연결에서 SPN을 지원하는 OLE DB 멤버 함수에 대해 설명합니다.  
  
|멤버 함수|Description|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString* 은 **ServerSPN** 및 **FailoverPartnerSPN** 을 키워드로 포함할 수 있습니다.|  
|IDataInitialize::GetInitializationString|SSPROP_INIT_SERVERSPN 및 SSPROP_INIT_FAILOVERPARTNERSPN이 기본값이 아닌 경우 *ppwszInitString* 을 통해 **ServerSPN** 및 **FailoverPartnerSPN** 에 대한 키워드 값으로 초기화 문자열에 포함됩니다. 기본값인 경우에는 초기화 문자열에 포함되지 않습니다.|  
|IDBInitialize::Initialize|데이터 원본 초기화 속성에서 DBPROP_INIT_PROMPT를 설정하여 프롬프트를 활성화한 경우 OLE DB 로그인 대화 상자가 표시됩니다. 이를 통해 주 서버 및 해당 장애 조치(Failover) 파트너 모두에 대한 SPN이 입력되도록 할 수 있습니다.<br /><br /> DPPROP_INIT_PROVIDERSTRING에 공급자 문자열이 설정되어 있으면 해당 문자열이 새 키워드인 **ServerSPN** 과 **FailoverPartnerSPN** 을 인식하고 해당 값을 사용하여(있는 경우) SSPROP_INIT_SERVER_SPN 및 SSPROP_INIT_FAILOVER_PARTNER_SPN을 초기화합니다.<br /><br /> IDBInitialize::Initialize를 호출하기 전에 IDBProperties::SetProperties를 호출하여 SSPROP_INIT_SERVER_SPN 및 SSPROP_INIT_FAILOVER_PARTNER_SPN 속성을 설정할 수 있습니다. 이 방법을 공급자 문자열 대신 사용할 수 있습니다.<br /><br /> 두 곳 이상에서 속성이 설정된 경우 프로그래밍 방식으로 설정된 값이 공급자 문자열에 설정된 값보다 우선적으로 적용됩니다. 초기화 문자열에 설정된 값은 로그인 대화 상자에서 설정된 값보다 우선적으로 적용됩니다.<br /><br /> 공급자 문자열에서 동일한 키워드가 여러 번 나타나는 경우 가장 먼저 발견된 값이 우선적으로 적용됩니다.|  
|IDBProperties::GetProperties|IDBProperties::GetProperties를 호출하여 새 데이터 원본 초기화 속성 SSPROP_INIT_SERVERSPN 및 SSPROP_INIT_FAILOVERPARTNERSPN의 값과 새 데이터 원본 속성 SSPROP_AUTHENTICATIONMETHOD 및 SSPROP_MUTUALLYAUTHENTICATED의 값을 가져올 수 있습니다.|  
|IDBProperties::GetPropertyInfo|IdbProperties::GetPropertyInfo에는 새 데이터 원본 초기화 속성 SSPROP_INIT_SERVERSPN 및 SSPROP_INIT_FAILOVERPARTNERSPN이나 새 데이터 원본 속성 SSPROP_AUTHENTICATION_METHOD 및 SSPROP_MUTUALLYAUTHENTICATED가 포함됩니다.|  
|IDBProperties::SetProperties|IDBProperties::SetProperties를 호출하여 새 데이터 원본 초기화 속성 SSPROP_INITSERVERSPN 및 SSPROP_INIT_FAILOVERPARTNERSPN의 값을 설정할 수 있습니다.<br /><br /> 언제라도 이러한 속성을 설정할 수 있지만 데이터 원본이 열려 있는 경우에는 "DB_E_ERRORSOCCURRED, "여러 단계 OLE DB 작업을 하는 동안 오류가 발생했습니다. 각 OLE DB 상태 값이 있으면 확인해 보십시오. 완료된 작업이 없습니다.""라는 오류가 반환됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
