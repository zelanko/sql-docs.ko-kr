---
title: 메타 데이터 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- user-defined metadata [Master Data Services], about user-defined metadata
- metadata [Master Data Services], about metadata
- metadata [Master Data Services]
- user-defined metadata [Master Data Services]
ms.assetid: ac1aabe3-d8d4-4d7a-8954-50ee3c185d81
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 25fa2078127816b2fd9d50bd7bd4c074c3577dae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082708"
---
# <a name="metadata-master-data-services"></a>메타데이터(MDS(Master Data Services))
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 사용자 정의 메타데이터는 모델 개체를 설명하는 데 사용되는 정보입니다. 예를 들어 특정 모델이나 엔터티의 소유자를 추적하거나 엔터티에 데이터를 제공하는 원본 시스템을 추적해야 하는 경우가 있을 수 있습니다.  
  
 사용자 정의 메타 데이터는 라는 모델로 관리 **메타 데이터**합니다. 이 모델은 자동으로 포함 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 설치 되며 다른 모든 MDS 모델과 유사 제외 하 고 버전을 만들 수 없습니다.  
  
 메타데이터 모델을 사용자 정의 메타데이터로 채운 후 구독 시스템에서 사용할 수 있도록 구독 뷰에 포함할 수 있습니다.  
  
## <a name="metadata-entities"></a>메타데이터 엔터티  
 메타데이터 모델에는 5개의 엔터티가 포함되며, 각각 사용자 정의 메타데이터를 지원하는 마스터 데이터 모델 개체의 유형을 나타냅니다. 예를 들어는 **모델 메타 데이터 정의** 엔터티 모델을 나타내는 멤버가 포함 및 **특성 메타 데이터 정의** 엔터티에 포함 된 모든 모델에서 모든 특성을 나타내는 멤버입니다.  
  
 모델 개체에 대한 메타데이터를 정의하려면 이러한 멤버의 특성 중 하나를 채웁니다. 예를 들어는 **엔터티 메타 데이터 정의** 엔터티를 텍스트로 Price 멤버의 Description 특성을 채울 수 있습니다: **고객에 게 판매 될 때의 제품 가격**합니다.  
  
 메타데이터 모델의 멤버는 사용자 정의 메타데이터를 지원하는 모델 개체가 추가되거나 삭제될 때마다 자동으로 업데이트됩니다.  
  
 메타데이터 모델은 버전을 지정하거나 버전 플래그를 추가 또는 변경하거나 모델 배포 패키지로 저장할 수 없습니다. 그러나 메타데이터 모델은 다른 마스터 데이터 모델의 모든 기능을 갖추고 있습니다. 예를 들어 메타데이터 모델에 대한 비즈니스 규칙 집합을 구현하여 데이터 정책을 적용할 수 있습니다.  
  
## <a name="customizing-your-metadata-model"></a>메타데이터 모델 사용자 지정  
 각 메타데이터 정의 엔터티에는 Name, Code 및 Description 특성이 포함됩니다. 모델 개체를 보다 자세히 설명하기 위해 추가 특성을 만들 수도 있습니다.  
  
 예를 들어 다음과 같은 특성을 만들 수 있습니다.  
  
-   Owner라는 도메인 기반 특성 - 각 모델 개체의 소유자를 추적하는 데 사용합니다.  
  
-   Last Review Date라는 자유 형식 특성 - 소유자가 개체를 마지막으로 검토한 날짜를 추적하는 데 사용합니다.  
  
-   도메인 기반 특성 이라는 추적 하 고 상호 작용 하는 원본 시스템을 관리 하는 데 사용할 수 있는 소스는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 인스턴스.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|모델 개체에 메타데이터를 추가합니다.|[메타 데이터 추가 &#40;Master Data Services&#41;](add-metadata-master-data-services.md)
)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [데이터 내보내기 &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  