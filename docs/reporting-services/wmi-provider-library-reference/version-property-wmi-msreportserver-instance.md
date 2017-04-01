---
title: "Version 속성(WMI MSReportServer_Instance) | Microsoft Docs"
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
helpviewer_keywords: 
  - "Version 속성"
ms.assetid: eea6bfe9-3130-4272-b3c2-c334349a7afd
caps.latest.revision: 9
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Version 속성(WMI MSReportServer_Instance)
  Major.Minor.Build.Revision 형식으로 보고서 서버의 버전을 반환합니다. 읽기 전용입니다.  
  
## 구문  
  
```vb  
Public Dim Version As String  
```  
  
```csharp  
public string Version;  
```  
  
## 속성 값  
 보고서 서버의 버전이 들어 있는 **string** 입니다.  
  
## 코드 예  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## 관련 항목:  
 [MSReportServer_Instance 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)  
  
  