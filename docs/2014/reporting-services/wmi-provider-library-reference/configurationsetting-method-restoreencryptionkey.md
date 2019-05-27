---
title: RestoreEncryptionKey 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- RestoreEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- RestoreEncryptionKey method
ms.assetid: 37e949f5-15af-4858-848a-f482ee94fcd9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d4cb556e127fa23f5b16506abdcc8e04ed433878
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098133"
---
# <a name="restoreencryptionkey-method-wmi-msreportserverconfigurationsetting"></a>RestoreEncryptionKey 메서드(WMI MSReportServer_ConfigurationSetting)
  지정된 암호화 키를 보고서 서버 데이터베이스에 다시 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub RestoreEncryptionKey(ByRef KeyFile() As Integer, _  
    ByRef Length As Int32, ByVal Password As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void RestoreEncryptionKey(out Byte[] KeyFile, out Int32 Length,   
            string Password, out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>매개 변수  
 *KeyFile[]*  
 [out] 암호화된 암호화 키를 포함하는 배열입니다.  
  
 *길이*  
 [out] 메서드에서 반환된 배열의 길이입니다.  
  
 *암호*  
 암호화 키를 암호화하는 데 사용되는 문자열입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
 *ExtendedErrors[]*  
 [out] 호출에서 반환되는 추가 오류가 들어 있는 문자열 배열입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 보고서 서버 데이터베이스에 보고서 서버에 대한 항목이 이미 있으면 삭제됩니다. 그런 다음, 지정된 암호화 키와 보고서 서버의 공개 키를 사용하여 새로운 항목이 만들어집니다.  
  
 이 메서드는 암호화 키 목록을 지우는 [DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md) 메서드 다음에 호출하는 것이 가장 효과적입니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
