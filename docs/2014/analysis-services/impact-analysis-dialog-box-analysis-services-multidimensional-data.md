---
title: 영향 분석 대화 상자 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.impactanalysisdialog.f1
ms.assetid: 208268eb-4e14-44db-9c64-6f74b776adb6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0c08690cd2f5b77471392cab3aad1587b4cb0f9a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080748"
---
# <a name="impact-analysis-dialog-box-analysis-services---multidimensional-data"></a>영향 분석 대화 상자(Analysis Services - 다차원 데이터)
  **및** 의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 영향 분석 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하면 **처리** 대화 상자에 나열된 개체를 처리하는 경우 영향을 받는 종속 개체를 식별하고 선택적으로 처리할 수 있습니다. **영향 분석** 대화 상자는 **처리** 대화 상자에서 **영향 분석** 을 클릭하여 표시할 수 있습니다.  
  
> [!NOTE]  
>  두 가지 이상의 방식으로 영향을 받을 경우 한 개체가 두 번 이상 표시됩니다.  
  
## <a name="options"></a>변수  
 **개체 목록**  
 종속 개체 목록을 표에 표시합니다. 표에는 다음 열이 있습니다.  
  
 **개체 이름**  
 처리해야 하는 종속 개체의 이름을 표시합니다. 이름 왼쪽에 있는 아이콘은 개체 유형을 나타냅니다.  
  
 **형식**  
 처리해야 하는 종속 개체의 유형을 표시합니다.  
  
 **영향 유형**  
 **처리** 대화 상자에서 개체를 처리할 경우 종속 개체에 미치는 영향을 표시합니다. 다음 표에서는 처리 시 발생 가능한 영향을 나열하고 각 영향의 결과로 발생하는 경고 또는 오류를 표시합니다.  
  
|영향|메시지|  
|------------|-------------|  
|개체가 삭제됨(처리되지 않음)|경고|  
|개체가 유효하지 않음|Error|  
|집계가 삭제됨|경고|  
|융통성 있는 집계가 삭제됨|경고|  
|인덱스가 삭제됨|경고|  
|자식이 아닌 개체가 처리됨|경고|  
  
 **프로세스 개체**  
 처리 작업으로 처리할 종속 개체를 선택합니다. 선택하지 않은 종속 개체는 처리 작업이 완료된 후 처리해야 합니다. 그렇지 않으면 해당 개체를 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [처리 대화 상자 &#40;Analysis Services-다차원 데이터&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
