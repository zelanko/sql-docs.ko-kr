---
title: SecureConnectionLevel 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SecureConnectionLevel
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 44db8007a7b8abfed99d65c93037dd647cc4cb41
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074449"
---
# <a name="secureconnectionlevel-property-wmi-msreportserverconfigurationsetting"></a>SecureConnectionLevel 속성(WMI MSReportServer_ConfigurationSetting)
  RSReportServer.config 파일에 지정된 보안 연결 수준을 반환합니다. 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>속성 값  
 `Integer` 보안 연결 수준을 나타내는 값입니다. 반환 값은 SSL이 구성되어 있는지 여부를 나타냅니다. 값이 1보다 크거나 같으면 SSL이 설정되어 있음을 나타냅니다. 값이 0이면 SSL이 해제되어 있음을 나타냅니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
