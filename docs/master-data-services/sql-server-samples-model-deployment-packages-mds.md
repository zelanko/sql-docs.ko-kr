---
title: 'SQL Server 예제: 모델 배포 패키지(MDS) | Microsoft Docs'
ms.custom: ''
ms.date: 07/28/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- Master Data Services
- sample
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6526794fe6895e31b618a25d17b47ccabb940258
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65487973"
---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>SQL Server 예제: 모델 배포 패키지(MDS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]을 설치할 때 데이터가 있는 샘플 모델 패키지가 포함됩니다. 이러한 패키지 파일의 기본 위치는 \<드라이브>\Program Files\Microsoft SQL Server\130\Master Data Services\Samples\Packages입니다.  
  
 샘플 모델 패키지를 배포하는 방법에 대한 지침은 [샘플 모델 및 데이터 배포](../master-data-services/master-data-services-installation-and-configuration.md#deploySample)를 참조하세요. [MDSModelDeploy 도구](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)를 사용하여 샘플 모델 패키지를 배포합니다.  
  
> [!IMPORTANT]
>  **의 샘플 업데이트(!!) [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
> 
>  샘플 패키지가 다음과 같은 새로운 기능을 지원하도록 업데이트되었습니다.  
> 
>  -   다 대 다 관계 표시.  
> 
>      자세한 내용은 [샘플 모델의 M2M 관계](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md#M2MSample)를 참조하세요.  
> 
> -   도메인 기반 특성에 대한 허용된 값 제한  
> 
>      자세한 내용은 [도메인 기반 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)를 참조하세요.  
> -   엔터티 변경에 대한 승인 필요.  
> 
>      자세한 내용은 [승인 필요&#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md)를 참조하세요.  
> -   비즈니스 규칙에서 Not 및 Else 연산자 사용  
> 
>      자세한 내용은 [비즈니스 규칙 예제](../master-data-services/business-rule-examples-master-data-services.md)를 참조하세요.  
> -   사용자 지정 인덱스 구현  
> 
>      자세한 내용은 [사용자 지정 인덱스&#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)를 참조하세요.  
 

 
 Master Data Services에서 패키지는 배포 가능한 모델 구조와 모델의 데이터(옵션)를 포함하는 XML 파일입니다. 모델 패키지를 사용하여 MDS 환경 간에 모델의 복사본을 이동하거나 기존 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 환경에 새로운 모델을 만듭니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDSModelDeploy를 사용하여 모델 배포 패키지 배포](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
