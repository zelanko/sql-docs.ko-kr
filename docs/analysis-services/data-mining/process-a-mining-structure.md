---
title: 마이닝 구조 처리 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9cb977ace8ccd1856d9a08c8eeaa2cf698637e68
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="process-a-mining-structure"></a>마이닝 구조 처리
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  마이닝 구조와 연결된 마이닝 모델을 검색하거나 사용하려면 먼저 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 배포하고 마이닝 구조와 마이닝 모델을 처리해야 합니다. 마이닝 구조나 마이닝 모델을 변경하는 경우 이를 다시 배포하고 처리하라는 메시지가 나타납니다. **의 데이터 마이닝 디자이너에 있는** 마이닝 구조 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 탭에서 구조를 처리하면 연결된 모델이 모두 처리됩니다.  
  
 다음 도구를 사용하여 마이닝 구조를 처리할 수 있습니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA: Process 명령  
  
 개별 모델을 처리하는 방법에 대한 자세한 내용은 [마이닝 모델 처리](../../analysis-services/data-mining/process-a-mining-model.md)를 참조하세요.  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>SQL Server Data Tools를 사용하여 마이닝 구조와 연결된 마이닝 모델을 모두 처리하려면  
  
1.  **의** 마이닝 모델 **메뉴 항목에서** 마이닝 구조 및 모든 모델 처리 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 선택합니다.  
  
     구조를 변경하는 경우 모델을 처리하기 전에 구조를 다시 배포하라는 메시지가 나타납니다. **예**를 클릭합니다.  
  
2.  클릭 **실행** 에 **마이닝 구조 처리- \<구조 >** 대화 상자.  
  
     **처리 진행률** 대화 상자가 열리고 모델 처리 세부 정보를 표시합니다.  
  
3.  모델 처리가 완료되면 **처리 진행률** 대화 상자에서 **닫기** 를 클릭합니다.  
  
4.  클릭 **닫기** 에 **마이닝 구조 처리- \<구조 >** 대화 상자.  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 구조 태스크 및 방법](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
