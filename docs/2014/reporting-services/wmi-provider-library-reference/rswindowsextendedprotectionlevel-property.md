---
title: RSWindowsExtendedProtectionLevel 속성 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 176766f1097e2edf010fa28cae51992e291dd92b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52394696"
---
# <a name="rswindowsextendedprotectionlevel-property-wmi-msreportserverconfigurationsetting"></a>RSWindowsExtendedProtectionLevel 속성(WMI MSReportServer_ConfigurationSetting)
  보고서 서버에서 지원하도록 구성된 보호 수준을 나타내는 문자열 값을 반환합니다. 이 속성은 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>Remarks  
 보고서 서버에서 지원하도록 구성된 보호 수준을 나타내는 문자열 값을 반환합니다. WMI 공급자가 연결되어 있는 보고서 서버에서 확장된 보호를 지원하지 않으면 ""(빈 문자열)이 반환됩니다. 다음 목록에서는 유효한 값을 보여 줍니다.  
  
 `"Off" | "Allow" | "Require"`  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>관련 항목  
 [RSWindowsExtendedProtectionScenario 속성&#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionscenario-property.md)   
 [SetExtendedProtectionSettings 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Reporting Services 인증에 대한 확장된 보호](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer 구성 파일](../report-server/rsreportserver-config-configuration-file.md)  
  
  
