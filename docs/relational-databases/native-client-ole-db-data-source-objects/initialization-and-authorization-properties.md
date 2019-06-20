---
title: 초기화 및 권한 부여 속성 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- authorization [OLE DB]
- properties [OLE DB]
- SQL Server Native Client OLE DB provider, initialization properties
- SQL Server Native Client OLE DB provider, authorization properties
- initialization properties [OLE DB]
ms.assetid: 913ab38c-e443-446c-b326-7447e95aa7f9
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e49f9b2bcd4784c76f693863c7837dd827ba2924
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806049"
---
# <a name="initialization-and-authorization-properties"></a>초기화 및 권한 부여 속성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 OLE DB 초기화 및 권한 부여 속성을 다음과 같이 해석합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_AUTH_CACHE_AUTHINFO|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 인증 정보를 캐시하지 않습니다.<br /><br /> 속성 값을 설정하려고 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환합니다. DBPROP 구조의 *dwStatus* 멤버는 DBPROPSTATUS_NOTSUPPORTED를 나타냅니다.|  
|DBPROP_AUTH_ENCRYPT_PASSWORD|합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 표준을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 메커니즘 암호를 숨깁니다.<br /><br /> 속성 값을 설정하려고 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환합니다. DBPROP 구조의 *dwStatus* 멤버는 DBPROPSTATUS_NOTSUPPORTED를 나타냅니다.|  
|DBPROP_AUTH_INTEGRATED|DBPROP_AUTH_INTEGRATED가 NULL 포인터, Null 문자열 또는 'SSPI' VT_BSTR 값으로 설정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 Windows 인증 모드를 사용하여 DBPROP_INIT_DATASOURCE 및 DBPROP_INIT_CATALOG 속성으로 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 사용자 액세스 권한을 부여합니다.<br /><br /> VT_EMPTY(기본값)로 설정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안이 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 암호는 DBPROP_AUTH_USERID 및 DBPROP_AUTH_PASSWORD 속성에 지정됩니다.|  
|DBPROP_AUTH_MASK_PASSWORD|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 표준 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 메커니즘을 사용하여 암호를 숨깁니다.<br /><br /> 속성 값을 설정하려고 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환합니다. DBPROP 구조의 *dwStatus* 멤버는 DBPROPSTATUS_NOTSUPPORTED를 나타냅니다.|  
|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 할당된 암호입니다. 이 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 액세스 권한을 부여하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택한 경우 사용됩니다.|  
|DBPROP_AUTH_PERSIST_ENCRYPTED|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 지속될 경우 인증 정보를 암호화하지 않습니다.<br /><br /> 속성 값을 설정하려고 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환합니다. DBPROP 구조의 *dwStatus* 멤버는 DBPROPSTATUS_NOTSUPPORTED를 나타냅니다.|  
|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 요청된 경우 암호의 이미지를 포함한 인증 값을 지속시킵니다. 암호화는 제공되지 않습니다.|  
|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인입니다. 이 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 액세스 권한을 부여하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택한 경우 사용됩니다.|  
|DBPROP_INIT_ASYNCH|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 비동기 시작을 지원합니다.<br /><br /> DBPROP_INIT_ASYNCH 속성에 DBPROPVAL_ASYNCH_INITIALIZE 비트를 설정하면 **IDBInitialize::Initialize**는 비블로킹 호출이 됩니다. 자세한 내용은 [비동기 작업 수행](../../relational-databases/native-client/features/performing-asynchronous-operations.md)합니다.|  
|DBPROP_INIT_CATALOG|연결할 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 이름입니다.|  
|DBPROP_INIT_DATASOURCE|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 서버의 네트워크 이름입니다. 컴퓨터에서 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행 중인 경우 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하기 위해 DBPROP_INIT_DATASOURCE 값은 *\\\ServerName\InstanceName*으로 지정됩니다. 이스케이프 시퀀스 \\\는 백슬래시 자체에 대해 사용됩니다.|  
|DBPROP_INIT_GENERALTIMEOUT|데이터 원본 초기화 및 명령 실행을 제외한 요청 제한 시간이 초과되기 전까지의 초 수를 나타냅니다. 값 0은 제한 시간이 없음을 나타냅니다. 네트워크 연결에서, 또는 분산된 시나리오나 트랜잭션된 시나리오에서 작동하는 공급자는 참여한 구성 요소에 실행 시간이 긴 요청의 이벤트에서 제한 시간을 초과하도록 통지하기 위해 이 속성을 지원할 수 있습니다. 데이터 원본 초기화 및 명령 실행에 대한 제한 시간은 계속 각각 DBPROP_INIT_TIMEOUT과 DBPROP_COMMANDTIMEOUT에 의해 결정됩니다.<br /><br /> DBPROP_INIT_GENERALTIMEOUT은 읽기 전용이며, 이를 설정하려고 하면 DBPROPSTATUS_NOTSETTABLE의 *dwstatus* 오류가 반환됩니다.|  
|DBPROP_INIT_HWND|호출 응용 프로그램의 Windows 핸들입니다. 유효한 창 핸들은 초기화 속성 요청이 허용될 때 표시되는 초기화 대화 상자에 필요합니다.|  
|DBPROP_INIT_IMPERSONATION_LEVEL|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 가장 수준 조정을 지원하지 않습니다.<br /><br /> 속성 값을 설정하려고 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환합니다. DBPROP 구조의 *dwStatus* 멤버는 DBPROPSTATUS_NOTSUPPORTED를 나타냅니다.|  
|DBPROP_INIT_LCID|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 로캘 ID의 유효성을 확인하고 로캘 ID가 지원되지 않거나 클라이언트에 설치되어 있지 않은 경우 오류를 반환합니다.|  
|DBPROP_INIT_LOCATION|속성 값을 설정하려고 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환합니다. DBPROP 구조의 *dwStatus* 멤버는 DBPROPSTATUS_NOTSUPPORTED를 나타냅니다.|  
|DBPROP_INIT_MODE|속성 값을 설정하려고 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환합니다. DBPROP 구조의 *dwStatus* 멤버는 DBPROPSTATUS_NOTSUPPORTED를 나타냅니다.|  
|DBPROP_INIT_PROMPT|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 데이터 원본 초기화를 위한 모든 확인 모드를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBPROMPT_NOPROMPT를 속성의 기본 설정으로 사용합니다.|  
|DBPROP_INIT_PROTECTION_LEVEL|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결에 보호 수준을 지원하지 않습니다.<br /><br /> 속성 값을 설정하려고 시도하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환합니다. DBPROP 구조의 *dwStatus* 멤버는 DBPROPSTATUS_NOTSUPPORTED를 나타냅니다.|  
|DBPROP_INIT_PROVIDERSTRING|이 항목의 뒷부분에 나오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 문자열을 참조하십시오.|  
|DBPROP_INIT_TIMEOUT|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 지정된 시간(초) 내에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 설정하지 못할 경우 초기화 시 오류를 반환합니다.|  
  
 공급자별 속성 집합 DBPROPSET_SQLSERVERDBINIT에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 이러한 추가 초기화 속성을 정의 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_AUTH_OLD_PASSWORD|형식: VT_BSTR<br /><br /> R/W: Write<br /><br /> 기본값: VT_EMPTY<br /><br /> 설명: 현재 또는 만료 된 암호입니다. 자세한 내용은 [프로그래밍 방식으로 암호 변경](../../relational-databases/native-client/features/changing-passwords-programmatically.md)합니다.|  
|SSPROP_INIT_APPNAME|형식: VT_BSTR<br /><br /> R/W: 읽기/쓰기<br /><br /> 설명: 클라이언트 응용 프로그램 이름입니다.|  
|SSPROP_INIT_AUTOTRANSLATE|형식: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_TRUE<br /><br /> 설명: OEM/ANSI 문자 변환입니다.<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 클라이언트 코드 페이지와 서버 간의 확장된 문자 일치에서 문제를 최소화 하기 위해-유니코드 변환 하 여 클라이언트와 서버 간에 전송 되는 ANSI 문자 문자열을 변환 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**char**, **varchar**또는 **text** 변수, 매개 변수 또는 열 인스턴스로 전송된 클라이언트 DBTYPE_STR 데이터는 클라이언트 ACP(ANSI 코드 페이지)를 사용하여 문자에서 유니코드로 변환된 후 서버의 ACP를 사용하여 유니코드에서 문자로 변환됩니다.<br /><br /> 클라이언트 DBTYPE_STR 변수로 전송된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char**, **varchar** 또는 **text** 데이터는 서버 ACP를 사용하여 문자에서 유니코드로 변환된 후 클라이언트 ACP를 사용하여 유니코드에서 문자로 변환됩니다.<br /><br /> 이러한 변환은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 의해 클라이언트에서 수행됩니다. 이를 위해서는 서버에 사용된 것과 동일한 ACP를 클라이언트에서 사용할 수 있어야 합니다.<br /><br /> 이러한 설정은 다음 전송에 대해 발생하는 변환에는 영향을 미치지 않습니다.<br /><br /> 서버의 **char**, **varchar** 또는 **text**로 전송된 유니코드 DBTYPE_WSTR 클라이언트 데이터.<br /><br /> 클라이언트의 유니코드 DBTYPE_WSTR 변수에 전송된 **char**, **varchar** 또는 **text** 서버 데이터.<br /><br /> 서버의 유니코드 **nchar**, **nvarchar** 또는 **ntext**로 전송된 ANSI DBTYPE_STR 클라이언트 데이터.<br /><br /> 클라이언트의 ANSI DBTYPE_STR 변수로 전송된 유니코드 **char**, **varchar** 또는 **text** 서버 데이터.<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 문자 변환을 수행 하지 않습니다.<br /><br /> 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 전송 하는 클라이언트 ANSI 문자 DBTYPE_STR 데이터를 변환 하지 않습니다 **char**합니다 **varchar**, 또는 **텍스트** 변수 매개 변수 또는 서버의 열입니다. 서버에서 클라이언트의 DBTYPE_STR 변수로 전송된 **char**, **varchar** 또는 **text** 데이터에 대해 변환이 수행되지 않습니다.<br /><br /> 클라이언트와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 서로 다른 ACP를 사용하는 경우 확장 문자가 잘못 해석될 수 있습니다.|  
|SSPROP_INIT_CURRENTLANGUAGE|형식: VT_BSTR<br /><br /> R/W: 읽기/쓰기<br /><br /> 설명: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어 이름입니다. 시스템 메시지 선택 및 서식 지정에 사용되는 언어를 식별합니다. 언어는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행 중인 컴퓨터에 설치되어 있어야 하며 그렇지 않은 경우 데이터 원본 초기화가 실패합니다.|  
|SSPROP_INIT_DATATYPECOMPATIBILITY|형식: VT_UI2<br /><br /> R/W: 읽기/쓰기<br /><br /> 기본값: 0<br /><br /> 설명: 간의 데이터 형식이 호환 되도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 데이터 개체 (ADO (ActiveX) 응용 프로그램입니다. 기본값인 0을 사용할 경우 공급자에서 사용되는 데이터 형식 처리가 기본 데이터 형식 처리가 됩니다. 값에 80을 사용하면 데이터 형식 처리는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 데이터 형식만 사용합니다. 자세한 내용은 [SQL Server Native Client를 사용 하 여 ADO를 사용 하 여](../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)입니다.|  
|SSPROP_INIT_ENCRYPT|형식: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 네트워크를 통해 이동 하는 데이터를 암호화 하려면 위해 SSPROP_INIT_ENCRYPT 속성이 VARIANT_TRUE로 설정 됩니다.<br /><br /> 프로토콜 암호화 사용이 설정된 경우 SSPROP_INIT_ENCRYPT 설정에 관계없이 항상 암호화가 수행됩니다. 프로토콜 암호화 사용이 해제되고 SSPROP_INIT_ENCRYPT가 VARIANT_TRUE로 설정된 경우 암호화가 수행됩니다.<br /><br /> 프로토콜 암호화 사용이 해제되고 SSPROP_INIT_ENCRYPT가 VARIANT_FALSE로 설정된 경우 암호화가 수행되지 않습니다.|  
|SSPROP_INIT_FAILOVERPARTNER|형식: VT_BSTR<br /><br /> R/W: 읽기/쓰기<br /><br /> 설명: 데이터베이스 미러링에 대 한 장애 조치 파트너의 이름을 지정합니다. 이는 초기화 속성이며 초기화 전에만 설정할 수 있습니다. 초기화 후에는 주 서버에 의해 반환된 장애 조치(Failover) 파트너가 있는 경우 이를 반환합니다.<br /><br /> 이를 통해 지능형 응용 프로그램은 가장 최근에 확인된 백업 서버를 캐시할 수 있지만 이러한 응용 프로그램은 연결이 처음 설정될 때(또는 풀링된 경우 다시 설정될 때)만 정보가 업데이트되므로 장시간 연결에서는 정보가 최신 상태가 아닐 수 있음을 인식해야 합니다.<br /><br /> 연결을 설정한 후 응용 프로그램은 이 특성을 쿼리하여 장애 조치(Failover) 파트너의 ID를 확인할 수 있습니다. 주 서버에 장애 조치(failover) 파트너가 없는 경우 이 속성은 빈 문자열을 반환합니다. 자세한 내용은 [데이터베이스 미러링 사용](../../relational-databases/native-client/features/using-database-mirroring.md)을 참조하세요.|  
|SSPROP_INIT_FILENAME|형식: VT_BSTR<br /><br /> R/W: 읽기/쓰기<br /><br /> 설명: 연결할 수 있는 데이터베이스의 주 파일 이름을 지정합니다. 이 데이터베이스는 연결되어 해당 연결에 대한 기본 데이터베이스가 됩니다. SSPROP_INIT_FILENAME을 사용하려면 데이터베이스 이름을 DBPROP_INIT_CATALOG 초기화 속성의 값으로 지정해야 합니다. 데이터베이스 이름이 없으면 SSPROP_INIT_FILENAME에 지정된 주 파일 이름을 찾고 해당 데이터베이스를 DBPROP_INIT_CATALOG에 지정된 이름에 연결합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이를 다시 연결하지 않습니다.|  
|SSPROP_INIT_MARSCONNECTION|형식: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 연결에 대 한 여러 활성 결과 집합 (MARS)은 사용할 수 있는지를 지정 합니다. 데이터베이스에 연결을 설정하기 전에 이 옵션을 true로 설정해야 합니다. 자세한 내용은 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)을 참조하세요.|  
|SSPROP_INIT_NETWORKADDRESS|형식: VT_BSTR<br /><br /> R/W: 읽기/쓰기<br /><br /> 설명: 인스턴스를 실행 하는 서버 네트워크 주소의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_INIT_DATASOURCE 속성으로 지정 합니다.|  
|SSPROP_INIT_NETWORKLIBRARY|형식: VT_BSTR<br /><br /> R/W: 읽기/쓰기<br /><br /> 설명: 인스턴스와 통신 하는 데 사용 되는 networklibrary (DLL)의 이름을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. 이름에는 경로 또는 .dll 파일 확장명이 포함되면 안 됩니다.<br /><br /> 기본값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 구성 유틸리티를 사용하여 사용자 지정할 수 있습니다.<br /><br /> 참고: TCP 및 명명 된 파이프가이 속성에 의해 지원 됩니다. 이 속성은 내부적으로 접두사를 생성하는 데 사용되므로 이 속성을 접두사와 함께 사용하는 경우 이중 접두사로 인해 오류가 발생합니다.|  
|SSPROP_INIT_PACKETSIZE|형식: VT_I4<br /><br /> R/W: 읽기/쓰기<br /><br /> 설명: 네트워크 패킷 크기 (바이트)에서입니다. 패킷 크기 속성 값은 512에서 32,767 사이여야 합니다. 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 네트워크 패킷 크기는 4,096입니다.|  
|SSPROP_INIT_TAGCOLUMNCOLLATION|형식: BOOL<br /><br /> R/W: Write<br /><br /> 기본값: FALSE<br /><br /> 설명: 서버 쪽 커서를 사용 하는 경우 데이터베이스 업데이트 동안 사용 됩니다. 이 속성은 클라이언트의 코드 페이지가 아닌 서버에서 얻은 데이터 정렬 정보를 데이터에 첨부합니다. 현재 이 속성은 대상 데이터의 데이터 정렬을 알고 이를 올바르게 변환하는 분산 쿼리 처리에서만 사용됩니다.|  
|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|형식: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 서버 인증서 유효성 검사를 사용 하지 않도록 설정 하거나 사용 하는 데 사용 합니다. 이 속성은 읽기/쓰기이지만 연결이 설정된 후에 이 속성을 설정하려고 하면 오류가 발생합니다.<br /><br /> 인증서 유효성 검사가 필요하도록 클라이언트가 구성된 경우 이 속성은 무시됩니다. 그러나 응용 프로그램에서 이 속성을 SSPROP_INIT_ENCRYPT와 함께 사용하면 클라이언트가 암호화를 요구하지 않도록 구성되고 클라이언트에 제공된 인증서가 없는 경우에도 서버에 대한 연결이 암호화되도록 보장할 수 있습니다.<br /><br /> 클라이언트 응용 프로그램은 연결이 열린 후에 이 속성을 쿼리하여 실제 사용되는 암호화 및 유효성 검사 설정을 확인할 수 있습니다.<br /><br /> 참고: 인증서 유효성 검사 없이 암호화를 사용 하 여 패킷 스니핑에 대 한 부분적인 보호가 제공 하지만 중간자 개입 공격 으로부터 보호 되지 않습니다. 서버 인증서 유효성을 검사하지 않고 단순히 로그인과 서버로 전송되는 데이터의 암호화만 허용합니다.<br /><br /> 자세한 내용은 [유효성 검사 없이 암호화 사용](../../relational-databases/native-client/features/using-encryption-without-validation.md)을 참조하세요.|  
|SSPROP_INIT_USEPROCFORPREP|형식: VT_I4<br /><br /> R/W: 읽기/쓰기<br /><br /> 기본값: SSPROPVAL_USEPROCFORPREP_ON<br /><br /> 설명: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저 사용법입니다. **ICommandPrepare** 인터페이스를 지원하기 위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 임시 저장 프로시저 사용을 정의합니다. 이 속성은 SQL Server 6.5에 연결하는 경우에만 의미가 있었습니다. 이후 버전에서는 이 속성이 무시됩니다.<br /><br /> SSPROPVAL_USEPROCFORPREP_OFF: 명령이 준비 될 때 임시 저장된 프로시저가 만들어지지 않습니다.<br /><br /> SSPROPVAL_USEPROCFORPREP_ON: 명령이 준비 될 때 임시 저장된 프로시저가 생성 됩니다. 임시 저장 프로시저는 세션이 해제될 때 삭제됩니다.<br /><br /> SSPROPVAL_USEPROCFORPREP_ON_DROP: 명령이 준비 될 때 임시 저장된 프로시저가 생성 됩니다. 이 프로시저는 **ICommandPrepare::Unprepare**로 명령이 준비 취소될 때, **ICommandText::SetCommandText**로 명령 개체에 대해 새 명령이 지정될 때, 또는 명령을 참조하는 모든 애플리케이션이 해제될 때 삭제됩니다.|  
|SSPROP_INIT_WSID|형식: VT_BSTR<br /><br /> R/W: 읽기/쓰기<br /><br /> 설명: 워크스테이션을 식별하는 문자열입니다.|  
  
 공급자별 속성 집합 DBPROPSET_SQLSERVERDATASOURCEINFO에서 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 추가 속성을 정의 참조 하세요 [데이터 원본 정보 속성](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md) 자세한 합니다.  
  
## <a name="the-sql-server-native-client-ole-db-provider-string"></a>SQL Server Native Client OLE DB 공급자 문자열  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 공급자 문자열 속성 값에서 ODBC 유사 구문을 인식합니다. 공급자 문자열 속성은 OLE DB 데이터 원본에 대한 연결이 설정될 때 OLE DB 초기화 속성 DBPROP_INIT_PROVIDERSTRING의 값으로 제공됩니다. 이 속성은 OLE DB 데이터 원본에 대한 연결을 구현하기 위해 필요한 OLE DB 공급자별 연결 데이터를 지정합니다. 문자열 내에서 요소는 세미콜론으로 구분됩니다. 문자열의 마지막 요소는 세미콜론으로 끝나야 합니다. 각 요소는 키워드, 등호 문자, 그리고 초기화 시 전달되는 값으로 구성됩니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
Server=MyServer;UID=MyUserName;  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하면 소비자는 공급자 문자열 속성을 사용할 필요가 없습니다. 소비자는 OLE DB 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자별 초기화 속성을 사용하여 공급자 문자열에 반영된 모든 초기화 속성을 설정할 수 있습니다.  
  
 사용할 수 있는 키워드 목록은 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 참조 하세요 [SQL Server Native Client를 사용 하 여 연결 문자열 키워드를 사용 하 여](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)입니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 개체 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
