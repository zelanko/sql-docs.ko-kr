---
title: IsSharePointIntegrated 속성(WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: de2fb448c599f53ec2c535c85a0f836d4a23213b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325653"
---
# <a name="issharepointintegrated-property-wmi"></a>IsSharePointIntegrated 속성(WMI)
  보고서 서버가 SharePoint 통합 모드에 있는지 여부를 지정합니다. SharePoint 모드에서는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 인스턴스가 SharePoint 공유 서비스이며 WMI 공급자를 통해 제어되지 않으므로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]부터는 이 속성이 항상 `False`를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>속성 값  
 보고서 서버가 SharePoint 통합 모드에 있는지 여부를 나타내는 `Boolean` 개체입니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
