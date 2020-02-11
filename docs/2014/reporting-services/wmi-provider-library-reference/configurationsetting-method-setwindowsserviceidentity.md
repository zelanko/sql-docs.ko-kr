---
title: SetWindowsServiceIdentity 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d08e9900453fe259d727e202489d728e0dce47e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097882"
---
# <a name="setwindowsserviceidentity-method-wmi-msreportserver_configurationsetting"></a>SetWindowsServiceIdentity 메서드(WMI MSReportServer_ConfigurationSetting)
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
  
 *계정일*  
 Windows 서비스를 실행하는 데 사용할 "DOMAIN\alias" 형식의 Windows 계정입니다.  
  
 *암호*  
 계정의 암호입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>Return Value  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 *UseBuiltInAccount* 매개 변수가로 `true` 설정 되어 있고 보고서 서버가 Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] 또는 Windows XP에서 실행 되는 경우 *Name*, *Domain*및 *Password* 매개 변수의 값이 무시 되 고 로컬 시스템 계정이 사용 됩니다.  
  
 *UseBuiltInAccount* 매개 변수를로 `true` 설정 하 고 보고서 서버에서 Windows server 2003를 실행 하는 경우 *도메인* 및 *암호* 속성이 무시 되 고 이름 필드에 "Builtin\NetworkService" 또는 "Builtin\System" 또는 "Builtin\LocalService"가 포함 되어야 합니다.  
  
 SetWindowsServiceIdentity 메서드는 보고서 서버 설치 디렉터리에 있는 파일 및 폴더에 대한 파일 사용 권한을 설정합니다.  
  
 *계정* 매개 변수에 지정 된 계정에는 `LogonAsService` Windows의 권한이 필요 합니다. 이 권한은 메서드를 통해 지정된 계정에 부여됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임 스페이스:**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
