---
title: 마이닝 구조에서 마이닝 모델 삭제 | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b17489213e0f057d8f291095f01b65f97a977ff1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019320"
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>마이닝 구조에서 마이닝 모델 삭제
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터 마이닝 디자이너, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 DMX 문을 사용하여 마이닝 모델을 삭제할 수 있습니다.  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>SQL Server Data Tools를 사용하여 마이닝 모델 삭제  
  
1.  **에서** 마이닝 모델 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭을 선택합니다.  
  
2.  삭제할 모델을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
     **개체 삭제** 대화 상자가 열립니다.  
  
3.  **확인**을 클릭합니다.  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 마이닝 모델 삭제  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 모델이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 엽니다.  
  
2.  **마이닝 구조**를 확장하고 **마이닝 모델**을 확장합니다.  
  
3.  삭제할 모델을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
     모델을 삭제해도 학습 데이터는 삭제되지 않고 모델을 학습할 때 메타데이터 및 패턴만 삭제됩니다.  
  
### <a name="delete-a-mining-model-using-dmx"></a>DMX를 사용하여 마이닝 모델 삭제  
  
-   [마이닝 모델 삭제 & #40; DMX & #41;](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 태스크 및 방법](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
