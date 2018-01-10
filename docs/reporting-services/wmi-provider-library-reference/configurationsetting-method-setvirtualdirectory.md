---
title: "SetVirtualDirectory 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
caps.latest.revision: "11"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f94837f98c1b2e2b97c9acac256470d1978d873d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---setvirtualdirectory"></a>ConfigurationSetting 메서드 - SetVirtualDirectory
  지정한 응용 프로그램에 가상 디렉터리 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *응용 프로그램*  
 가상 디렉터리를 설정할 응용 프로그램의 이름입니다.  
  
 *VirtualDirectory*  
 가상 디렉터리의 이름입니다.  
  
 *lcid*  
 가상 디렉터리의 로캘 ID입니다.  
  
 *오류*  
 [out] 발생한 오류에 대한 설명입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타내고 오류 코드는 호출이 실패했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 각 응용 프로그램의 모든 URL 예약에 대해 하나의 가상 디렉터리 이름만 지정할 수 있습니다.  
  
 VirtualDirectory는 가상 디렉터리의 명명 규칙을 준수해야 합니다. VirtualDirectory는 빈 문자열이나 공백이 될 수 없습니다.  
  
 \Configuration\URLReservations\Application\VirtualDirectory 요소의 값을 업데이트합니다. URL 예약을 만들지 않아도 업데이트할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
