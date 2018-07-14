---
title: SetServiceState 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f154e0eb7666fd4c8534e701f42a521b4fb70ff8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222533"
---
# <a name="setservicestate-method-wmi-msreportserverconfigurationsetting"></a>SetServiceState 메서드(WMI MSReportServer_ConfigurationSetting)
  보고서 서버 Windows 및 웹 서비스를 설정하거나 해제합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *EnableWindowsService*  
 `Boolean` Windows 서비스의 상태를 나타내는 값입니다. 값이 `true` 보고서 서버 Windows 시작 서비스를 `false` Windows 서비스를 중지 합니다.  
  
 *EnableWebService*  
 A `Boolean` 의 상태를 나타내는 값을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 서비스입니다. `true` 값은 보고서 서버 웹 서비스를 시작하고 `false` 값은 웹 서비스를 중지합니다.  
  
 *EnableReportManager*  
 `Boolean` 보고서 관리자의 필요한 상태를 나타내는 값입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
