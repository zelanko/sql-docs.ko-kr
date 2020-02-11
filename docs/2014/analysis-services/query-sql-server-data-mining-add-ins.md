---
title: 쿼리 (SQL Server 데이터 마이닝 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [data mining]
- Data Mining Query Advanced Editor
- query builder [data mining]
- DMX
ms.assetid: 16af4a6f-18d4-496a-a304-7a13aa32ee76
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dcddeb64b14301f08a7dc723ef89737102f257ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070476"
---
# <a name="query-sql-server-data-mining-add-ins"></a>쿼리(SQL Server 데이터 마이닝 추가 기능)
  ![데이터 마이닝 리본, 모델 쿼리 단추](media/dmc-query.gif "데이터 마이닝 리본, 모델 쿼리 단추")  
  
 
  **쿼리** 마법사를 사용하여 기존 마이닝 모델과의 상호 작용을 통해 Excel 테이블, Excel 범위 또는 다른 데이터 원본에 있는 데이터를 기반으로 예측을 만들 수 있습니다. 추세 예측을 위해 새 데이터를 기존 모델에 적용하는 프로세스를 *예측 쿼리*라고 합니다.  
  
 또한 **쿼리** 마법사는 데이터 마이닝 모델 만들기 또는 수정, 사용자 지정 쿼리 생성, 다른 도구에서 지원되지 않는 구조(예: 중첩된 데이터 세트) 사용을 위한 고급 편집기를 제공합니다.  
  
-   텍스트 편집기를 사용 하 여 다른 곳에서 만든 DMX (Data 마이닝 확장) 문에 입력 하거나 붙여 넣습니다.  
  
-   대화형 쿼리 작성기를 사용하여 템플릿과 대화 상자를 통해 사용자 지정 DMX 문을 작성합니다.  
  
-   DMX 문을 만들어 마이닝 모델과 구조를 관리하거나 백업합니다.  
  
## <a name="using-the-query-wizard"></a>쿼리 마법사 사용  
  
1.  먼저 입력으로 사용할 데이터 원본을 지정해야 합니다. 기존 Excel 테이블 또는 범위에 있는 데이터를 사용하거나 SQL 문을 지정하여 데이터를 검색할 수 있습니다.  
  
2.  그러면 마법사는 연결된 서버에 있는 데이터 마이닝 모델 목록을 제공합니다. 원하는 모델을 알고 있고 데이터 마이닝에 익숙하다면 **고급** 을 클릭하여 **데이터 마이닝 고급 쿼리 편집기**를 열 수 있습니다.  
  
3.  선택한 모델 유형에 따라 평가할 데이터가 포함된 열을 지정하고 입력 데이터 열과 모델 열 간의 매핑을 정의해야 합니다. 선택한 알고리즘에 따라 모델의 다른 속성을 설정할 수 있습니다.  
  
4.  마지막으로 마법사는 하나 이상의 예측을 선택하고 결과를 저장할 대상을 지정하는 능력을 제공합니다.  
  
 언제든지 **고급** 을 클릭하여 DMX 문의 각 부분을 더 세부적으로 제어할 수 있는 **데이터 마이닝 고급 쿼리 편집기**로 전환할 수 있습니다. 고급 쿼리 편집 도구를 사용 하는 방법에 대 한 자세한 내용은 [고급 데이터 마이닝 쿼리 편집기](advanced-data-mining-query-editor.md)를 참조 하십시오.  
  
### <a name="requirements"></a>요구 사항  
 
  **쿼리** 마법사를 사용하려면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 연결되어 있어야 합니다. 또한 서버에는 적절한 유형의 데이터 마이닝 모델이 최소 한 개 이상 있어야 합니다. 사용할 수 있는 마이닝 모델이 없는 경우 Excel용 데이터 마이닝 클라이언트에서 제공하는 마법사를 사용하여 만들 수 있습니다. 마법사를 사용 하 여 새 마이닝 모드를 만드는 방법에 대 한 자세한 내용은 [데이터 마이닝 모델 만들기](creating-a-data-mining-model.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Excel 용 데이터 마이닝 추가 기능 &#40;마이닝 모델 배포 및 확장&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   
 [Excel 용 데이터 마이닝 클라이언트 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
  
