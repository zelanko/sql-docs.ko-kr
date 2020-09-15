---
description: RSWindowsExtendedProtectionLevel 속성
title: RSWindowsExtendedProtectionLevel 속성 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4098d19c86ab6940aebd254ba08a196ae880dc5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373049"
---
# <a name="rswindowsextendedprotectionlevel-property"></a>RSWindowsExtendedProtectionLevel 속성
  보고서 서버에서 지원하도록 구성된 보호 수준을 나타내는 문자열 값을 반환합니다. 이 속성은 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>설명  
 보고서 서버에서 지원하도록 구성된 보호 수준을 나타내는 문자열 값을 반환합니다. WMI 공급자가 연결되어 있는 보고서 서버에서 확장된 보호를 지원하지 않으면 ""(빈 문자열)이 반환됩니다. 다음 목록에서는 유효한 값을 보여 줍니다.  
  
 `"Off" | "Allow" | "Require"`  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>참고 항목  
 [RSWindowsExtendedProtectionScenario 속성&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [SetExtendedProtectionSettings 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Reporting Services 인증에 대한 확장된 보호](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
