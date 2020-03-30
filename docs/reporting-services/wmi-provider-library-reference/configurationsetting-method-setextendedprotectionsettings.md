---
title: SetExtendedProtectionSettings 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cbfd4392572713e1c81fef07467842e18549e089
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65581019"
---
# <a name="configurationsetting-method---setextendedprotectionsettings"></a>ConfigurationSetting 메서드 - SetExtendedProtectionSettings
  SetExtendedProtectionSettings 메서드는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 파일인 RSReportServer.config에서 RSWindowsExtendedProtectionLevel 및 RSWindowsExtendedProtectionScenario 속성을 설정하는 데 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetExtendedProtectionSettings( _  
        ByVal ExtendedProtectionLevel As String, _  
        ByVal ExtendedProtectionScenario As String, _  
        ByRef Warnings() As String, _  
        ByRef Length As Int32, _  
        ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetExtendedProtectionSettings(  
            string ExtendedProtectionLevel,  
            string ExtendedProtectionScenario,  
            out string[] Warnings,  
            out Int32 Length,  
            out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ExtendedProtectionLevel*  
 RSRreportserver.config 파일에서 RSWindowsExtendedProtectionLevel을 설정합니다. 이 필수 값은 대/소문자를 구분하지 않습니다.  
  
 다음 목록에서는 유효한 값을 보여 줍니다.  
  
 `"Off | Allow | Require"`  
  
 *ExtendedProtectionScenario*  
 RSReportserver.config 파일에서 RSWindowsExtendedProtectionScenario를 설정합니다. 이 필수 값은 대/소문자를 구분하지 않습니다.  
  
 다음 목록에서는 유효한 값을 보여 줍니다.  
  
 `"Any" | "Proxy" | "Direct"`  
  
## <a name="remarks"></a>설명  
 RSWindowsExtendedProtectionLevel 및 RSWindowsExtendedProtectionScenario 속성은 RSReportServer.config 파일의 AuthenticationTypes에 RSWindowNTLM, RSWindowsNegotiate, 또는 RSWindowsKerberos가 포함된 경우 적용됩니다. 이러한 속성을 설정하면 사용자와 클라이언트 소프트웨어가 보고서 서버에 인증하는 방식에 영향을 줍니다. 먼저 확장된 보호와 관련된 설명서를 읽은 후 ExtendedProtectionLevel을 **Allow** 또는 **Require**로 설정하는 것이 좋습니다.  
  
 ExtendedProtectionLevel을 설정하려면 사용자가 보고서 서버의 BUILTIN\Administrators 그룹의 멤버여야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [RSWindowsExtendedProtectionScenario 속성&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [RSWindowsExtendedProtectionLevel 속성&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [Reporting Services 인증에 대한 확장된 보호](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
