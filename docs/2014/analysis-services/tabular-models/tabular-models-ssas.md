---
title: 테이블 형식 모델링 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 11a5a9332c7fa85fd6407523ffd9c7c48a2c0514
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198753"
---
# <a name="tabular-modeling-ssas-tabular"></a>테이블 형식 모델링(SSAS 테이블 형식)
  테이블 형식 모델은 Analysis Services의 인 메모리(in-memory) 데이터베이스입니다. 최첨단 비교 알고리즘과 다중 쿼리 프로세서를 사용하는 xVelocity 메모리 내 분석 엔진(VertiPaq)은 Microsoft Excel 및 Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]등의 보고 클라이언트 애플리케이션을 통해 테이블 형식 모델 개체와 데이터에 신속하게 액세스할 수 있게 합니다.  
  
 테이블 형식 모델은 캐시된 모드와 DirectQuery 모드라는 두 가지 모드를 통해 데이터 액세스를 지원합니다. 캐시된 모드에서는 관계형 데이터베이스, 데이터 피드 및 일반 텍스트 파일을 포함하여 여러 원본의 데이터를 통합할 수 있습니다. DirectQuery 모드에서는 인 메모리 모델을 무시하고 클라이언트 애플리케이션에서 (SQL Server 관계형) 원본에 데이터를 직접 쿼리할 수 있도록 허용합니다.  
  
 테이블 형식 모델은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 새로운 테이블 형식 모델 프로젝트 템플릿을 사용하여 만듭니다. 여러 원본에서 데이터를 가져온 다음 관계, 계산 열, 측정값, KPI 및 계층을 추가하여 모델을 보강할 수 있습니다. 그런 다음 클라이언트 보고 애플리케이션에서 연결할 수 있는 Analysis Services 인스턴스에 모델을 배포할 수 있습니다. 배포된 모델은 SQL Server Management Studio에서 다차원 모델처럼 관리할 수 있습니다. 이러한 모델을 처리 최적화를 위해 분할하거나, 역할 기반 보안을 사용하여 행 수준 보안을 설정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [테이블 형식 모델 솔루션 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
 [테이블 형식 Model 데이터베이스 &#40;&AMP;#40;SSAS 테이블 형식&#41;](tabular-model-databases-ssas-tabular.md)  
  
 [테이블 형식 모델 데이터 액세스](tabular-model-data-access.md)  
  
  
