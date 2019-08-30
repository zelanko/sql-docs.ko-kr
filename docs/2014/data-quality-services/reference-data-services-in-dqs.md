---
title: DQS의 참조 데이터 서비스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f4f7c1003db22721d9140c166b1ed03e72b9ab0f
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154435"
---
# <a name="reference-data-services-in-dqs"></a>DQS의 참조 데이터 서비스
  참조 데이터는 신뢰할 수 있는 공용 도메인에서 또는 고급 상용 콘텐츠 공급자를 통해 사용할 수 있는 관련 또는 분류된 전역 데이터(엔터프라이즈의 경계를 벗어남)의 정확하고 완전한 집합을 의미합니다.  
  
 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )의 참조 데이터 서비스 기능을 사용하여 타사 참조 데이터 공급자를 구독하고 고품질 데이터를 기준으로 비즈니스 데이터의 유효성을 검사하여 비즈니스 데이터를 쉽게 정리하고 보강할 수 있습니다. 정리 프로세스가 진행되는 동안 Data Quality Services 내에서 업계 선두 데이터 품질 서비스 공급업체의 서비스를 사용하여 데이터 표준화, 수정 또는 보강을 수행할 수 있습니다. 예를 들어 지역 번호 또는 우편 번호 목록을 사용하여 참조 데이터를 기준으로 고객 주소의 유효성을 검사할 수 있습니다.  
  
 참조 데이터 서비스 기능에는 다음과 같은 이점이 있습니다.  
  
-   참조 데이터를 사용하면 타사 회사에서 보증하는 데이터에 비교하여 자신의 데이터 품질을 보장할 수 있습니다.  
  
-   DQS 기술 자료 구축 및 데이터 품질 프로젝트에 참조 데이터 프로세스가 통합되어 있으므로 포괄적인 데이터 품질 프로세스를 도입할 수 있습니다.  
  
-   에서는 Azure Marketplace 및 타사 참조 데이터 공급자에서 직접 참조 데이터를 사용할 수 있습니다.  
  
##  <a name="Marketplace"></a>Azure Marketplace의 참조 데이터 사용  
 DQS는 Azure Marketplace의 참조 데이터를 사용 하 여 콘텐츠 공급자가 Marketplace를 통해 참조 데이터 서비스를 제공할 수 있도록 지원 합니다. Marketplace는 단일 마켓플레이스와 고품질 데이터 및 애플리케이션 배달 채널을 클라우드 서비스로 제공하는 Microsoft의 서비스입니다. Marketplace에 대 한 자세한 내용은 [Azure Marketplace에 대해 알아보기](https://azuremarketplace.microsoft.com/marketplace/)를 참조 하세요.  
  
 Marketplace와 DQS 간의 원활한 통합은 DQS 내 데이터 품질 프로젝트에 대한 정보 검색, 탐색 및 가져오기와 관련된 단계를 간소화합니다. DQS에서 데이터를 가져올 수 있으므로 DQS 사용자는 DQS, Marketplace 및 참조 데이터 서비스 공급자를 혁신적인 방식으로 결합하여 고품질 데이터를 얻을 수 있습니다.  
  
 DQS에서 Marketplace의 참조 데이터를 정리 작업에 사용하려면 유효한 Marketplace 계정 키가 있어야 합니다. Marketplace 계정 키를 만드는 것은 무료이며 유료 데이터 세트를 구독하는 경우에만 요금이 청구됩니다. 무료 데이터 세트를 구독하고 사용하는 경우에는 요금이 청구되지 않습니다. Marketplace 계정 키를 만드는 방법은 [계정 만들기](https://go.microsoft.com/fwlink/?LinkId=212936)(https://go.microsoft.com/fwlink/?LinkId=212936) )를 참조하세요.  
  
 또한 DQS 내에서 다음과 같은 Marketplace 작업을 수행할 수 있습니다.  
  
-   Marketplace에서 데이터 집합을 찾아봅니다.  
  
-   Marketplace 계정 키를 만듭니다.  
  
-   계정 키 및 데이터 공급자 구독과 같은 Marketplace 계정 세부 사항을 관리합니다.  
  
 **에 있는** 구성 **화면의** 참조 데이터 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]탭에서 이러한 작업을 수행할 수 있습니다.  
  
##  <a name="Direct"></a> 타사 참조 데이터 공급자를 통해 직접 참조 데이터 사용  
 인터넷에 연결되어 있지 않아서 Marketplace를 사용할 수 없는 경우 DQS는 조직의 네트워크 내에 있는 데이터 공급자에 직접 연결할 수 있도록 지원합니다. 다이렉트 온라인 타사 참조 데이터 공급자의 참조 데이터를 사용하려면 DQS에서 해당 데이터 공급자에 대한 레코드를 만들어야 합니다.  
  
##  <a name="HowToCleanse"></a> 참조 데이터를 사용하여 데이터를 정리하는 방법  
 참조 데이터를 사용하여 DQS의 데이터를 정리하기 위한 3단계는 다음과 같습니다.  
  
1.  **DQS에서 참조 데이터 공급자 세부 정보 구성**: DQS에서 참조 데이터를 사용 하려면 DQS에서 참조 데이터 서비스 세부 정보를 구성 해야 합니다.  
  
    1.  Marketplace를 사용하는 경우 유효한 Marketplace 계정 키를 제공하고 Marketplace의 [Data Quality Services](../data-quality-services/data-quality-services.md) 데이터 범주로 이동한 후 필요한 공급자를 구독합니다.  
  
    2.  다이렉트 온라인 참조 데이터 공급자를 사용하는 경우 DQS에서 다이렉트 참조 데이터 공급자 세부 정보를 추가해야 사용할 수 있습니다.  
  
     DQS에서 참조 데이터 공급자 세부 정보를 구성하는 작업은 특정 데이터 공급자에 대해 한 번만 수행하면 됩니다. DQS 관리자만 DQS에서 참조 데이터 설정을 구성할 수 있습니다.  
  
2.  **기술 자료의 도메인/복합 도메인을 참조 데이터 서비스에 매핑**: 1 단계에서 구독/추가한 적절 한 참조 데이터 서비스에 도메인/복합 도메인을 매핑합니다.  
  
3.  **데이터 품질 프로젝트의 정리 작업에 매핑된 도메인 사용**: **정리** 작업에 대한 데이터 품질 프로젝트를 만들 때 2단계서 참조 데이터 서비스와 매핑된 도메인/복합 도메인이 포함된 기술 자료를 선택하고 정리 작업을 수행합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|Marketplace 또는 다이렉트 온라인 타사 데이터 공급자의 참조 데이터 서비스를 사용하도록 DQS를 구성하는 방법에 대해 설명합니다.|[참조 데이터를 사용하도록 DQS 구성](../../2014/data-quality-services/configure-dqs-to-use-reference-data.md)|  
|기술 자료의 도메인/복합 도메인을 참조 데이터 서비스에 매핑하는 방법에 대해 설명합니다.|[참조 데이터에 도메인 또는 복합 도메인 연결](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)|  
|참조 데이터 서비스를 사용하여 데이터를 정리하는 방법에 대해 설명합니다.|[참조 데이터&#40;외부&#41; 기술 자료를 사용하여 데이터 정리](../../2014/data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
