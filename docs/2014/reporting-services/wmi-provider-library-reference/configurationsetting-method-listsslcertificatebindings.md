---
title: ListSSLCertificateBindings 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9802176b5f5c82ba60a4e47d85445b54eaa1a5f0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031624"
---
# <a name="listsslcertificatebindings-method-wmi-msreportserverconfigurationsetting"></a>ListSSLCertificateBindings 메서드(WMI MSReportServer_ConfigurationSetting)
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
 [out] 인증서 바인딩이 있는 애플리케이션입니다.  
  
 *CertificateHash[]*  
 [out] 인증서에 대한 해시입니다.  
  
 *IPAddress[]*  
 [out] 애플리케이션의 IP 주소입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
