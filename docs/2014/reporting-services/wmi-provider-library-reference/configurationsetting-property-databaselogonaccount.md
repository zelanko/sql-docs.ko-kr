---
title: DatabaseLogonAccount 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseLogonAccount
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e98447aff31df0f95bc333fc643ab90a5b3f82ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62646319"
---
# <a name="databaselogonaccount-property-wmi-msreportserverconfigurationsetting"></a>DatabaseLogonAccount 속성(WMI MSReportServer_ConfigurationSetting)
  보고서 서버에서 보고서 서버 데이터베이스에 연결할 때 사용하는 로그온 계정을 지정합니다. 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>속성 값  
 로그온 계정 이름을 나타내는 `String` 개체입니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 속성의 유효 값은 [DatabaseLogonType](configurationsetting-property-databaselogontype.md) 속성 값에 따라 달라집니다.  
  
 경우이 속성은 무시 합니다 [DatabaseLogonType](configurationsetting-property-databaselogontype.md) 속성이 `2 (Service)`.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
