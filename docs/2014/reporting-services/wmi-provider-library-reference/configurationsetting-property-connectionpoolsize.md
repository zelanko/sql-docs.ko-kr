---
title: ConnectionPoolSize 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- ConnectionPoolSize
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ConnectionPoolSize property
ms.assetid: b80c8e5d-b725-4fe4-aec6-02fb18ec4434
caps.latest.revision: 17
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 0d534e8fd5435cd26b72a37649afed12411362d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091439"
---
# <a name="connectionpoolsize-property-wmi-msreportserverconfigurationsetting"></a>ConnectionPoolSize 속성(WMI MSReportServer_ConfigurationSetting)
  보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 통신하기 위해 보고서 서버에서 사용하는 연결 풀 크기입니다. 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim ConnectionPoolSize As UInt32  
```  
  
```csharp  
public UInt32 ConnectionPoolSize;  
```  
  
## <a name="property-values"></a>속성 값  
 읽기 전용 **정수** 개체의 값을 반환 하는 `768`합니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  