---
title: SecureConnectionLevel 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fdb8fc97b8b2403366e19456b7c744012ee9007f
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570258"
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>ConfigurationSetting 속성 - SecureConnectionLevel
  RSReportServer.config 파일에 지정된 보안 연결 수준을 반환합니다. 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>속성 값  
 보안 연결 수준을 나타내는 **Integer** 값입니다. 반환 값은 SSL이 구성되어 있는지 여부를 나타냅니다. 값이 1보다 크거나 같으면 SSL이 설정되어 있음을 나타냅니다. 값이 0이면 SSL이 해제되어 있음을 나타냅니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks

SQL Server 2008 R2에서 SecureConnectionLevel은 설정/해제가 전환됩니다. 자세한 내용은 [ConfigurationSetting 메서드 - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)을 참조하세요.

## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
