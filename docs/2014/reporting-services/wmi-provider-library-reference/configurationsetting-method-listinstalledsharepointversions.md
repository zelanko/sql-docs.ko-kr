---
title: ListInstalledSharePointVersions 메서드(WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListInstalledSharePointVersions method
ms.assetid: 8f0a5e9f-23f1-41e5-9a90-dfec19ef1df7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 28c42910b72e36c046d5ef75c574b9c4506c006c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024104"
---
# <a name="listinstalledsharepointversions-method-wmi"></a>ListInstalledSharePointVersions 메서드(WMI)
  보고서 서버와 같은 컴퓨터에 설치되어 있는 Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 버전을 나타내는 토큰 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub ListInstalledSharePointVersions(ByRef VersionTokens() _  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] VersionTokens,   
    out Int32 Length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *VersionTokens[]*  
 [out] 설치된 보고서 서버와 호환되는 SharePoint 제품 또는 기술의 버전을 나타내는 토큰이 들어 있는 배열입니다.  
  
 *길이*  
 [out] 버전 토큰 배열의 길이입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 반환되는 각 토큰은 현재 설치되어 있는 보고서 서버와 호환되는 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 또는 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 버전을 나타냅니다. 특정 버전의 SharePoint가 이전 SharePoint 버전과 호환되는 경우 호환되는 각 SharePoint 버전에 대한 토큰이 반환됩니다.  
  
 다음 표에서는 반환되는 SharePoint 토큰을 보여 줍니다.  
  
|**버전 토큰**|**설명**|  
|------------------------|---------------------|  
|WSS_V2_Compatible|[!INCLUDE[winSPServ](../../includes/winspserv-md.md)]2.0과 호환되는 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 또는 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 설치 프로그램이 설치되어 있습니다.|  
|WSS_V3_Compatible|[!INCLUDE[winSPServ](../../includes/winspserv-md.md)]3.0과 호환되는 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 또는 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 이 설치되어 있습니다.|  
|WSS_V4_Compatible|Office 14와 호환되는 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 이 설치되어 있습니다.|  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
