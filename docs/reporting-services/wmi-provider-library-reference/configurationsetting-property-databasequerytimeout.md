---
title: "DatabaseQueryTimeout 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
apiname: DatabaseQueryTimeout Property
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
caps.latest.revision: "35"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8c56a5f4102236affc6860aea200857509d4e2af
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
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
  
## <a name="see-also"></a>관련 항목:  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
