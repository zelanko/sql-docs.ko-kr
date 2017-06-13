---
title: "DeleteEncryptionKey 메서드 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
- DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DeleteEncryptionKey method
ms.assetid: ed2f25b6-6a63-468d-9279-a577ca01b096
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 06775389935ba0b9cf072fc8f417cfb52eac7811
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="configurationsetting-method---deleteencryptionkey"></a>DeleteEncryptionKey ConfigurationSetting 메서드
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
  
## <a name="remarks"></a>주의  
 *DeleteEncryptionKey* 메서드는 보고서 서버 데이터베이스의 보안 정보에 대한 액세스 권한이 있는 보고서 서버의 키 테이블에서 항목을 삭제합니다. 지정된 *InstallationID* 매개 변수가 데이터베이스의 설치 ID와 일치하지 않으면 메서드에서 오류가 반환됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
