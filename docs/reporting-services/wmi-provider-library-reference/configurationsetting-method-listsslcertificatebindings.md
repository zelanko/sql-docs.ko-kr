---
title: ListSSLCertificateBindings 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4c972b4f5b757985b28c576541dff968b14f60a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723761"
---
# <a name="configurationsetting-method---listsslcertificatebindings"></a>ConfigurationSetting 메서드 - ListSSLCertificateBindings
  컴퓨터에 설치된 SSL 인증서 목록을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub ListSSLCertificateBindings(ByVal LCID As Int32, ByRef Application() As String, _  
    ByRef CertificateHash() As String, ByRef IPAddresses() As String, ByRef Port() As Int32, _  
    ByRef Errors() As String, ByRef Length As Int32, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListSSLCertificateBindings(Int32 Lcid, out string[] Application,   
    out string[] CertificateHash,out string[] IPAddress,   
    out Int32[] Port, out string Errors,   
    out Int32 length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *LCID*  
 반환되는 오류 메시지에 사용할 로캘입니다.  
  
 *Application[]*  
 [out] 인증서 바인딩이 있는 응용 프로그램입니다.  
  
 *CertificateHash[]*  
 [out] 인증서에 대한 해시입니다.  
  
 *IPAddress[]*  
 [out] 응용 프로그램의 IP 주소입니다.  
  
 *Port[]*  
 [out] rsreportserver.config의 바인딩에 저장되는 포트 번호입니다.  
  
 *Errors[]*  
 [out] 발생한 오류에 대한 설명입니다.  
  
 *길이*  
 [out] 메서드에서 반환된 배열의 길이입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
