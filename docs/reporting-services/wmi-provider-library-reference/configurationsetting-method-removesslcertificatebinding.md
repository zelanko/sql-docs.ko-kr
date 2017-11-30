---
title: "RemoveSSLCertificateBindings 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
helpviewer_keywords: RemoveSSLCertificateBindings method
ms.assetid: b8b484c9-04c4-4ae9-980e-67bbe5aa8481
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 09a6c39747e353d4b531ab356f88cab1766b19c4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="configurationsetting-method---removesslcertificatebinding"></a>ConfigurationSetting 메서드 - RemoveSSLCertificateBinding
  SSL 인증서 바인딩을 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub RemoveSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveSSLCertificateBindings(string Application,  
    string CertificateHash, string IPAddress, Int32 Port, Int32 Lcid,  
    out string Error, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *응용 프로그램*  
 인증서 바인딩을 제거해야 하는 응용 프로그램의 이름입니다.  
  
 *CertificateHash*  
 인증서에 대한 해시입니다.  
  
 *IPAddress*  
 응용 프로그램의 IP 주소입니다.  
  
 *포트*  
 바인딩과 연결된 SSL 포트입니다.  
  
 *lcid*  
 반환되는 오류 메시지에 사용할 로캘입니다.  
  
 *오류*  
 [out] 발생한 오류에 대한 설명입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타내고 오류 코드는 호출이 실패했음을 나타냅니다.  
  
## <a name="remarks"></a>주의  
 이 메서드는 rsreportserver.config 파일에서 특정 바인딩을 제거하고 HTTP.SYS 파일에서 특정 바인딩을 선택적으로 제거합니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
