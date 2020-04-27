---
title: SetEmailConfiguration 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 142fd8bf2116d4cc672aeb607938ea8c1c73bf8a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097993"
---
# <a name="setemailconfiguration-method-wmi-msreportserver_configurationsetting"></a>SetEmailConfiguration 메서드(WMI MSReportServer_ConfigurationSetting)
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
 전자 메일을 보내는 데 SMTP 서버를 사용하는지 여부를 나타내는 부울 값입니다. 이 값은 true로만 설정할 수 있습니다. 기본값은 False입니다.  
  
 *SMTPServer*  
 SMTP 서버의 이름이나 IP 주소가 들어 있는 문자열입니다.  
  
 *SenderEmailAddress*  
 보고서 서버에서 보낸 전자 메일의 '받는 사람:' 필드에 사용된 전자 메일 주소입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>Return Value  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 *SendUsingSMTPServer* 매개 변수를로 `true`설정 하면 보고서 서버 구성 파일의 **sendusing** 항목이 1로 설정 됩니다. *SendUsingSMTPServer* 가로 `false`설정 되 면 **sendusing** 항목이 구성 되지 않습니다.  
  
 이 메서드를 사용하면 보고서 서버 구성 파일의 **SendUsing** 항목을 1이 아닌 다른 값으로 설정할 수 없습니다. SMTP 메일 외의 다른 항목에 대해 보고서 서버를 구성하려면 구성 파일을 수동으로 편집해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
