---
title: 프로그래밍 방식으로 암호 변경 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bd7d14e180a44f974e4d6ba89421caa8cbba3535
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32954708"
---
# <a name="changing-passwords-programmatically"></a>프로그래밍 방식으로 암호 변경
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전에는 사용자 암호가 만료될 때 관리자만 암호를 다시 설정할 수 있었습니다. 부터는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 지원을 통해 프로그래밍 방식의 암호 만료 처리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 변경을 통해는 **SQL Server 로그인** 대화 상자.  
  
> [!NOTE]  
>  가능한 경우 런타임에 자격 증명을 입력하라는 메시지를 사용자에게 표시하고 해당 자격 증명을 지속형 형식으로 저장하지 마십시오. 유지 해야 하는 자격 증명을 암호화 해야 하를 사용 하 여 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)합니다. 암호의 사용에 대 한 자세한 내용은 참조 [Strong Passwords](../../../relational-databases/security/strong-passwords.md)합니다.  
  
## <a name="sql-server-login-error-codes"></a>SQL Server 로그인 오류 코드  
 인증 문제로 인해 연결할 수 없는 경우 분석 및 검색 지원을 위해 응용 프로그램에서 다음 SQL Server 오류 코드 중 하나를 사용할 수 있습니다.  
  
|SQL Server 오류 코드|오류 메시지|  
|---------------------------|-------------------|  
|15113|사용자에 대 한 로그인 하지 못했습니다. ' %. * l s 원인: 암호 유효성 검사가 실패 했습니다. 계정이 잠겼습니다.|  
|18463|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 지금은 암호를 사용할 수 없습니다.|  
|18464|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 너무 짧아서 정책 요구 사항에 맞지 않습니다.|  
|18465|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 너무 길어서 정책 요구 사항에 맞지 않습니다.|  
|18466|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 복잡하지 않기 때문에 정책 요구 사항에 맞지 않습니다.|  
|18467|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 암호 필터 DLL의 요구 사항에 맞지 않습니다.|  
|18468|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호 유효성 검사 중에 오류가 발생했습니다.|  
|18487|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 계정의 암호가 만료 되었습니다.|  
|18488|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 계정의 암호를 변경 해야 합니다.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 있지만 사용자 인터페이스 암호 만료를 지원 및 프로그래밍 방식으로 합니다.  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB 사용자 인터페이스 암호 만료  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 변경 내용을 통해 암호 만료를 지원는 **SQL Server 로그인** 대화 상자. DBPROP_INIT_PROMPT 값을 DBPROMPT_NOPROMPT로 설정하면 암호가 만료할 경우 초기 연결 시도가 실패합니다.  
  
 사용자에 게 DBPROP_INIT_PROMPT를 다른 값으로 설정 되어가 **SQL Server 로그인** 암호가 만료 된 여부에 관계 없이 대화 상자에서. 사용자가 클릭할 수는 **옵션** 단추 및 확인 **암호 변경** 암호를 변경 합니다.  
  
 사용자가 확인을 클릭 하 고 암호가 만료 된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 입력 하 고 사용 하 여 새 암호를 확인 하 라는 메시지는 **SQL Server 암호 변경** 대화 상자.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB 프롬프트 동작 및 잠긴 계정  
 계정이 잠겨 연결 시도가 실패할 수 있습니다. 표시 된 후이 문제가 발생 된 **SQL Server 로그인** 대화 상자에서 서버 오류 메시지가 사용자에 게 표시 되 고 연결 시도가 중단 됩니다. 표시 된도 발생할 수 있습니다는 **SQL Server 암호 변경** 대화 상자 사용자가 이전 암호에 대 한 잘못 된 값을 입력 합니다. 이 경우 동일한 오류 메시지가 표시되고 연결 시도가 중단됩니다.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB 연결 풀링, 암호 만료 및 잠긴 계정  
 연결 풀에서 연결이 활성화되어 있는 동안 계정이 잠기거나 해당 암호가 만료될 수 있습니다. 서버는 두 가지 경우에서 만료된 암호와 잠긴 계정을 확인합니다. 첫 번째는 연결을 처음 만들 때입니다. 두 번째 경우는 연결을 다시 설정하여 연결이 풀에서 제거될 때입니다.  
  
 다시 설정 시도가 실패하면 풀에서 연결이 제거되고 오류가 반환됩니다.  
  
### <a name="ole-db-programmatic-password-expiration"></a>OLE DB 프로그래밍 방식 암호 만료  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBPROPSET_SQLSERVERDBINIT 속성 집합에 추가 된 SSPROP_AUTH_OLD_PASSWORD (VT_BSTR 유형) 속성의 추가 통해 암호 만료를 지원 합니다.  
  
 기존 "암호" 속성은 DBPROP_AUTH_PASSWORD를 참조하며 새 암호를 저장하는 데 사용됩니다.  
  
> [!NOTE]  
>  연결 문자열에서 "이전 암호" 속성은 공급자 문자열 속성을 통해 사용할 수 없는 현재(만료된) 암호인 SSPROP_AUTH_OLD_PASSWORD를 설정합니다.  
  
 공급자는 이 속성 값을 저장하지 않습니다. 이 속성을 설정하면 새 연결이 발생하기 때문에 공급자가 첫 번째 연결의 연결 풀을 사용하지 않습니다. 암호 변경에 성공하면 현재 연결을 다시 사용할 수 없습니다. 암호 변경 후 유효하지 않은 이전 암호가 현재 연결에 포함되어 있기 때문입니다. 또한 로그인에 성공하면 공급자는 이 속성을 지웁니다. 이후에 이전 암호를 검색하려고 하면 VT_EMPTY가 반환됩니다.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD는 암호가 만료된 경우에만 사용되기 때문에 저장하면 안 됩니다.  
  
 "이전 암호" 속성을 설정할 때마다 공급자는 Windows 인증도 지정되어 항상 우선 적용되지 않는 경우 암호 변경이 시도되고 있다고 가정합니다.  
  
 Windows 인증을 사용 하는 경우 DB_E_ERRORSOCCURRED 또는 db_s_errorsoccurred가 이전 암호 지정 여부 REQUIRED 또는 OPTIONAL로 각각 및 DBPROPSTATUS_의 상태 값에 따라 결과 이전 암호를 지정 CONFLICTINGBADVALUE에 반환 된 *dwStatus*합니다. 이 검색 될 때 **idbinitialize:: Initialize** 호출 됩니다.  
  
 암호 변경 시도가 예기치 않게 실패하는 경우 서버에서 오류 코드 18468을 반환합니다. 연결 시도에서 표준 OLEDB 오류가 반환됩니다.  
  
 DBPROPSET_SQLSERVERDBINIT 속성 집합에 대 한 자세한 내용은 참조 [초기화 및 권한 부여 속성](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)합니다.  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 있지만 사용자 인터페이스 암호 만료를 지원 및 프로그래밍 방식으로 합니다.  
  
### <a name="odbc-user-interface-password-expiration"></a>ODBC 사용자 인터페이스 암호 만료  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 변경 내용을 통해 암호 만료를 지원는 **SQL Server 로그인** 대화 상자.  
  
 경우 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 라고의 값과 **DriverCompletion** 암호가 만료 된 경우 초기 연결 시도가 실패 SQL_DRIVER_NOPROMPT로 설정 됩니다. SQLSTATE 값 28000과 원시 오류 코드 값 18487에 대 한 후속 호출에서 반환될지 **SQLError** 또는 **SQLGetDiagRec**합니다.  
  
 경우 **DriverCompletion** 설정한 다른 값으로 사용자에 게는 **SQL Server 로그인** 암호가 만료 된 여부에 관계 없이 대화 상자. 사용자가 클릭할 수는 **옵션** 단추 및 확인 **암호 변경** 암호를 변경 합니다.  
  
 사용자가 확인을 클릭 하 고 암호가 만료 된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 입력 하 고 사용 하 여 새 암호를 확인 하는 프롬프트는 **SQL Server 암호 변경** 대화 상자.  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>ODBC 프롬프트 동작 및 잠긴 계정  
 계정이 잠겨 연결 시도가 실패할 수 있습니다. 표시 된 후이 문제가 발생 된 **SQL Server 로그인** 대화 상자에서 서버 오류 메시지가 사용자에 게 표시 되 고 연결 시도가 중단 됩니다. 표시 된도 발생할 수 있습니다는 **SQL Server 암호 변경** 대화 상자 사용자가 이전 암호에 대 한 잘못 된 값을 입력 합니다. 이 경우 동일한 오류 메시지가 표시되고 연결 시도가 중단됩니다.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>ODBC 연결 풀링, 암호 만료 및 잠긴 계정  
 연결 풀에서 연결이 활성화되어 있는 동안 계정이 잠기거나 해당 암호가 만료될 수 있습니다. 서버는 두 가지 경우에서 만료된 암호와 잠긴 계정을 확인합니다. 첫 번째는 연결을 처음 만들 때입니다. 두 번째 경우는 연결을 다시 설정하여 연결이 풀에서 제거될 때입니다.  
  
 다시 설정 시도가 실패하면 풀에서 연결이 제거되고 오류가 반환됩니다.  
  
### <a name="odbc-programmatic-password-expiration"></a>ODBC 프로그래밍 방식 암호 만료  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 SQL_COPT_SS_OLDPWD 특성을 사용 하 여 서버에 연결 하기 전에 설정의 추가 통해 암호 만료를 지원 합니다.는 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 함수입니다.  
  
 연결 핸들의 SQL_COPT_SS_OLDPWD 특성은 만료된 암호를 참조합니다. 연결 풀링에 방해가 되므로 이 특성에 대한 연결 문자열 특성은 없습니다. 로그인에 성공하면 드라이버가 이 특성을 지웁니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는이 기능에 대 한 네 경우에서 SQL_ERROR를 반환: 암호 만료, 암호 정책 충돌, 계정 잠금 및 Windows 인증을 사용 하는 동안 이전 암호 속성이 설정 된 경우. 사용자에 게 해당 오류 메시지를 반환 하는 드라이버 때 [SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md) 가 호출 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
