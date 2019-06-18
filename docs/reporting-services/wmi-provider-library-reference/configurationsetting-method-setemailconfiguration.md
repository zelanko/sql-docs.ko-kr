---
title: SetEmailConfiguration 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3e2b3e3c1d3d9fc5193a8c87c2aa96f9ff2d3ba2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581005"
---
# <a name="configurationsetting-method---setemailconfiguration"></a>ConfigurationSetting 메서드 - SetEmailConfiguration
  보고서 서버가 전자 메일을 보낼 때 사용할 전자 메일 배달 확장 프로그램을 구성합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetEmailConfiguration(ByVal SendUsingSMTPServer As Boolean, _  
    ByVal SMTPServer As String, ByVal SenderEmailAddress As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetEmailConfiguration (Boolean SendUsingSMTPServer,   
   string SMTPServer, string SenderEmailAddress,   
   out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *SendUsingSMTPServer*  
 전자 메일을 보내는 데 SMTP 서버를 사용하는지 여부를 나타내는 부울 값입니다. 이 값은 true로만 설정할 수 있습니다. 기본값은 false입니다.  
  
 *SMTPServer*  
 SMTP 서버의 이름이나 IP 주소가 들어 있는 문자열입니다.  
  
 *SenderEmailAddress*  
 보고서 서버에서 보낸 전자 메일의 '받는 사람:' 필드에 사용된 전자 메일 주소입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 *SendUsingSMTPServer* 매개 변수를 **true**로 설정하면 보고서 서버 구성 파일의 **SendUsing** 항목이 1로 설정됩니다. *SendUsingSMTPServer* 매개 변수를 **false**로 설정하면 **SendUsing** 항목이 구성되지 않습니다.  
  
 이 메서드를 사용하면 보고서 서버 구성 파일의 **SendUsing** 항목을 1이 아닌 다른 값으로 설정할 수 없습니다. SMTP 메일 외의 다른 항목에 대해 보고서 서버를 구성하려면 구성 파일을 수동으로 편집해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
