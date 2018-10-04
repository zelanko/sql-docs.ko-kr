---
title: 데이터 원본에 데이터 품질 규칙 적용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8e2c8b435fd4af7955a96b303f810582fb496ca5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063223"
---
# <a name="apply-data-quality-rules-to-data-source"></a>데이터 원본에 데이터 품질 규칙 적용
  DQS(Data Quality Services)를 통해 데이터 원본에 DQS 정리 변환을 연결하여 패키지 데이터 흐름의 데이터를 수정할 수 있습니다. DQS에 대한 자세한 내용은 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)을 참조하십시오. 변환에 대한 자세한 내용은 [DQS Cleansing Transformation](dqs-cleansing-transformation.md)을 참조하십시오.  
  
 DQS 정리 변환을 사용하여 데이터를 처리할 경우 Data Quality 서버에 데이터 품질 프로젝트가 만들어집니다. Data Quality 클라이언트를 사용하여 프로젝트를 관리합니다. 자세한 내용은 [데이터 품질 프로젝트 관리&#40;열기, 잠금 해제, 이름 바꾸기 및 삭제&#41;](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)를 참조하세요.  
  
### <a name="to-correct-data-in-the-data-flow"></a>데이터 흐름에서 데이터를 수정하려면  
  
1.  패키지를 만듭니다.  
  
2.  DQS 정리 변환을 구성하고 추가합니다. 자세한 내용은 [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md)을 참조하세요.  
  
3.  DQS 정리 변환을 데이터 원본에 연결합니다.  
  
  
