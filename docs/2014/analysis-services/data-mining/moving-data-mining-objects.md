---
title: 데이터 마이닝 개체 이동 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], models
- data mining editor [Analysis Services]
- mining models [Analysis Services], managing
- Data Mining Designer
- mining models [Analysis Services], modifying
ms.assetid: bc108407-2603-4387-b930-b5bb9df78069
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dff20b2b3e273ec0aac653346084f6c2854a8330
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078669"
---
# <a name="moving-data-mining-objects"></a>데이터 마이닝 개체 이동
  데이터 마이닝 개체를 이동하기 위한 가장 일반적인 시나리오는 테스트 또는 분석 환경에서 프로덕션 환경으로 모델을 배포하거나 다른 사용자와 모델을 공유하는 것입니다.  
  
 이 항목에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 제공하는 도구와 스크립트 언어를 사용하여 데이터 마이닝 개체를 이동하는 방법에 대해 설명합니다.  
  
## <a name="moving-data-mining-objects-between-databases-or-servers"></a>데이터베이스 또는 서버 간 데이터 마이닝 개체 이동  
 다음 방법으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 간이나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 간에 데이터 마이닝 개체를 이동할 수 있습니다.  
  
-   다른 데이터베이스에 솔루션을 다시 배포합니다.  
  
-   개별 개체 스크립팅  
  
-   데이터베이스의 복사본을 백업한 다음 복원  
  
-   구조와 모델 내보내기 및 가져오기  
  
 다음 섹션에서는 이러한 옵션에 대해 자세히 설명합니다.  
  
### <a name="deploying"></a>배포  
 다른 서버나 데이터베이스에 솔루션을 배포하려면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 만든 솔루션 파일이 있어야 합니다.  
  
 Analysis Services 솔루션 배포에 대한 자세한 내용은 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)를 참조하세요.  
  
### <a name="scripting"></a>스크립팅  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 은 개체를 스크립팅하는 데 사용할 수 있는 여러 언어를 제공합니다.  
  
-   **XMLA**: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체를 마우스 오른쪽 단추로 클릭하면 XMLA를 사용하여 개체를 스크립팅할 수 있습니다. 스크립트를 실행하려면 대상 서버의 **XMLA 쿼리** 창에서 스크립트를 엽니다.  
  
-   **DMX**: [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 제공하는 템플릿 또는 쿼리 작성기 중 하나를 사용하여 스크립트를 만들 수 있습니다.  
  
 하지만 각 스크립트 언어로 수행할 수 있는 태스크에는 차이가 있습니다.  
  
-   개체 설명 및 데이터 바인딩과 같은 속성은 DMX가 아닌 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 언어를 사용해서만 만들거나 변경할 수 있습니다.  
  
-   DMX만 마이닝 개체의 가져오기 및 내보내기를 지원합니다.  
  
-   DMX만 PMML 생성 또는 PMML에서 모델 정의 가져오기를 지원합니다.  
  
-   DMX만 응용 프로그램 데이터를 사용한 모델 학습을 지원합니다. 또한 DMX INSERT INTO 문은 키 열의 값을 제공하지 않는 모델 학습을 지원합니다.  
  
 자세한 내용은 [ASSL&#40;Analysis Services Scripting Language&#41;을 사용하여 개발](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)을 참조하세요.  
  
### <a name="backup-and-restore"></a>Backup 및 Restore 메서드  
 전체 Analysis Services 데이터베이스의 백업 및 복원은 현재 데이터 마이닝 구조가 OLAP 개체에 의존하는 경우 선택하는 방법입니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 데이터베이스 백업을 더 빠르고 쉽게 할 수 있는 새로운 백업 및 복원 기능을 제공합니다.  
  
 백업에 대한 자세한 내용은 [Analysis Services 데이터베이스 백업 및 복원](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)을 참조하세요.  
  
### <a name="exporting-and-importing"></a>내보내기 및 가져오기  
 DMX 문을 사용하여 마이닝 모델 및 구조를 내보낸 다음 다시 가져오는 것은 개별 관계형 데이터 마이닝 개체를 이동하거나 백업하는 가장 쉬운 방법입니다. 이러한 작업에 사용하는 DMX 구문에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [내보내기 &AMP;#40;DMX&AMP;#41;](/sql/dmx/export-dmx)  
  
-   [가져오기 &AMP;#40;DMX&AMP;#41;](/sql/dmx/import-dmx)  
  
 INCLUDE DEPENDENCIES 옵션을 지정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 필요한 모든 데이터 원본 뷰 정의도 내보내며, 사용자가 모델 또는 구조를 가져올 때 대상 서버에서 데이터 원본 뷰를 다시 생성합니다. 모델 가져오기를 마친 후에는 개체에 대해 필요한 마이닝 사용 권한을 설정해야 합니다.  
  
> [!NOTE]  
>  OLAP 모델은 DMX를 사용하여 내보내고 가져올 수 없습니다. 마이닝 모델이 OLAP 큐브를 기반으로 하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 기능을 사용하여 전체 데이터베이스를 백업한 다음 복원하거나 큐브와 해당 모델을 다시 배포해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 솔루션 및 개체 관리](management-of-data-mining-solutions-and-objects.md)  
  
  
