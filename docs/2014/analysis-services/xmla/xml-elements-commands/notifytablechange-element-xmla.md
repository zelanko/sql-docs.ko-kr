---
title: NotifyTableChange 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- NotifyTableChange Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords:
- NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 612738591115a2e7af964ba4ee5d9950587e45bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37203903"
---
# <a name="notifytablechange-element-xmla"></a>NotifyTableChange 요소(XMLA)
  인스턴스에 알립니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 지정 된 데이터 원본의 테이블이 변경 발생 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <NotifyTableChange>  
      <Object>...</Object>  
      <TableNotifications>...</TableNotifications>  
   </NotifyTableChange>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../xml-elements-properties/object-element-xmla.md), [TableNotifications](../xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `NotifyTableChange` 명령을 사용하면 클라이언트 응용 프로그램이 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 데이터 원본에 포함된 하나 이상의 테이블이 변경되었음을 알릴 수 있습니다. 자동 관리 캐싱의 경우 이 알림은 해당 테이블을 기반으로 한 ROLAP(관계형 OLAP) 개체를 검토 및 업데이트해야 함을 나타냅니다.  
  
 이 알림 방법은 변경 사항 검색 및 추적이 어려운 데이터 원본 뷰에 정의된 명명된 쿼리 또는 뷰를 기반으로 하는 ROLAP 개체에서 사용하기에 좋습니다.  
  
 `Object` 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스의 데이터 원본을 참조해야 합니다. `Object` 요소가 데이터 원본 이외의 개체를 참조하면 오류가 발생합니다.  
  
 자동 관리 캐싱에 대한 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](../../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
