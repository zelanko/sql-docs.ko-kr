---
title: GetReportServerUrls 메서드(WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2580538f24fe220369f0f6ea807e6caa8dd822a6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020532"
---
# <a name="getreportserverurls-method-wmi-msreportserverinstance"></a>GetReportServerUrls 메서드(WMI MSReportServer_Instance)
  사용자가 보고서 서버 및 보고서 관리자에 액세스하는 데 사용할 수 있는 URL 목록을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ApplicationName[]*  
 설치된 애플리케이션이 들어 있는 배열입니다. 값은 `ReportServerWebService` 또는 `ReportManager`입니다.  
  
 *URLs[]*  
 성공적으로 등록된 URL이 들어 있는 배열입니다.  
  
 *길이*  
 반환된 배열의 길이가 들어 있는 정수 값입니다.  
  
 *HRESULT*  
 성공 또는 오류 코드를 나타내는 값입니다.  
  
## <a name="return-values"></a>반환 값  
  
## <a name="remarks"></a>Remarks  
 WMI 관리 개체에서 노출되는 메서드는 InvokeMethod 함수를 통해 호출됩니다. 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework WMI 설명서의 "관리 개체에서 메서드 실행(Executing Methods on Management Objects)"을 참조하십시오.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
