---
title: '3 단원: 데이터와 일치 하 여 공급자 목록에서 중복 항목 제거 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c59a2fce106b08f53722ce44ae69225b680d7925
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484649"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>3단원: 데이터 일치로 공급자 목록에서 중복 항목 제거
  기술 자료에 일치 정책을 만들어서 일치 작업 수행을 위한 기술 자료를 준비합니다. 기술 자료에는 하나의 일치 정책만 있을 수 있습니다. 일치 정책은 하나 이상의 일치 규칙으로 구성됩니다. 규칙은 일치 프로세스에 관련된 도메인을 식별하고 일치 판단 시 각 도메인 값의 가중치를 지정합니다. 이 규칙에 도메인 값이 정확히 일치하는 항목이어야 하는지, 또는 유사하면 되는지 여부와 유사성 수준을 지정합니다. 도메인 일치 항목이 일치 프로세스의 필수 구성 요소인지 여부도 지정합니다. 각 규칙을 따로 테스트하고 샘플 데이터에 대해 전제 정책을 테스트할 수 있습니다. 테스트 과정에서 일치 점수가 클러스터(그룹)의 DQS 구성에 지정된 **최소 레코드 점수** 임계값보다 큰 레코드가 표시됩니다. 만족할 때까지 정책의 규칙을 계속 조정할 수 있습니다.  
  
 정책 정의 후 데이터 품질 프로젝트를 만들어 일치 작업을 실행할 수 있습니다. 일치 프로젝트는 평가할 데이터 원본에 일치 정책의 일치 규칙을 적용합니다. 이 프로세스는 두 행이 일치 항목일 가능성을 평가합니다. DQS는 일치 분석을 수행할 때 DQS에서 일치 항목으로 간주한 레코드의 클러스터를 만듭니다. DQS가 임의로 레코드 중 하나를 피벗 레코드로 식별합니다. 클러스터에 적합한 일치 항목이 아닌 레코드를 확인하거나 거부할 수 있습니다. 자세한 내용은 [일치 정책 만들기](https://msdn.microsoft.com/library/hh270290.aspx) 항목을 참조하십시오.  
  
 이 단원에서는 일치 작업을 수행하여 공급자 목록에서 중복 항목을 제거합니다. 먼저 공급자 목록에서 중복 항목을 식별하는 하나의 규칙으로 일치 정책을 만들어 기술 자료에 게시합니다. 다음으로 일치에 대한 데이터 품질 프로젝트를 만들고 실행합니다. 마지막으로 일치 작업의 결과를 나중에 MDS(Master Data Services)에 데이터를 업로드하는 데 사용할 Excel 파일로 내보냅니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 1: 일치 정책 정의](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  
