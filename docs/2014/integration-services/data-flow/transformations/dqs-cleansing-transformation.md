---
title: DQS 정리 변환 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4c597a99a0762efe2098696fe8d582d6a3c56f1b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079053"
---
# <a name="dqs-cleansing-transformation"></a>DQS 정리 변환
  DQS 정리 변환은 DQS(Data Quality Services)를 통해, 데이터 원본 또는 유사한 데이터 원본에 대해 만든 승인된 규칙을 적용하여 연결된 데이터 원본에서 데이터를 수정합니다. 데이터 수정 규칙에 대한 자세한 내용은 [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하십시오. DQS에 대한 자세한 내용은 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)을 참조하십시오.  
  
 데이터를 수정해야 할지 여부를 확인하기 위해 DQS 정리 변환은 다음과 같은 조건이 충족되는 경우 입력 열의 데이터를 처리합니다.  
  
-   데이터 수정을 위해 열이 선택됩니다.  
  
-   열 데이터 형식에 데이터 수정이 지원됩니다.  
  
-   열은 호환 가능한 데이터 형식의 도메인에 매핑됩니다.  
  
 변환에는 행 수준 오류를 처리하기 위해 구성할 수 있는 오류 출력이 포함됩니다. 오류 출력을 구성하려면 **DQS 정리 변환 편집기**를 사용합니다.  
  
 데이터 흐름에 [Fuzzy Grouping Transformation](fuzzy-grouping-transformation.md) 을 포함하여 중복된 것으로 간주되는 데이터 행을 식별할 수 있습니다.  
  
## <a name="data-quality-projects-and-values"></a>데이터 품질 프로젝트 및 값  
 DQS 정리 변환으로 데이터를 처리하면 Data Quality 서버에 정리 프로젝트가 생성됩니다. Data Quality 클라이언트를 사용하여 프로젝트를 관리합니다. 또한 Data Quality 클라이언트를 사용하여 프로젝트 값을 DQS 기술 자료 도메인으로 가져올 수 있습니다. 값만 도메인(또는 연결된 도메인)으로 가져올 수 있으며, DQS 정리 변환은 해당 도메인을 사용하도록 구성되었습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [데이터 품질 클라이언트에서 Integration Services 프로젝트 열기](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [도메인으로 정리 프로젝트 값 가져오기](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [데이터 원본에 데이터 품질 규칙 적용](apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   [관리 &#40;열기, 잠금 해제, 이름 바꾸기 및 삭제&#41; 데이터 품질 프로젝트](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)  
  
-   social.technet.microsoft.com의 문서, [복합 도메인을 사용하여 복합 데이터 정리](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)  
  
  
