---
title: DatabaseLogonAccount 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseLogonAccount
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 603ae515642fa524841c160cafc82c4e8ace3249
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571659"
---
# <a name="configurationsetting-property---databaselogonaccount"></a>ConfigurationSetting 속성 - DatabaseLogonAccount
  보고서 서버에서 보고서 서버 데이터베이스에 연결할 때 사용하는 로그온 계정을 지정합니다. 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>속성 값  
 로그온 계정 이름을 나타내는 **String** 개체입니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 속성의 유효 값은 [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md) 속성 값에 따라 달라집니다.  
  
 [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md) 속성이 **2(서비스)** 로 설정되어 있으면 이 속성은 무시됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
