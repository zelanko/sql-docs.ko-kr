---
title: 데이터 원본에 데이터 품질 규칙 적용 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 85410c2b33a48670a7b443eb4b72b92fe16688b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726295"
---
# <a name="apply-data-quality-rules-to-data-source"></a>데이터 원본에 데이터 품질 규칙 적용

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  DQS(Data Quality Services)를 통해 데이터 원본에 DQS 정리 변환을 연결하여 패키지 데이터 흐름의 데이터를 수정할 수 있습니다. DQS에 대한 자세한 내용은 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)을 참조하십시오. 변환에 대한 자세한 내용은 [DQS Cleansing Transformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)을 참조하십시오.  
  
 DQS 정리 변환을 사용하여 데이터를 처리할 경우 Data Quality 서버에 데이터 품질 프로젝트가 만들어집니다. Data Quality 클라이언트를 사용하여 프로젝트를 관리합니다. 자세한 내용은 [데이터 품질 프로젝트 열기, 잠금 해제, 이름 바꾸기 및 삭제](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md)를 참조하세요.  
  
### <a name="to-correct-data-in-the-data-flow"></a>데이터 흐름에서 데이터를 수정하려면  
  
1.  패키지를 만듭니다.  
  
2.  DQS 정리 변환을 구성하고 추가합니다. 자세한 내용은 [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md)을 참조하세요.  
  
3.  DQS 정리 변환을 데이터 원본에 연결합니다.  
  
  
