---
description: SetDatabaseConnection 메서드(WMI MSReportServer_ConfigurationSetting)
title: SetDatabaseConnection 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ca1e82757c5e194fc0c9e1b723b7a929a2c93837
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373339"
---
# <a name="configurationsetting-method---setdatabaseconnection"></a>ConfigurationSetting 메서드 - SetDatabaseConnection
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
 연결에 사용할 자격 증명의 유형입니다. 값은  
  
-   0 - Windows  
  
-   1 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 - Windows 서비스  
  
 *UserName*  
 보고서 서버 데이터베이스에 연결하는 데 사용되는 계정 이름입니다.  
  
 *암호*  
 보고서 서버 데이터베이스에 연결하는 데 사용되는 암호입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>Return Value  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 *CredentialsType* 매개 변수를 0(Windows)으로 설정하면 *UserName* 및 *Password* 매개 변수를 설정해야 합니다. *UserName* 매개 변수는 "domain\username" 형식이어야 하며 값은 유효한 Windows 로그온을 나타내야 합니다.  
  
 *CredentialsType* 매개 변수를 1([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])로 설정하면 *UserName* 매개 변수에 전달되는 값이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름의 요구 사항을 따라야 합니다.  
  
 *CredentialsType* 매개 변수를 2(Windows 서비스)로 설정하면 보고서 서버에서 통합 보안을 사용하여 보고서 서버 데이터베이스에 연결하고 *UserName* 및 *Password* 매개 변수는 무시됩니다. 보고 서버 웹 서비스는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 계정 또는 애플리케이션 풀의 계정과 Windows 서비스 계정을 사용하여 보고서 서버 데이터베이스에 액세스합니다.  
  
 SetDatabaseConnection 메서드는 호출되면 지정된 보고서 서버에 대한 구성 파일에 있는 자격 증명과 데이터베이스 정보를 암호화하여 저장합니다.  
  
 SetDatabaseConnection 메서드는 보고서 서버에서 지정된 데이터를 사용하여 보고서 서버 데이터베이스에 연결할 수 있는지 확인하지 않습니다.  
  
 처음 설정하는 경우 ConnectionPoolSize 속성은 ConnectionPoolSize = #Processors * 75 프로세서를 기반으로 설정됩니다.  
  
 SetDatabaseConnection 메서드는 지정된 계정에 권한을 부여하지 않습니다. 보고서 서버 데이터베이스에 액세스하고 결과 스크립트를 실행해야 하는 각 계정에 대해 [GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md) 메서드를 호출해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
