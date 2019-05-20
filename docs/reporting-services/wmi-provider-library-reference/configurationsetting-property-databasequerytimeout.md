---
title: DatabaseQueryTimeout 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseQueryTimeout Property
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8149c0954195796ce71a48e022a2f7bc83471601
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65573588"
---
# <a name="configurationsetting-property---databasequerytimeout"></a>ConfigurationSetting 속성 - DatabaseQueryTimeout
  보고서 서버에서 명령이 실패하거나 수행 시간이 너무 오래 걸린다고 간주하기 전에 경과해야 하는 시간(초)를 지정합니다. 보고서 서버는 보고서의 데이터 원본이 아닌 SQL 카탈로그에 대해 쿼리 시간을 계산합니다. 읽기/쓰기입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>속성 값  
 쿼리를 실행할 수 있는 시간(초)을 나타내는 부호 없는 32비트 **정수** 개체입니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
