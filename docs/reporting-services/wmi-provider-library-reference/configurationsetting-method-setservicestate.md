---
title: "SetServiceState 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname: SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: "20"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 85e26f683c03e9b411ae3dc7d17f1b326981740d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="configurationsetting-method---setservicestate"></a>ConfigurationSetting 메서드 - SetServiceState
  보고서 서버 Windows 및 웹 서비스를 설정하거나 해제합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetServiceState(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *EnableWindowsService*  
 Windows 서비스의 상태를 나타내는 **Boolean** 값입니다. **true** 값은 보고서 서버 Windows 서비스를 시작하고 **false** 값은 Windows 서비스를 중지합니다.  
  
 *EnableWebService*  
 **웹 서비스 상태를 나타내는** Boolean [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 값입니다. **true** 값은 보고서 서버 웹 서비스를 시작하고 **false** 값은 웹 서비스를 중지합니다.  
  
 *EnableReportManager*  
 보고서 관리자의 필요한 상태를 나타내는 **Boolean** 값입니다.
 
 > [!NOTE] 
 > 이 설정은 SQL Server 2016 Reporting Services 누적 업데이트 2부터 사용되지 않습니다. 웹 포털은 항상 사용할 수 있습니다. 값이 무시됩니다.
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
