---
title: DatabaseQueryTimeout 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseQueryTimeout Property
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2e92e3e0f6752ea99fe89c962ebe96e343c0195b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66097749"
---
# <a name="databasequerytimeout-property-wmi-msreportserverconfigurationsetting"></a>DatabaseQueryTimeout 속성(WMI MSReportServer_ConfigurationSetting)
  보고서 서버에서 명령이 실패하거나 수행 시간이 너무 오래 걸린다고 간주하기 전에 경과해야 하는 시간(초)를 지정합니다. 보고서 서버는 보고서의 데이터 원본이 아닌 SQL 카탈로그에 대해 쿼리 시간을 계산합니다. 읽기/쓰기입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>속성 값  
 쿼리를 실행할 수 있는 시간(초)을 나타내는 부호 없는 32비트 `integer` 개체입니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
