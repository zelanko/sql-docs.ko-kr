---
title: 프로그래밍 방식으로 암호 변경 | Microsoft Docs
description: 프로그래밍 방식으로 OLE DB 드라이버를 사용 하 여 SQL Server에 대 한 암호를 변경 합니다.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], password expiration
- OLE DB Driver for SQL Server, passwords
- passwords [SQL Server], expiration
- MSOLEDBSQL, password expiration
- expiration [OLE DB Driver for SQL Server]
- passwords [SQL Server], modifying
- expired passwords [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, password expiration
- modifying passwords
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 89d674e075e8a05697328f60c6bb47a40e82ebf9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775437"
---
# <a name="changing-passwords-programmatically"></a>프로그래밍 방식으로 암호 변경
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전에는 사용자 암호가 만료될 때 관리자만 암호를 다시 설정할 수 있었습니다. 부터는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], OLE DB Driver for SQL Server 지원 변경 내용 및 OLE DB 드라이버를 통해 프로그래밍 방식으로 암호 만료를 처리 합니다 **SQL Server 로그인** 대화 상자.  
  
> [!NOTE]  
>  가능한 경우 런타임에 자격 증명을 입력하라는 메시지를 사용자에게 표시하고 해당 자격 증명을 지속형 형식으로 저장하지 마십시오. 자격 증명을 저장해야 하는 경우 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 암호화해야 합니다. 암호 사용에 대한 자세한 내용은 [강력한 암호](../../../relational-databases/security/strong-passwords.md)를 참조하세요.  
  
## <a name="sql-server-login-error-codes"></a>SQL Server 로그인 오류 코드  
 인증 문제로 인해 연결할 수 없는 경우 분석 및 검색 지원을 위해 응용 프로그램에서 다음 SQL Server 오류 코드 중 하나를 사용할 수 있습니다.  
  
|SQL Server 오류 코드|오류 메시지|  
|---------------------------|-------------------|  
|15113|사용자가 로그인 하지 못했습니다 ' %. * l s 이유: 암호 유효성 검사가 실패 했습니다. 계정이 잠겼습니다.|  
|18463|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 지금은 암호를 사용할 수 없습니다.|  
|18464|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 너무 짧아서 정책 요구 사항에 맞지 않습니다.|  
|18465|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 너무 길어서 정책 요구 사항에 맞지 않습니다.|  
|18466|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 복잡하지 않기 때문에 정책 요구 사항에 맞지 않습니다.|  
|18467|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호가 암호 필터 DLL의 요구 사항에 맞지 않습니다.|  
|18468|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 암호를 변경하지 못했습니다. 암호 유효성 검사 중에 오류가 발생했습니다.|  
|18487|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 계정의 암호가 만료되었습니다.|  
|18488|사용자 '%.*ls'이(가) 로그인하지 못했습니다. 원인: 계정의 암호를 변경해야 합니다.|  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버  
 OLE DB Driver for SQL Server 사용자 인터페이스를 통해 암호 만료를 지원 하 고 프로그래밍 방식으로 합니다.  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB 사용자 인터페이스 암호 만료  
 SQL Server용 OLE DB 드라이버는 **SQL Server 로그인** 대화 상자의 변경 내용을 통해 암호 만료를 지원합니다. DBPROP_INIT_PROMPT 값을 DBPROMPT_NOPROMPT로 설정하면 암호가 만료할 경우 초기 연결 시도가 실패합니다.  
  
 DBPROP_INIT_PROMPT를 다른 값으로 설정하면 암호 만료 여부에 관계없이 사용자에게 **SQL Server 로그인** 대화 상자가 표시됩니다. 사용자는 **옵션** 단추를 클릭하고 **암호 변경**을 선택하여 암호를 변경할 수 있습니다.  
  
 사용자가 확인을 클릭하면 암호가 만료된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 **SQL Server 암호 변경** 대화 상자를 사용하여 새 암호를 입력하고 확인하라는 메시지를 사용자에게 표시합니다.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB 프롬프트 동작 및 잠긴 계정  
 계정이 잠겨 연결 시도가 실패할 수 있습니다. **SQL Server 로그인** 대화 상자가 표시된 후 이 문제가 발생하면 서버 오류 메시지가 사용자에게 표시되고 연결 시도가 중단됩니다. 사용자가 이전 암호에 잘못된 값을 입력하면 **SQL Server 암호 변경** 대화 상자가 표시된 후에도 이 문제가 발생할 수 있습니다. 이 경우 동일한 오류 메시지가 표시되고 연결 시도가 중단됩니다.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB 연결 풀링, 암호 만료 및 잠긴 계정  
 연결 풀에서 연결이 활성화되어 있는 동안 계정이 잠기거나 해당 암호가 만료될 수 있습니다. 서버는 두 가지 경우에서 만료된 암호와 잠긴 계정을 확인합니다. 첫 번째는 연결을 처음 만들 때입니다. 두 번째 경우는 연결을 다시 설정하여 연결이 풀에서 제거될 때입니다.  
  
 다시 설정 시도가 실패하면 풀에서 연결이 제거되고 오류가 반환됩니다.  
  
### <a name="ole-db-programmatic-password-expiration"></a>OLE DB 프로그래밍 방식 암호 만료  
 SQL Server용 OLE DB 드라이버는 DBPROPSET_SQLSERVERDBINIT 속성 집합에 추가된 SSPROP_AUTH_OLD_PASSWORD(VT_BSTR 유형) 속성을 추가하여 암호 만료를 지원합니다.  
  
 기존 "암호" 속성은 DBPROP_AUTH_PASSWORD를 참조하며 새 암호를 저장하는 데 사용됩니다.  
  
> [!NOTE]  
>  연결 문자열에서 "이전 암호" 속성은 공급자 문자열 속성을 통해 사용할 수 없는 현재(만료된) 암호인 SSPROP_AUTH_OLD_PASSWORD를 설정합니다.  
  
 공급자는 이 속성 값을 저장하지 않습니다. 이 속성을 설정하면 새 연결이 발생하기 때문에 공급자가 첫 번째 연결의 연결 풀을 사용하지 않습니다. 암호 변경에 성공하면 현재 연결을 다시 사용할 수 없습니다. 암호 변경 후 유효하지 않은 이전 암호가 현재 연결에 포함되어 있기 때문입니다. 또한 로그인에 성공하면 공급자는 이 속성을 지웁니다. 이후에 이전 암호를 검색하려고 하면 VT_EMPTY가 반환됩니다.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD는 암호가 만료된 경우에만 사용되기 때문에 저장하면 안 됩니다.  
  
 "이전 암호" 속성을 설정할 때마다 공급자는 Windows 인증도 지정되어 항상 우선 적용되지 않는 경우 암호 변경이 시도되고 있다고 가정합니다.  
  
 Windows 인증이 사용되는 경우 이전 암호를 지정하면 이전 암호가 REQUIRED 또는 OPTIONAL로 지정되었는지에 따라 각각 DB_E_ERRORSOCCURRED 또는 DB_S_ERRORSOCCURRED가 발생하고, DBPROPSTATUS_CONFLICTINGBADVALUE의 상태 값이 *dwStatus*에 반환됩니다. 이 값은 **IDBInitialize::Initialize**를 호출할 때 검색됩니다.  
  
 암호 변경 시도가 예기치 않게 실패하는 경우 서버에서 오류 코드 18468을 반환합니다. 연결 시도에서 표준 OLEDB 오류가 반환됩니다.  
  
 DBPROPSET_SQLSERVERDBINIT 속성 집합에 대 한 자세한 내용은 참조 하세요. [초기화 및 권한 부여 속성](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)합니다.  

  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
