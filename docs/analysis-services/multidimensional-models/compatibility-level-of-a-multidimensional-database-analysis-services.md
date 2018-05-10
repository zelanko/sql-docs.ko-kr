---
title: (Analysis Services)는 다차원 데이터베이스의 호환성 수준을 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b25211d1eeacdbc09f4508aede2181c96a428e4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="compatibility-level-of-a-multidimensional-database-analysis-services"></a>다차원 데이터베이스의 호환성 수준(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 데이터베이스 호환성 수준 속성은 데이터베이스의 기능 수준을 결정합니다. 호환성 수준은 각 모델 유형에 고유합니다. 예를 들어 호환성 수준 **1100** 은 다차원 데이터베이스인지 테이블 형식 데이터베이스인지에 따라 의미가 달라집니다.  
  
 이 항목에서는 다차원 데이터베이스의 호환성 수준에 대해서만 설명합니다. 테이블 형식 솔루션에 대한 자세한 내용은 [Analysis Services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)을 참조하세요.  
  
> [!NOTE]  
>  테이블 형식 모델은 다차원 모델에 적용되지 않는 추가 데이터베이스 호환성 수준이 있습니다. 호환성 수준 **1103** 은 다차원 모델에 없습니다. 테이블 형식 솔루션의 [1103](http://go.microsoft.com/fwlink/?LinkId=301727) 에 대한 자세한 내용은 **SQL Server 2012 SP1 및 호환성 수준에서 테이블 형식 모델의 새로운 기능** 을 참조하세요.  
  
 **다차원 데이터베이스의 호환성 수준**  
  
 현재 기능 수준에 따라 달라지는 다차원 데이터베이스 동작은 문자열 저장소 아키텍처뿐입니다. 데이터베이스 호환성 수준을 높여 측정값 및 차원의 문자열 저장소에 대한 4GB 최대 제한을 재정의할 수 있습니다.  
  
 다차원 데이터베이스에 대해 유효한 **CompatibilityLevel** 속성 값은 다음과 같습니다.  
  
|설정|Description|  
|-------------|-----------------|  
|**1050**|이 값은 스크립트나 도구에 표시되지 않지만 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]또는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서 만든 데이터베이스에 해당됩니다. **CompatibilityLevel** 이 명시적으로 설정되지 않은 모든 데이터베이스는 **1050** 수준에서 암시적으로 실행됩니다.|  
|**1100**|이 값은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 만드는 새 데이터베이스의 기본값입니다. 이 호환성 수준에서만 지원되는 기능(즉, 차원 특성의 증가된 문자열 저장소 또는 문자열 데이터가 포함된 고유 카운트 측정값)을 사용할 수 있도록 이전 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 만든 데이터베이스에 대해 이 값을 지정할 수도 있습니다.<br /><br /> **CompatibilityLevel** 을 **1100** 으로 설정한 데이터베이스에서는 파티션 및 차원에 대한 대체 문자열 저장소를 선택할 수 있는 **StringStoresCompatibilityLevel**추가 속성을 가져옵니다.|  
  
> [!WARNING]  
>  데이터베이스 호환성 수준을 더 높여서 설정하는 경우 되돌릴 수 없습니다. 호환성 수준을 **1100**으로 높인 후에는 계속하여 최신 서버에서 데이터베이스를 실행해야 합니다. **1050**으로 롤백할 수 없습니다. **또는** 미만의 서버 버전에서는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 1100 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]데이터베이스를 연결하거나 복원할 수 없습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 데이터베이스 호환성 수준은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 도입되었습니다. 데이터베이스 호환성 수준을 보거나 설정하려면 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이상이 있어야 합니다.  
  
 데이터베이스는 로컬 큐브일 수 없습니다. 로컬 큐브는 **CompatibilityLevel** 속성을 지원하지 않습니다.  
  
 데이터베이스가 이전 릴리스(SQL Server 2008 R2 이하)에서 만들어진 다음 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이상인 서버로 연결되거나 복원되었어야 합니다. SQL Server 2012에 배포된 데이터베이스는 이미 **1100** 이며 다운그레이드하여 하위 수준에서 실행할 수 없습니다.  
  
## <a name="determine-the-existing-database-compatibility-level-for-a-multidimensional-database"></a>다차원 데이터베이스에 대한 기존 데이터베이스 호환성 수준을 결정합니다.  
 데이터베이스 호환성 수준은 XMLA를 통해서만 보거나 수정할 수 있습니다. SQL Server Management Studio에서 데이터베이스를 지정하는 XMLA 스크립트를 보거나 수정할 수 있습니다.  
  
 **CompatibilityLevel** 속성에 대한 데이터베이스의 XMLA 정의를 검색했지만 그 결과가 없는 경우 **1050** 수준의 데이터베이스가 있을 가능성이 가장 높습니다.  
  
 XMLA 스크립트 보기 및 수정에 대한 지침은 다음 섹션에서 제공됩니다.  
  
## <a name="set-the-database-compatibility-level-in-sql-server-management-studio"></a>SQL Server Management Studio에서 데이터베이스 호환성 수준 설정  
  
1.  나중에 변경 내용을 되돌릴 경우에 대비하여 호환성 수준을 올리기 전에 데이터베이스를 백업합니다.  
  
2.  SQL Server Management Studio를 사용하여 데이터베이스를 호스팅하는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에 연결합니다.  
  
3.  데이터베이스 이름을 마우스 오른쪽 단추로 클릭하고 **데이터베이스 스크립팅**, **ALTER**를 차례로 가리킨 다음 **새 쿼리 편집기 창**을 선택합니다. 데이터베이스의 XMLA 표현이 새 창에서 열립니다.  
  
4.  다음 XML 요소를 복사합니다.  
  
    ```  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    ```  
  
5.  `</Annotations>` 닫는 요소 뒤와 `<Language>` 요소 앞에 붙여넣습니다. XML은 다음 예와 비슷해야 합니다.  
  
    ```  
    </Annotations>  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    <Language>1033</Language>  
    ```  
  
6.  파일을 저장합니다.  
  
7.  스크립트를 실행하려면 쿼리 메뉴에서 **실행** 을 클릭하거나 F5 키를 누릅니다.  
  
## <a name="supported-operations-that-require-the-same-compatibility-level"></a>지원되는 작업 중 호환성 수준이 같아야 하는 작업  
 다음 작업의 경우 원본 데이터베이스의 호환성 수준이 같아야 합니다.  
  
1.  다른 데이터베이스에서 파티션을 병합하는 경우 두 데이터베이스의 호환성 수준이 같아야 합니다.  
  
2.  다른 데이터베이스의 연결된 차원을 사용하려면 호환성 수준이 같아야 합니다. 예를 들어 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 데이터베이스에서 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 데이터베이스의 연결된 차원을 사용하려면 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 데이터베이스를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 서버로 포팅하고 호환성 수준을 **1100**으로 설정해야 합니다.  
  
3.  서버 동기화는 동일한 버전과 데이터베이스 호환성 수준을 공유하는 서버에 대해서만 지원됩니다.  
  
## <a name="next-steps"></a>다음 단계  
 데이터베이스 호환성 수준을 높인 후 **에서** StringStoresCompatibilityLevel [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]속성을 설정할 수 있습니다. 그러면 측정값 및 차원에 대한 문자열 저장소가 증가합니다. 이 기능에 대한 자세한 내용은 [차원 및 파티션에 대한 문자열 저장소 구성](../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 백업, 복원 및 동기화&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
