---
title: DeleteEncryptionKey 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DeleteEncryptionKey method
ms.assetid: ed2f25b6-6a63-468d-9279-a577ca01b096
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5e594b68fffccc3cb73feda3541a93686bfc6aef
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59957649"
---
# <a name="deleteencryptionkey-method-wmi-msreportserverconfigurationsetting"></a>DeleteEncryptionKey 메서드(WMI MSReportServer_ConfigurationSetting)
  보고서 서버 데이터베이스에서 암호화 키를 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub DeleteEncryptionKeys(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptionKeys(string InstallationID, out Int32 HRESULT,   
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>매개 변수  
 *InstallationID*  
 보고서 서버 데이터베이스의 키 테이블에 있는 보고서 서버의 설치 ID입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
 *ExtendedErrors[]*  
 [out] 호출에서 반환되는 추가 오류가 들어 있는 문자열 배열입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 HRESULT를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 *DeleteEncryptionKey* 메서드는 보고서 서버 데이터베이스의 보안 정보에 대한 액세스 권한이 있는 보고서 서버의 키 테이블에서 항목을 삭제합니다. 지정된 *InstallationID* 매개 변수가 데이터베이스의 설치 ID와 일치하지 않으면 메서드에서 오류가 반환됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
