---
title: SetVirtualDirectory 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e68bb7c70d08fb07d3079436fafe5fd61ae104f1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66097916"
---
# <a name="setvirtualdirectory-method-wmi-msreportserverconfigurationsetting"></a>SetVirtualDirectory 메서드(WMI MSReportServer_ConfigurationSetting)
  지정한 애플리케이션에 가상 디렉터리 이름을 설정합니다.  
  
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
 가상 디렉터리를 설정할 애플리케이션의 이름입니다.  
  
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
 각 애플리케이션의 모든 URL 예약에 대해 하나의 가상 디렉터리 이름만 지정할 수 있습니다.  
  
 VirtualDirectory는 가상 디렉터리의 명명 규칙을 준수해야 합니다. VirtualDirectory는 빈 문자열이나 공백이 될 수 없습니다.  
  
 \Configuration\URLReservations\Application\VirtualDirectory 요소의 값을 업데이트합니다. URL 예약을 만들지 않아도 업데이트할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
