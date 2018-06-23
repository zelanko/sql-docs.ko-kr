---
title: SetSecureConnectionLevel 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
caps.latest.revision: 21
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f761337d48cc168ee87a0557201b5827a80afd21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089230"
---
# <a name="setsecureconnectionlevel-method-wmi-msreportserverconfigurationsetting"></a>SetSecureConnectionLevel 메서드(WMI MSReportServer_ConfigurationSetting)
  보고서 서버의 보안 연결 수준을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetSecureConnectionLevel(Level as Integer, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Int32 Level,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *Level*  
 보안 연결 수준을 나타내는 정수 값입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 메서드를 호출하면 보고서 서버의 SecureConnectionLevel 속성이 지정된 값으로 설정됩니다. 값이 0이면 SSL이 해제되어 있음을 나타냅니다. 값이 1보다 크거나 같으면 SSL이 설정됨을 나타냅니다.  
  
-   값이 설정 되 면 보고서 서버 구성 파일에 SecureConnectionLevel 요소 변경 되 면 및 `URLRoot` 구성 파일의 요소는 경우 "https://"를 사용 하도록 설정 되어 지정 된 *수준* 보다 크면 또는 1 또는 "http://" 같은 경우 지정 된 *수준* 은 0입니다.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서 SecureConnectionLevel은 설정/해제가 전환되며 기본값은 0입니다. SetSecureConnectionLevel 메서드 API를 통해 전달되는 값이 1보다 크거나 같으면 SSL이 설정된 것으로 간주하고 그에 따라 구성 속성 SecureConnectionLevel이 rsreportserver.config 파일에서 설정됩니다. 값 2와 3도 이전 버전과의 호환성을 위해 계속 허용됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  