---
title: Excel용 MDS 추가 기능의 데이터 품질 일치 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: be78d051-0d56-46d3-bb89-327e218dadd6
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fbb510e5c7035a8b6247bf1098951f5dec276f26
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="data-quality-matching-in-the-mds-add-in-for-excel"></a>Excel용 MDS 추가 기능의 데이터 품질 일치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  시간이 지날수록 MDS 저장소에 추가하는 데이터가 늘어나게 됩니다. 데이터를 추가하기 전에 새 데이터와 MDS에서 관리되는 기존 데이터를 비교하면 중복되거나 정확하지 않은 데이터가 추가되는 것을 방지할 수 있습니다.  
  
 MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 DQS(Data Quality Services)를 사용하여 비슷한 데이터를 일치시킵니다. 추가 기능에 포함된 일치 기능을 사용하면 비슷한 레코드가 그룹화되고 결과의 정확성을 보여 주는 점수가 표시됩니다. DQS가 제공하는 일치 기능에 대한 자세한 내용은 [Data Matching](../../data-quality-services/data-matching.md)를 참조하십시오.  
  
## <a name="workflow-for-data-quality-matching"></a>데이터 품질 일치 워크플로  
 DQS를 MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]와 함께 사용하는 경우 다음 워크플로를 따르십시오.  
  
1.  MDS 관리 데이터 목록을 검색하여 MDS에서 관리되지 않는 목록과 결합합니다. 자세한 내용은 [데이터 결합&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)를 참조하십시오.  
  
2.  DQS 기술 자료를 사용하여 결합된 목록의 데이터를 비교합니다. 자세한 내용은 [유사한 데이터 일치&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)를 참조하십시오.  
  
3.  DQS가 발견한 유사성에 대한 자세한 정보를 보려면 세부 열을 표시합니다.  
  
4.  결과를 모두 이동해 MDS 저장소에 추가되어야 하는 데이터와 중복된 데이터를 확인합니다.  
  
5.  새 데이터 및/또는 업데이트된 데이터를 MDS 저장소에 게시합니다.  
  
## <a name="knowledge-bases"></a>기술 자료  
 추가 기능에 제공되는 일치 결과는 DQS 기술 자료를 기준으로 합니다.  
  
-   기본 기술 자료(DQS 데이터)는 DQS를 설치할 때 만들어집니다. Data Quality 클라이언트의 기본 기술 자료에 일치 정책을 추가하지 않고 기본 기술 자료를 사용하기로 선택할 경우 워크시트의 열을 기술 자료의 도메인에 매핑한 다음 선택한 도메인에 가중치 값을 할당해야 합니다.  
  
-   Data Quality 클라이언트를 사용하여 일치 정책을 포함한 새 기술 자료를 만들거나, 기본 기술 자료에 일치 정책을 추가할 수 있습니다. 이 경우 가중치 값은 이미 만들어 둔 일치 정책에 따라 결정되므로 도메인에 열을 매핑하기만 하면 됩니다. 자세한 내용은 [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md)을 참조하세요.  
  
 기술 자료에 대한 자세한 내용은 [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|외부 데이터와 MDS 관리 데이터를 비교하기 전에 결합합니다.|[데이터 결합&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  
|DQS 기술 자료를 사용하여 데이터의 유사성을 찾습니다.|[유사한 데이터 일치&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [개요: Excel에서 데이터 가져오기&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Data Matching](../../data-quality-services/data-matching.md)  
  
  
