---
title: "DatabaseLogonAccount 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "DatabaseLogonAccount"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "DatabaseLogonAccount 속성"
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
caps.latest.revision: 24
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# DatabaseLogonAccount 속성(WMI MSReportServer_ConfigurationSetting)
  보고서 서버에서 보고서 서버 데이터베이스에 연결할 때 사용하는 로그온 계정을 지정합니다. 읽기 전용입니다.  
  
## 구문  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## 속성 값  
 로그온 계정 이름을 나타내는 **String** 개체입니다.  
  
## 코드 예  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 주의  
 이 속성의 유효 값은 [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md) 속성 값에 따라 달라집니다.  
  
 [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md) 속성이 **2(서비스)**로 설정되어 있으면 이 속성은 무시됩니다.  
  
## 요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 관련 항목:  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  