---
title: DataSources 및 DataSets 컬렉션 참조(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1290f2813d11c53e91dc233c6ffa1c065a824f0f
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295575"
---
# <a name="built-in-collections---datasources-and-datasets-references-report-builder"></a>기본 제공 컬렉션 - DataSources 및 데이터 세트 참조(보고서 작성기)
  **DataSources** 컬렉션은 보고서에 사용되는 모든 데이터 원본을 나타냅니다. 마찬가지로 **DataSets** 컬렉션은 보고서의 모든 데이터 원본에 대한 모든 데이터 세트를 나타냅니다. **보고서 데이터** 창을 사용하여 참조하는 데이터 원본 아래에 구성된 보고서 데이터 세트를 계층적으로 볼 수 있습니다. 이러한 컬렉션에 대한 참조를 추가할 경우 보고서를 미리 볼 때 값이 표시되지 않습니다. 이러한 컬렉션은 보고서가 보고서 서버에 게시된 다음에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 **DataSources** 컬렉션은 게시된 보고서 정의에 참조되는 데이터 원본을 나타냅니다. 이 정보를 보고서에 포함하도록 선택하여 보고서 데이터의 원본을 문서화할 수 있습니다. 이 컬렉션은 **미리 보기** 모드에서는 사용할 수 없습니다. 다음 표에서는 **DataSources** 컬렉션 내의 변수를 설명합니다.  
  
|**변수**|**형식**|**설명**|  
|------------------|--------------|---------------------|  
|**DataSourceReference**|**String**|보고서 서버에 있는 데이터 원본 정의의 전체 경로입니다. 예를 들어 보고서 기록의 일부로 보고서에 사용된 모든 데이터 원본 목록을 포함할 수 있습니다. 다음 예에서는 AdventureWorks2012라는 데이터 원본의 전체 경로를 보여 줍니다.<br /><br /> `/DataSources/AdventureWorks2012`.|  
|**형식**|**String**|데이터 원본의 데이터 공급자 유형입니다. `SQL`)을 입력합니다.|  
  
## <a name="datasets"></a>DataSets  
 **DataSets** 컬렉션은 보고서 정의에 참조되는 데이터 세트를 나타냅니다. 보고서에 입력란으로 쿼리를 포함하면 보고서에 정확히 어떤 데이터가 있는지 알고자 하는 사용자가 원본 명령 텍스트를 볼 수 있습니다. 이 컬렉션은 **미리 보기** 모드에서는 사용할 수 없습니다. 다음 표에서는 **DataSets** 컬렉션의 멤버를 설명합니다.  
  
|**멤버**|**형식**|**설명**|  
|----------------|--------------|---------------------|  
|**CommandText**|**String**|데이터베이스 데이터 원본의 경우 이 멤버는 데이터 원본에서 데이터를 검색하는 데 사용되는 쿼리입니다. 쿼리가 식인 경우 이 멤버는 평가 식입니다.|  
|**RewrittenCommandText**|**String**|데이터 공급자의 확장 CommandText 값입니다. 일반적으로 이 값은 보고서 매개 변수에 매핑된 쿼리 매개 변수가 있는 보고서에 사용됩니다. 데이터 공급자는 명령 텍스트 매개 변수 참조를 매핑된 보고서 매개 변수에 대해 선택된 상수 값으로 확장할 때 이 속성을 설정합니다.|  
  
### <a name="using-query-expressions"></a>쿼리 식 사용  
 식을 사용하여 데이터 세트에 포함된 쿼리를 정의할 수 있습니다. 이 기능을 사용하면 사용자의 입력, 다른 데이터 세트의 데이터 또는 다른 변수를 기반으로 쿼리가 변경되는 보고서를 디자인할 수 있습니다. 쿼리에 대한 자세한 내용은 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
