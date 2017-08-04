---
title: "Union All 변환을 사용 하 여 데이터 병합 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merging datasets [Integration Services]
- merging inputs [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 78304403-a81c-4101-b87e-ec80ddfdac98
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b2f9933f48083b0849ba01312979911bacb4fd86
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="merge-data-by-using-the-union-all-transformation"></a>UNION ALL 변환을 사용하여 데이터 병합
  UNION ALL 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 두 개의 데이터 원본이 이미 들어 있어야 합니다.  
  
 UNION ALL 변환은 여러 입력을 조합합니다. 변환에 연결된 첫 번째 입력은 참조 입력이며 이후에 연결되는 입력은 보조 입력입니다. 출력에는 참조 입력에 있는 열이 포함됩니다.  
  
### <a name="to-combine-inputs-in-a-data-flow"></a>데이터 흐름에서 입력을 조합하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 패키지를 두 번 클릭하여 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 패키지를 연 후 **데이터 흐름** 탭을 클릭합니다.  
  
2.  **도구 상자**에서 UNION ALL 변환을 **데이터 흐름** 탭의 디자인 화면으로 끌어 옵니다.  
  
3.  데이터 원본이나 이전 변환에서 연결선을 UNION ALL 변환으로 끌어서 UNION ALL 변환을 데이터 흐름에 연결합니다.  
  
4.  UNION ALL 변환을 두 번 클릭합니다.  
  
5.  **UNION ALL 변환 편집기**에서 행을 클릭하여 입력의 열을 **출력 열 이름** 목록의 열로 매핑한 후 입력 목록에서 열을 선택합니다. 선택  **\<무시 >** 입력 목록의 열 매핑을 건너 뜁니다.  
  
    > [!NOTE]  
    >  두 열을 매핑하려면 해당 열의 메타데이터가 일치해야 합니다.  
  
    > [!NOTE]  
    >  참조 열로 매핑되지 않은 보조 입력의 열은 출력에서 Null 값으로 설정됩니다.  
  
6.  선택적으로 **출력 열 이름** 열에서 열의 이름을 수정합니다.  
  
7.  각 입력에 있는 각 열에 대해 5와 6단계를 반복합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Union All 변환](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](../../../integration-services/data-flow/integration-services-paths.md)   
 [데이터 흐름 태스크](../../../integration-services/control-flow/data-flow-task.md)  
  
  
