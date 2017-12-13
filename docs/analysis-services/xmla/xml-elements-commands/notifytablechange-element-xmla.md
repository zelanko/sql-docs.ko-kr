---
title: "NotifyTableChange 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: NotifyTableChange Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords: NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 66d277cd3bff3c0dfbb8ea95d0ac6ca76be20f78
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="notifytablechange-element-xmla"></a>NotifyTableChange 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]인스턴스를에 알립니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 의 지정된 된 데이터 원본의 테이블에 변경 내용이 발생 하는 합니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **NotifyTableChange** 명령을 명시적으로 알려야 하는 클라이언트 응용 프로그램을 사용 하면는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 하나 인스턴스 또는 데이터 원본에 포함 된 테이블을 더 변경 되었습니다. 자동 관리 캐싱의 경우 이 알림은 해당 테이블을 기반으로 한 ROLAP(관계형 OLAP) 개체를 검토 및 업데이트해야 함을 나타냅니다.  
  
 이 알림 방법은 변경 사항 검색 및 추적이 어려운 데이터 원본 뷰에 정의된 명명된 쿼리 또는 뷰를 기반으로 하는 ROLAP 개체에서 사용하기에 좋습니다.  
  
 **개체** 요소에서 데이터 원본을 참조 해야는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스입니다. **Object** 요소가 데이터 원본 이외의 개체를 참조하면 오류가 발생합니다.  
  
 자동 관리 캐싱에 대한 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [명령 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
