---
title: IsSharePointIntegrated 속성(WMI MSReportServer_Instance) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cbeaf43d507dd3aa852c9ecf783f808595fae6b0
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43271325"
---
# <a name="msreportserverinstance-properties---issharepointintegrated"></a>MSReportServer_Instance 속성 - IsSharePointIntegrated
  보고서 서버가 SharePoint 통합 모드에 있는지 여부를 지정합니다. SharePoint 모드에서는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]인스턴스가 SharePoint 공유 서비스이며 WMI 공급자를 통해 제어되지 않으므로 **부터는 이 속성이 항상** False [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>속성 값  
 보고서 서버가 SharePoint 통합 모드에 있는지 여부를 나타내는 **Boolean** 값입니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_Instance 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)   
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
