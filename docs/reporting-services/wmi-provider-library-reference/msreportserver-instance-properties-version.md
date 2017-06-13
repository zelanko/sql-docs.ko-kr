---
title: "Version 속성 (WMI MSReportServer_Instance) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Version property
ms.assetid: eea6bfe9-3130-4272-b3c2-c334349a7afd
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 342c13617ea4841f68df243ed21bd51683f328d0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="msreportserverinstance-properties---version"></a>MSReportServer_Instance 속성-버전
  Major.Minor.Build.Revision 형식으로 보고서 서버의 버전을 반환합니다. 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim Version As String  
```  
  
```csharp  
public string Version;  
```  
  
## <a name="property-value"></a>속성 값  
 보고서 서버의 버전이 들어 있는 **string** 입니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [MSReportServer_Instance 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)  
  
  
