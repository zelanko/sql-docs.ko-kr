---
title: 마이닝 모델을 처리 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0fd3f0ad2566a8907ea5fb18d00782eb8a6f35d4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="process-a-mining-model"></a>마이닝 모델 처리
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에 있는 데이터 마이닝 디자이너의 마이닝 모델 탭에서는 마이닝 구조와 연관된 특정 마이닝 모델을 처리하거나 구조와 연관된 모든 모델을 처리할 수 있습니다.  
  
 다음 도구를 사용하여 마이닝 모델을 처리할 수 있습니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 XMLA Process 명령도 사용할 수 있습니다. 자세한 내용은 [도구 및 처리 접근 방법&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)을 참조하세요.  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>SQL Server Data Tools를 사용하여 단일 마이닝 모델 처리  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 표에 있는 하나 이상의 모델 열에서 마이닝 모델을 선택합니다.  
  
2.  **마이닝 모델** 메뉴에서 **모델 처리**를 선택합니다.  
  
     마이닝 구조를 변경한 경우 모델을 처리하기 전에 구조를 다시 배포할지 묻는 메시지가 표시됩니다. **예**를 클릭합니다.  
  
3.  에 **마이닝 모델 처리- \<모델 >** 대화 상자를 클릭 **실행**합니다.  
  
     **처리 진행률** 대화 상자가 열리고 모델 처리 세부 정보를 표시합니다.  
  
4.  모델이 성공적으로 처리되면 **처리 진행률** 대화 상자에서 **닫기** 를 클릭합니다.  
  
5.  클릭 **닫기** 에 **마이닝 모델 처리- \<모델 >** 대화 상자.  
  
 마이닝 구조 및 선택한 마이닝 모델만 처리되었습니다.  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>마이닝 구조와 연관된 모든 마이닝 모델 처리  
  
1.  데이터 마이닝 디자이너에 있는 **마이닝 모델** 탭의 **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리** 를 선택합니다.  
  
2.  마이닝 구조를 변경한 경우 모델을 처리하기 전에 구조를 다시 배포할지 묻는 메시지가 표시됩니다. **예**를 클릭합니다.  
  
3.  에 **마이닝 구조 처리- \<구조 >** 대화 상자를 클릭 **실행**합니다.  
  
4.  **처리 진행률** 대화 상자가 열리고 모델 처리 세부 정보를 표시합니다.  
  
5.  모델이 성공적으로 처리되면 **처리 진행률** 대화 상자에서 **닫기** 를 클릭합니다.  
  
6.  클릭 **닫기** 에 **처리 \<모델 >** 대화 상자.  
  
 마이닝 구조 및 모든 연관된 마이닝 모델이 처리되었습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 태스크 및 방법](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
