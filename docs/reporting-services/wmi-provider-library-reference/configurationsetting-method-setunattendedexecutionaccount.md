---
title: "SetUnattendedExecutionAccount 메서드 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
apiname:
- SetUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetUnattendedExecutionAccount method
ms.assetid: 1ba6be6f-b05c-4ea0-af98-cd0780290b70
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1c94627129ed2e6706112aad013a3395c4a1e68a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---setunattendedexecutionaccount"></a>SetUnattendedExecutionAccount ConfigurationSetting 메서드
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
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>주의  
 SetUnattendedExecutionAccount 메서드는 보고서 서버가 지정된 사용자로 로그인할 수 있는지 여부를 확인하지 않습니다.  
  
 보고서 서버의 Windows 서비스 컨텍스트에서 무인 실행을 실행하기 위해 SetUnattendedExecutionAccount 메서드를 사용할 수 없습니다.  
  
## <a name="requirements"></a>요구 사항  
 **Namespace:**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
