---
title: "ReencryptSecureInformation 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname: ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2023843b8bafc6c6fe0cd73e4510001dab4a52db
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="configurationsetting-method---reencryptsecureinformation"></a>ConfigurationSetting 메서드 - ReencryptSecureInformation
  새 암호화 키를 생성하고 이 새 키를 사용하여 카탈로그에 있는 모든 보안 정보를 다시 암호화합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>매개 변수  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
 *ExtendedErrors[]*  
 [out] 호출에서 반환되는 추가 오류가 들어 있는 문자열 배열입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>주의  
 관리자는 ReencryptSecureInformation 메서드를 사용하여 기존 암호화 키를 새 키로 바꿀 수 있습니다.  
  
 이 메서드가 호출되면 보고서 서버가 새 암호화 키를 생성하고 이 새 암호화 키로 모든 암호화 내용을 반복하여 다시 암호화합니다.  
  
 배달 확장 프로그램은 배달 설정 구조의 보안 정보를 저장할 수 있습니다. ReencryptSecureInformation이 호출되면 보고서 서버가 각 구독 및 해당 배달 확장 프로그램을 로드하여 연결된 설정에 저장된 정보를 다시 암호화합니다.  
  
 이 메서드를 스케일 아웃 배포의 컴퓨터에서 실행하면 스케일 아웃 배포의 각 컴퓨터를 다시 초기화해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
