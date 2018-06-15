---
title: SetWindowsServiceIdentity 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
caps.latest.revision: 19
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 45ceacca295b5ba6df2cb45f0386ed5bf50da70c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33031420"
---
# <a name="configurationsetting-method---setwindowsserviceidentity"></a>ConfigurationSetting 메서드 - SetWindowsServiceIdentity
  보고서 서버 Windows 서비스가 지정된 Windows 사용자로 실행되도록 하고 이 계정에 보고서 서버를 작동하기에 충분한 파일 시스템 사용 권한을 부여합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetWindowsServiceIdentity(UseBuiltInAccount as Boolean, _  
    Account as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetWindowsServiceIdentity(boolean UseBuiltInAccount,   
    string Account, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *UseBuiltInAccount*  
 지정된 계정이 기본 제공 Windows 계정인지 여부를 나타냅니다.  
  
 *계정*  
 Windows 서비스를 실행하는 데 사용할 "DOMAIN\alias" 형식의 Windows 계정입니다.  
  
 *암호*  
 계정의 암호입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 *UseBuiltInAccount* 매개 변수가 **true** 로 설정되어 있고 보고서 서버가 Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] 또는 Windows XP에서 실행되고 있으면 *Name*, *Domain*및 *Password* 매개 변수의 값이 무시되고 로컬 시스템 계정이 사용됩니다.  
  
 *UseBuiltInAccount* 매개 변수가 **true** 로 설정되어 있고 보고서 서버가 Windows Server 2003에서 실행되고 있으면 *Domain* 및 *Password* 속성이 무시되고 이름 필드에 “Builtin\NetworkService”, “Builtin\System” 또는 “Builtin\LocalService”가 포함되어야 합니다.  
  
 SetWindowsServiceIdentity 메서드는 보고서 서버 설치 디렉터리에 있는 파일 및 폴더에 대한 파일 사용 권한을 설정합니다.  
  
 *Account* 매개 변수에 지정된 계정에는 Windows의 **LogonAsService** 권한이 필요합니다. 이 권한은 메서드를 통해 지정된 계정에 부여됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
