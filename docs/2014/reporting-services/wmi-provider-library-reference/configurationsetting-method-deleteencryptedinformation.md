---
title: DeleteEncryptedInformation 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- DeleteEncryptedInformation (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DeleteEncryptedInformation method
ms.assetid: c14ed187-bdd9-4304-88e3-72072f03c21b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4ffe9834ea57f3f4a0d48387f631ae08a45182ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098517"
---
# <a name="deleteencryptedinformation-method-wmi-msreportserverconfigurationsetting"></a>DeleteEncryptedInformation 메서드(WMI MSReportServer_ConfigurationSetting)
  보고서 서버 데이터베이스에서 암호화된 정보를 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub DeleteEncryptedInformation(ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptedInformation(out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>매개 변수  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
 *ExtendedErrors[]*  
 [out] 호출에서 반환되는 추가 오류가 들어 있는 문자열 배열입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 이 메서드를 호출하면 다음 데이터가 삭제됩니다.  
  
-   사용자 이름 및 암호를 비롯하여 암호화되는 데이터 원본 정보  
  
-   배달 확장 프로그램 인터페이스를 사용하여 암호화되는 구독 데이터  
  
-   보고서 서버 데이터베이스에 있는 키 테이블의 모든 정보  
  
 이 메서드를 호출한 후 사용자는 보고서 서버 데이터베이스를 사용하는 각 컴퓨터를 초기화해야 합니다.  
  
 DeleteEncryptedInformation 메서드를 호출해도 보고서 서버 구성 파일에는 영향을 주지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
