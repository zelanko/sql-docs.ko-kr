---
title: XMLA를 사용 하 여 데이터 마이닝 쿼리 만들기 | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8732b3f366d5805f6321b4e07fe0de1dbc73fb42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-data-mining-query-by-using-xmla"></a>XMLA를 사용하여 데이터 마이닝 쿼리 만들기
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  AMO, DMX 또는 XML/A를 사용하여 데이터 마이닝 개체에 대한 다양한 쿼리를 만들 수 있습니다.  
  
 XML은 Analysis Services 서버와 모든 클라이언트 간의 통신에 사용됩니다. 따라서 일반적으로 DMX를 사용하면 내용 쿼리를 보다 쉽게 만들 수 있지만 SOAP 프로토콜을 지원하는 클라이언트를 사용하거나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 XML/A 쿼리를 만들어 XML/A의 DISCOVER 및 COMMAND 문을 통해 쿼리를 작성할 수도 있습니다.  
  
 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 사용할 수 있는 XML/A 템플릿을 사용하여 현재 서버에 저장된 마이닝 모델에 대한 모델 내용 쿼리를 만드는 방법을 설명합니다.  
  
## <a name="querying-data-mining-schema-rowsets-by-using-xmla"></a>XML/A를 사용하여 데이터 마이닝 스키마 행 집합 쿼리  
  
#### <a name="to-open-an-xmla-template"></a>XML/A 템플릿을 열려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **템플릿 탐색기**를 클릭합니다.  
  
2.  큐브 아이콘을 클릭하여 Analysis Services 템플릿 목록을 엽니다.  
  
3.  템플릿 범주 목록에서 **XMLA**, **스키마 행 집합**을 차례로 확장하고 **스키마 행 집합 검색** 을 두 번 클릭하여 해당 템플릿을 적절한 코드 편집기에서 엽니다.  
  
4.  **Analysis Services에 연결** 대화 상자에서 연결 정보를 지정한 다음 **연결**을 클릭합니다. **스키마 행 집합 검색** 템플릿으로 채워진 새 쿼리 편집기 창이 열립니다.  
  
#### <a name="to-discover-column-names-from-the-mining-model-content-schema-rowset"></a>MINING MODEL CONTENT 스키마 행 집합에서 열 이름을 검색하려면  
  
1.  **스키마 행 집합 검색** 템플릿이 열려 있는 상태에서 **실행**을 클릭합니다.  
  
     현재 인스턴스에서 사용할 수 있는 모든 행 집합에 대한 행 집합 이름 및 행 집합 열이 포함된 스키마 행 집합 목록이 **결과** 창에 반환됩니다.  
  
2.  에 **쿼리** 창 뒤에 커서를 배치  **\<제한 목록 >** 하 고 enter 키를 눌러 새 줄을 추가 합니다.  
  
3.  형식 빈 줄에 커서를 놓고  **\<SchemaName > DMSCHEMA_MINING_MODEL_CONTENT\</SchemaName >**  
  
     제한에 대한 전체 섹션은 다음과 같아야 합니다.  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT</SchemaName>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
4.  **실행**을 클릭합니다.  
  
     **결과** 창에 지정한 스키마 행 집합의 열 이름 목록이 표시됩니다.  
  
#### <a name="to-create-a-content-query-using-the-mining-model-content-schema-rowset"></a>MINING MODEL CONTENT 스키마 행 집합을 사용하여 내용 쿼리를 만들려면  
  
1.  **스키마 행 집합 검색** 템플릿에서 요청 유형 태그 내의 텍스트를 바꿔서 요청 유형을 변경합니다.  
  
     다음 줄을  
  
     `<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>`  
  
     다음 줄로 바꿉니다.  
  
     **\<RequestType > DMSCHEMA_MINING_MODEL_CONTENT\</RequestType >**  
  
2.  제한 목록에 새 조건을 추가하여 이름으로 마이닝 모델을 지정하도록 제한 목록을 변경합니다.  
  
3.  템플릿에서 `<Restriction List>` 뒤에 커서를 놓고 Enter 키를 눌러 새 줄을 추가합니다.  
  
4.  빈 줄에 커서를 놓고 **<MODEL_NAME>내 모델 이름</MODEL_NAME>** 을 입력합니다.  
  
     제한에 대한 전체 섹션은 다음과 같아야 합니다.  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<MODEL_NAME>My model name</MODEL_NAME>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
5.  **실행**을 클릭합니다.  
  
     결과 창에 지정한 모델의 값과 함께 스키마 정의가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 콘텐츠 & #40; Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [데이터 마이닝 스키마 행 집합](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
