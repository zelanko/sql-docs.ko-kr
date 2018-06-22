---
title: 레코드 집합 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.recordsetdest.f1
helpviewer_keywords:
- Recordset destination
- ADO recordsets [Integration Services]
- destinations [Integration Services], Recordset
- in-memory ADO recordsets [Integration Services]
ms.assetid: be973cf1-c4ff-49f8-987e-314c08ef98e4
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: bedd18c7aa79420c23c935058e4b23d584b6fa1a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081146"
---
# <a name="recordset-destination"></a>레코드 집합 대상
  레코드 집합 대상은 메모리 내 ADO 레코드 집합을 만들고 채웁니다. 레코드 집합의 모양은 디자인 타임에 레코드 집합 대상에 대한 입력에 의해 정의됩니다.  
  
## <a name="configuration-of-the-recordset-destination"></a>레코드 집합 대상 구성  
 레코드 집합 대상은 ADO 레코드 집합에 저장되는 변수를 지정하여 구성됩니다.  
  
 런타임 시 ADO 레코드 집합은 레코드 집합 대상의 VariableName 속성에 지정된 개체 유형의 변수에 기록됩니다. 그런 다음 이 변수를 통해 데이터 흐름 외부의 스크립트 및 다른 패키지 요소에서 레코드 집합을 사용할 수 있습니다.  
  
 이 원본에는 하나의 입력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../common-properties.md)  
  
-   [레코드 집합 대상 사용자 지정 속성](recordset-destination-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [레코드 집합 대상 사용](recordset-destination.md)  
  
  