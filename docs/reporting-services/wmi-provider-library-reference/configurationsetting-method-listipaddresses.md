---
title: ListIPAddresses 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListIPAddresses method
ms.assetid: 7e7cf182-fba0-4604-a474-098461e23e9d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1207c4c9688826b599548477a35ca123b9d39c28
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65579933"
---
# <a name="configurationsetting-method---listipaddresses"></a>ConfigurationSetting 메서드 - ListIPAddresses
  보고서 서버 컴퓨터의 IP 주소를 나열합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub ListIPAddresses (ByRef IPAddress() as String, _  
    ByRef IPVersion()as String, ByRef IsDhcpEnabled () as Boolean, _   
    ByRef Length as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListIPAddresses (out string[] IPAddress,   
    out string[] IPVersion, out bool[] isDhcpEnabled, out int length,   
    out int HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *IPAddress[]*  
 [out] 컴퓨터의 IP 주소 목록입니다.  
  
 *IPVersion[]*  
 [out] IP 주소의 버전입니다.  
  
 *IsDhcpEnabled[]*  
 [out] IP 주소에 DHCP를 사용할 수 있는지 여부를 나타냅니다.  
  
 *길이*  
 [out] 메서드에서 반환된 배열의 길이입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>Return Value  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타내고 오류 코드는 호출이 실패했음을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 *IPVersion* 문자열은 V4, V6입니다.  
  
 *IsDhcpEnabled* 가 **True**이면 *IPAddress* 가 동적이므로 SSL 바인딩에 사용해서는 안 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
