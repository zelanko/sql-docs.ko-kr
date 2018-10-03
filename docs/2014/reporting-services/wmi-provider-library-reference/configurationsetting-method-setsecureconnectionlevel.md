---
title: SetSecureConnectionLevel 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5dd2ca31f890f0f16b3bbc68097572bb82d2bef2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179163"
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
  
-   값으로 설정 하는 경우 보고서 서버 구성 파일의 SecureConnectionLevel 요소가 변경 되 면 하며 `URLRoot` 요소는 구성 파일의 경우 "https://"를 사용 하도록 설정 되어 지정 된 *수준* 보다 크면 또는 같은 1 또는 "http://" 하는 경우 지정 된 *수준* 은 0입니다.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서 SecureConnectionLevel은 설정/해제가 전환되며 기본값은 0입니다. SetSecureConnectionLevel 메서드 API를 통해 전달되는 값이 1보다 크거나 같으면 SSL이 설정된 것으로 간주하고 그에 따라 구성 속성 SecureConnectionLevel이 rsreportserver.config 파일에서 설정됩니다. 값 2와 3도 이전 버전과의 호환성을 위해 계속 허용됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
