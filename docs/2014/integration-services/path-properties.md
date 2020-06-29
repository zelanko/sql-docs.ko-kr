---
title: 경로 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- paths [Integration Services], properties
ms.assetid: 89b1e347-9579-4f6b-af74-c6519ea08eea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca263b866fb6d5d7ceb6352f708f387d79cad4f7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423470"
---
# <a name="path-properties"></a>경로 속성
  개체 모델의 데이터 흐름 개체에는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 구성 요소 수준, 입/출력, 입력 열 및 출력 열 수준에서 공통 속성과 사용자 지정 속성이 있습니다. 많은 속성은 데이터 흐름 엔진이 런타임에 할당하는 읽기 전용 값을 갖습니다.  
  
 이 항목은 데이터 흐름 개체를 연결하는 경로의 사용자 지정 속성을 나열하고 설명합니다.  
  
## <a name="path-properties"></a>경로 속성  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체 모델에서 데이터 흐름 구성 요소를 연결하는 경로는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 인터페이스를 구현합니다.  
  
 다음 표에서는 데이터 흐름 경로의 구성 가능한 속성에 대해 설명합니다. 데이터 흐름 엔진은 여기에 나열되지 않은 추가 읽기 전용 속성에도 값을 할당합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Integer(열거형)|디자이너 화면에 주석을 경로와 함께 표시할지 여부를 나타내는 값입니다. 가능한 값은 `AsNeeded`, `SourceName`, `PathName` 및 `Never`입니다. 기본값은 `AsNeeded`입니다.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|경로에 연결된 입력입니다.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|경로에 연결된 출력입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 경로](data-flow/integration-services-paths.md)   
 [공용 속성](../../2014/integration-services/common-properties.md)   
 [변환 사용자 지정 속성](data-flow/transformations/transformation-custom-properties.md)   
 [식을 사용하여 설정할 수 있는 데이터 흐름 속성](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
