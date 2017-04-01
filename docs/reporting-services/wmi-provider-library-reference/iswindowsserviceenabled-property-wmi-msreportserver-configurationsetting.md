---
title: "IsWindowsServiceEnabled 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "IsWindowsServiceEnabled"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "IsWindowsServiceEnabled 속성"
ms.assetid: b1b75d72-6220-43fe-abfb-f967f3972d00
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# IsWindowsServiceEnabled 속성(WMI MSReportServer_ConfigurationSetting)
  보고서 서버 Windows 서비스를 사용하는지 여부를 나타냅니다. 읽기 전용입니다.  
  
## 구문  
  
```vb  
Public Dim IsWindowsServiceEnabled As Boolean  
```  
  
```csharp  
public boolean IsWindowsServiceEnabled;  
```  
  
## 속성 값  
 읽기 전용 **부울** 값입니다. **true** 값은 보고서 서버 Windows 서비스를 사용할 수 있음을 나타냅니다.  
  
## 코드 예  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 관련 항목:  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  