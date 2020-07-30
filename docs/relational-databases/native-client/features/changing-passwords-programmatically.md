---
title: 프로그래밍 방식으로 암호 변경 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 13d0e51b7b06acdfbe847976d093765203b51638
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245801"
---
# <a name="changing-sql-server-native-client-passwords-programmatically"></a>프로그래밍 방식으로 SQL Server Native Client 암호 변경
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전에는 사용자 암호가 만료될 때 관리자만 암호를 다시 설정할 수 있었습니다. 부터 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client OLE DB 공급자와 native client ODBC 드라이버를 통해 프로그래밍 방식으로 암호 만료를 처리 하 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고 **SQL Server 로그인** 대화 상자를 변경 하는 것을 지원 합니다.  
  
> [!NOTE]  
>  가능한 경우 런타임에 자격 증명을 입력하라는 메시지를 사용자에게 표시하고 해당 자격 증명을 지속형 형식으로 저장하지 마십시오. 자격 증명을 저장해야 하는 경우 [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 암호화해야 합니다. 암호 사용에 대한 자세한 내용은 [강력한 암호](../../../relational-databases/security/strong-passwords.md)를 참조하세요.  
  
## <a name="sql-server-login-error-codes"></a>SQL Server 로그인 오류 코드  
 인증 문제로 인해 연결할 수 없는 경우 분석 및 검색 지원을 위해 애플리케이션에서 다음 SQL Server 오류 코드 중 하나를 사용할 수 있습니다.  
  
|SQL Server 오류 코드|오류 메시지|  
|---------------------------|-------------------|  
|15113|사용자 '%. * l s '이 (가) 로그인 하지 못했습니다. 이유: 암호 유효성 검사에 실패 했습니다. 계정이 잠겼습니다.|  
|18463|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 지금은 암호를 사용할 수 없습니다.|  
|18464|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 너무 짧아서 정책 요구 사항에 맞지 않습니다.|  
|18465|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 너무 길어서 정책 요구 사항에 맞지 않습니다.|  
|18466|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 복잡하지 않기 때문에 정책 요구 사항에 맞지 않습니다.|  
|18467|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 암호 필터 DLL의 요구 사항에 맞지 않습니다.|  
|18468|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호 유효성 검사 중에 오류가 발생했습니다.|  
|18487|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 계정의 암호가 만료되었습니다.|  
|18488|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 계정의 암호를 변경해야 합니다.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 사용자 인터페이스를 통해 또는 프로그래밍 방식으로 암호 만료를 지원 합니다.  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB 사용자 인터페이스 암호 만료  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 **SQL Server 로그인** 대화 상자에 대 한 변경 내용을 통해 암호 만료를 지원 합니다. DBPROP_INIT_PROMPT 값을 DBPROMPT_NOPROMPT로 설정하면 암호가 만료할 경우 초기 연결 시도가 실패합니다.  
  
 DBPROP_INIT_PROMPT를 다른 값으로 설정하면 암호 만료 여부에 관계없이 사용자에게 **SQL Server 로그인** 대화 상자가 표시됩니다. 사용자는 **옵션** 단추를 클릭하고 **암호 변경**을 선택하여 암호를 변경할 수 있습니다.  
  
 사용자가 확인을 클릭하면 암호가 만료된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 **SQL Server 암호 변경** 대화 상자를 사용하여 새 암호를 입력하고 확인하라는 메시지를 사용자에게 표시합니다.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB 프롬프트 동작 및 잠긴 계정  
 계정이 잠겨 연결 시도가 실패할 수 있습니다. **SQL Server 로그인** 대화 상자가 표시된 후 이 문제가 발생하면 서버 오류 메시지가 사용자에게 표시되고 연결 시도가 중단됩니다. 사용자가 이전 암호에 잘못된 값을 입력하면 **SQL Server 암호 변경** 대화 상자가 표시된 후에도 이 문제가 발생할 수 있습니다. 이 경우 동일한 오류 메시지가 표시되고 연결 시도가 중단됩니다.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB 연결 풀링, 암호 만료 및 잠긴 계정  
 연결 풀에서 연결이 활성화되어 있는 동안 계정이 잠기거나 해당 암호가 만료될 수 있습니다. 서버는 두 가지 경우에서 만료된 암호와 잠긴 계정을 확인합니다. 첫 번째는 연결을 처음 만들 때입니다. 두 번째 경우는 연결을 다시 설정하여 연결이 풀에서 제거될 때입니다.  
  
 다시 설정 시도가 실패하면 풀에서 연결이 제거되고 오류가 반환됩니다.  
  
### <a name="ole-db-programmatic-password-expiration"></a>OLE DB 프로그래밍 방식 암호 만료  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 DBPROPSET_SQLSERVERDBINIT 속성 집합에 추가 된 SSPROP_AUTH_OLD_PASSWORD (유형 VT_BSTR) 속성을 추가 하 여 암호 만료를 지원 합니다.  
  
 기존 "암호" 속성은 DBPROP_AUTH_PASSWORD를 참조하며 새 암호를 저장하는 데 사용됩니다.  
  
> [!NOTE]  
>  연결 문자열에서 "이전 암호" 속성은 공급자 문자열 속성을 통해 사용할 수 없는 현재(만료된) 암호인 SSPROP_AUTH_OLD_PASSWORD를 설정합니다.  
  
 공급자는 이 속성 값을 저장하지 않습니다. 이 속성을 설정하면 새 연결이 발생하기 때문에 공급자가 첫 번째 연결의 연결 풀을 사용하지 않습니다. 암호 변경에 성공하면 현재 연결을 다시 사용할 수 없습니다. 암호 변경 후 유효하지 않은 이전 암호가 현재 연결에 포함되어 있기 때문입니다. 또한 로그인에 성공하면 공급자는 이 속성을 지웁니다. 이후에 이전 암호를 검색하려고 하면 VT_EMPTY가 반환됩니다.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD는 암호가 만료된 경우에만 사용되기 때문에 저장하면 안 됩니다.  
  
 "이전 암호" 속성을 설정할 때마다 공급자는 Windows 인증도 지정되어 항상 우선 적용되지 않는 경우 암호 변경이 시도되고 있다고 가정합니다.  
  
 Windows 인증이 사용되는 경우 이전 암호를 지정하면 이전 암호가 REQUIRED 또는 OPTIONAL로 지정되었는지에 따라 각각 DB_E_ERRORSOCCURRED 또는 DB_S_ERRORSOCCURRED가 발생하고, DBPROPSTATUS_CONFLICTINGBADVALUE의 상태 값이 *dwStatus*에 반환됩니다. 이 값은 **IDBInitialize::Initialize**를 호출할 때 검색됩니다.  
  
 암호 변경 시도가 예기치 않게 실패하는 경우 서버에서 오류 코드 18468을 반환합니다. 연결 시도에서 표준 OLEDB 오류가 반환됩니다.  
  
 DBPROPSET_SQLSERVERDBINIT 속성 집합에 대한 자세한 정보는 p[초기화 및 권한 부여 속성](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)을 참조하세요.  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 사용자 인터페이스를 통해 또는 프로그래밍 방식으로 암호 만료를 지원 합니다.  
  
### <a name="odbc-user-interface-password-expiration"></a>ODBC 사용자 인터페이스 암호 만료  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 **SQL Server 로그인** 대화 상자에 대 한 변경 내용을 통해 암호 만료를 지원 합니다.  
  
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 이 호출 되 고 **drivercompletion** 값이 SQL_DRIVER_NOPROMPT로 설정 된 경우 암호가 만료 되 면 초기 연결 시도가 실패 합니다. SQLSTATE 값 28000 및 네이티브 오류 코드 값 18487은 **SQLError** 또는 **SQLGetDiagRec**에 대 한 후속 호출에서 반환 됩니다.  
  
 **Drivercompletion** 가 다른 값으로 설정 된 경우 암호가 만료 되었는지 여부에 관계 없이 사용자에 게 **SQL Server 로그인** 대화 상자가 표시 됩니다. 사용자는 **옵션** 단추를 클릭하고 **암호 변경**을 선택하여 암호를 변경할 수 있습니다.  
  
 사용자가 확인을 클릭 하 고 암호가 만료 되 면에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **암호 SQL Server 변경** 대화 상자를 사용 하 여 새 암호를 입력 하 고 확인 하 라는 메시지를 표시 합니다.  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>ODBC 프롬프트 동작 및 잠긴 계정  
 계정이 잠겨 연결 시도가 실패할 수 있습니다. **SQL Server 로그인** 대화 상자가 표시된 후 이 문제가 발생하면 서버 오류 메시지가 사용자에게 표시되고 연결 시도가 중단됩니다. 사용자가 이전 암호에 잘못된 값을 입력하면 **SQL Server 암호 변경** 대화 상자가 표시된 후에도 이 문제가 발생할 수 있습니다. 이 경우 동일한 오류 메시지가 표시되고 연결 시도가 중단됩니다.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>ODBC 연결 풀링, 암호 만료 및 잠긴 계정  
 연결 풀에서 연결이 활성화되어 있는 동안 계정이 잠기거나 해당 암호가 만료될 수 있습니다. 서버는 두 가지 경우에서 만료된 암호와 잠긴 계정을 확인합니다. 첫 번째는 연결을 처음 만들 때입니다. 두 번째 경우는 연결을 다시 설정하여 연결이 풀에서 제거될 때입니다.  
  
 다시 설정 시도가 실패하면 풀에서 연결이 제거되고 오류가 반환됩니다.  
  
### <a name="odbc-programmatic-password-expiration"></a>ODBC 프로그래밍 방식 암호 만료  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 함수를 사용 하 여 서버에 연결 하기 전에 설정 된 SQL_COPT_SS_OLDPWD 특성을 추가 하 여 암호 만료를 지원 합니다.  
  
 연결 핸들의 SQL_COPT_SS_OLDPWD 특성은 만료된 암호를 참조합니다. 연결 풀링에 방해가 되므로 이 특성에 대한 연결 문자열 특성은 없습니다. 로그인에 성공하면 드라이버가 이 특성을 지웁니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는이 기능에 대해 암호 만료, 암호 정책 충돌, 계정 잠금 및 Windows 인증을 사용 하는 동안 이전 암호 속성이 설정 된 경우의 네 가지 경우에 SQL_ERROR를 반환 합니다. [SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md) 가 호출 되 면 드라이버는 사용자에 게 적절 한 오류 메시지를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
