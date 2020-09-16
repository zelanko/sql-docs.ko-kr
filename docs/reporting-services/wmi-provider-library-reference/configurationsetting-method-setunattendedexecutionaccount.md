---
description: SetUnattendedExecutionAccount 메서드(WMI MSReportServer_ConfigurationSetting)
title: SetUnattendedExecutionAccount 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetUnattendedExecutionAccount method
ms.assetid: 1ba6be6f-b05c-4ea0-af98-cd0780290b70
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5f65c36ae1f27039061642dba87ec79b6f81c7c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497926"
---
# <a name="configurationsetting-method---setunattendedexecutionaccount"></a>ConfigurationSetting 메서드 - SetUnattendedExecutionAccount
  무인 모드로 보고서를 실행하는 데 사용되는 계정을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub SetUnattendedExecutionAccount(UserName as String, _  
    Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetUnattendedExecutionAccount (string UserName,   
    string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *UserName*  
 무인 실행에 사용할 Windows 계정입니다.  
  
 *암호*  
 지정된 계정의 암호입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>Return Value  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 SetUnattendedExecutionAccount 메서드는 보고서 서버가 지정된 사용자로 로그인할 수 있는지 여부를 확인하지 않습니다.  
  
 보고서 서버의 Windows 서비스 컨텍스트에서 무인 실행을 실행하기 위해 SetUnattendedExecutionAccount 메서드를 사용할 수 없습니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
