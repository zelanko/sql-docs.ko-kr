---
title: CreateSSLCertificateBinding 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- CreateSSLCertificateBinding
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: da18ee258d12a667280c601526f0433c1a5b0600
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070493"
---
# <a name="createsslcertificatebinding-method-wmi-msreportserverconfigurationsetting"></a>CreateSSLCertificateBinding 메서드(WMI MSReportServer_ConfigurationSetting)
  SSL 인증서 바인딩을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *응용 프로그램*  
 인증서 바인딩을 만들어야 하는 응용 프로그램의 이름입니다.  
  
 *CertificateHash*  
 인증서에 대한 해시입니다.  
  
 *IPAddress*  
 응용 프로그램의 IP 주소입니다.  
  
 *포트*  
 바인딩과 연결된 SSL 포트입니다.  
  
 *Lcid*  
 반환되는 오류 메시지에 사용할 로캘입니다.  
  
 *오류*  
 [out] 발생한 오류에 대한 설명입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타내고 오류 코드는 호출이 실패했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 응용 프로그램의 rsreportserver.config에 바인딩을 추가합니다. HTTP.SYS에 바인딩이 없으면 이 파일에 바인딩이 만들어집니다.  
  
 바인딩을 만들기 전에 메서드 호출은 지정된 응용 프로그램에 대한 URL 예약을 검사하여 SSL 인증서 바인딩이 유효한지 확인합니다.  
  
 다음과 같은 경우 유효성 검사 후 오류가 발생할 수 있습니다.  
  
1.  인증서가 없는 경우  
  
2.  지정한 IPAddress가 이 컴퓨터의 IPAddress와 일치하지 않는 경우  
  
3.  지정한 IPAddress가 DHCP IPAddress(정기적으로 변경됨)인 경우 - 대신 와일드카드 IP 주소 사용(0.0.0.0)  
  
4.  지정한 IPAddress가 URL 예약의 IP 주소와 일치하지 않고 와일드카드 또는 호스트 이름 URL 예약이 모두 없는 경우  
  
5.  호스트 이름을 지정하는 URL 예약이 있으나 해당 호스트 이름이 인증서의 호스트 이름과 일치하지 않는 경우  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
