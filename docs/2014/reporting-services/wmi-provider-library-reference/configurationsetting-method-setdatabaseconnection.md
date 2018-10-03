---
title: SetDatabaseConnection 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 68907320922f0181521a9ff30de708f660e8dd8c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207103"
---
# <a name="setdatabaseconnection-method-wmi-msreportserverconfigurationsetting"></a>SetDatabaseConnection 메서드(WMI MSReportServer_ConfigurationSetting)
  특정 보고서 서버 데이터베이스에 대한 보고서 서버 데이터베이스 연결을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *Server*  
 보고서 서버 데이터베이스를 호스트하는 데 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.  
  
 *DatabaseName*  
 보고서 서버 데이터베이스의 이름입니다.  
  
 *CredentialsType*  
 연결에 사용할 자격 증명의 유형입니다. 사용할 수 있는 값에는  
  
-   0 - Windows  
  
-   1 – [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 - Windows 서비스  
  
 *UserName*  
 보고서 서버 데이터베이스에 연결하는 데 사용되는 계정 이름입니다.  
  
 *암호*  
 보고서 서버 데이터베이스에 연결하는 데 사용되는 암호입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 *CredentialsType* 매개 변수를 0(Windows)으로 설정하면 *UserName* 및 *Password* 매개 변수를 설정해야 합니다. *UserName* 매개 변수는 "domain\username" 형식이어야 하며 값은 유효한 Windows 로그온을 나타내야 합니다.  
  
 *CredentialsType* 매개 변수를 1([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])로 설정하면 *UserName* 매개 변수에 전달되는 값이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름의 요구 사항을 따라야 합니다.  
  
 *CredentialsType* 매개 변수를 2(Windows 서비스)로 설정하면 보고서 서버에서 통합 보안을 사용하여 보고서 서버 데이터베이스에 연결하고 *UserName* 및 *Password* 매개 변수는 무시됩니다. 보고서 서버 웹 서비스는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 계정 또는 응용 프로그램 풀의 계정과 Windows 서비스 계정을 사용하여 보고서 서버 데이터베이스에 액세스합니다.  
  
 SetDatabaseConnection 메서드는 호출되면 지정된 보고서 서버에 대한 구성 파일에 있는 자격 증명과 데이터베이스 정보를 암호화하여 저장합니다.  
  
 SetDatabaseConnection 메서드는 보고서 서버에서 지정된 데이터를 사용하여 보고서 서버 데이터베이스에 연결할 수 있는지 확인하지 않습니다.  
  
 처음 설정하는 경우 ConnectionPoolSize 속성은 ConnectionPoolSize = #Processors * 75 프로세서를 기반으로 설정됩니다.  
  
 SetDatabaseConnection 메서드는 지정된 계정에 권한을 부여하지 않습니다. 호출 해야 합니다 [GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md) 보고서 서버 데이터베이스에 대 한 액세스를 해야 하 고 결과 스크립트를 실행 하는 각 계정에 대 한 메서드.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
