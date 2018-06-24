---
title: 복합 도메인의 데이터 정리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7d1076e0-7710-469a-9107-e293e4bd80ac
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ba152d105052ae8f481794ca28869cb5d4528de4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078870"
---
# <a name="cleanse-data-in-a-composite-domain"></a>복합 도메인의 데이터 정리
  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )의 복합 도메인 정리에 대한 정보를 제공합니다. 복합 도메인은 둘 이상의 단일 도메인으로 구성되며 여러 관련 용어로 구성된 데이터 필드에 매핑됩니다. 복합 도메인의 개별 도메인은 서로 공통된 정보 영역이 있어야 합니다. 복합 도메인에 대 한 자세한 내용은 참조 하십시오. [복합 도메인 관리](../../2014/data-quality-services/managing-a-composite-domain.md)합니다.  
  
##  <a name="Mapping"></a> 원본 데이터에 복합 도메인 매핑  
 원본 데이터와 복합 도메인을 매핑하는 방법에는 두 가지가 있습니다.  
  
-   원본 데이터는 복합 도메인에 매핑되는 단일 필드입니다(예:Full Name).  
  
    -   복합 도메인이 참조 데이터 서비스에 매핑된 경우 원본 데이터가 수정 및 구문 분석을 위해 있는 그대로 참조 데이터 서비스에 전송됩니다.  
  
    -   복합 도메인이 참조 데이터 서비스에 매핑되지 않은 경우에는 복합 도메인에 대해 정의된 구문 분석 방법에 따라 구문 분석됩니다. 복합 도메인의 구문 분석 방법을 지정 하는 방법에 대 한 자세한 내용은 참조 [복합 도메인 만들기](../../2014/data-quality-services/create-a-composite-domain.md)  
  
-   원본 데이터는 복합 도메인 내 개별 도메인에 매핑되는 여러 필드(예: First Name, Middle Name 및 Last Name)로 구성됩니다.  
  
 원본 데이터에 복합 도메인을 매핑하는 방법에 대 한 예제를 보려면 [참조 데이터에 도메인 또는 복합 도메인 연결](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)합니다.  
  
##  <a name="CDCorrection"></a> 선언적 도메인 간 규칙을 사용하여 데이터 수정  
 복합 도메인의 도메인 간 규칙을 사용하여 복합 도메인의 개별 도메인 간 관계를 나타내는 규칙을 만들 수 있습니다. 도메인 간 규칙은 복합 도메인과 관련된 원본 데이터에 대해 정리 작업을 실행할 때 고려됩니다. 선언적 *Then* 도메인 간 규칙 **값이 다음 값과 같음**은 도메인 간 규칙의 유효성에 대해 알려줄 뿐만 아니라 데이터 정리 작업 시 데이터를 수정합니다.  
  
 다음 예제를 살펴보세요. 3개의 개별 도메인 ProductName, CompanyName 및 ProductVersion이 있는 복합 도메인 Product가 있습니다. 다음과 같은 선언적 도메인 간 규칙을 만드세요.  
  
 IF 도메인 'CompanyName' 값이 다음을 포함 *Microsoft* AND 도메인 'ProductName' 값이 다음 값과 같음 *Office* AND 'ProductVersion' 값이 다음 값과 같음 *2010* THEN 도메인 'ProductName' 값이 다음 값과 같음 *Microsoft Office 2010*  
  
 이 도메인 간 규칙을 실행하면 정리 작업 후 원본 데이터(ProductName)가 다음과 같이 수정됩니다.  
  
 **원본 데이터**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Office|Microsoft Inc.|2010|  
  
 **출력 데이터**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Microsoft Office 2010|Microsoft Inc.|2010|  
  
 선언적 *Then* 도메인 간 규칙 **값이 다음 값과 같음**을 테스트하면 **복합 도메인 규칙 테스트** 대화 상자에 올바른 데이터를 표시하는 새 열 **다음으로 수정**이 포함됩니다. 정리 데이터 품질 프로젝트에서 이 선언적 도메인 간 규칙이 100% 신뢰도의 데이터를 변경하고, **이유** 열에 규칙 '*\<<Cross-Domain Rule Name>*’에 의해 수정됨 메시지가 표시됩니다. 도메인 간 규칙에 대 한 자세한 내용은 참조 [도메인 간 규칙을 만들](../../2014/data-quality-services/create-a-cross-domain-rule.md)합니다.  
  
> [!NOTE]  
>  선언적 도메인 간 규칙은 참조 데이터 서비스에 연결된 복합 도메인에 대해 작동하지 않습니다.  
  
##  <a name="DataProfiling"></a> 복합 도메인의 데이터 프로파일링  
 DQS 프로파일링에서는 정리 작업 시 *완결성* (데이터가 존재하는 정도)과 *정확도* (데이터를 의도된 용도에 맞게 사용할 수 있는 정도)의 두 가지 데이터 품질 차원을 제공합니다. 프로파일링은 복합 도메인에 대한 신뢰할 수 있는 완결성 통계를 제공할 수 없습니다. 완결성 통계가 필요한 경우 복합 도메인 대신 단일 도메인을 사용하세요. 복합 도메인을 사용하려는 경우 프로파일링을 위해 단일 도메인을 사용하는 하나의 기술 자료를 만들어 완결성을 확인하고 정리 작업을 위해 복합 도메인을 사용하는 다른 도메인을 만드는 것이 좋습니다. 예를 들어 프로파일링은 복합 도메인을 사용하는 주소 레코드에 대해 95%의 완결성을 표시할 수 있지만 우편 번호 열과 같은 열의 경우 불완결성 수준이 매우 높을 수 있습니다. 이 예에서는 단일 도메인을 사용하는 우편 번호 열의 완결성을 평가하는 것이 좋습니다.  
  
 프로파일링은 복합 도메인에 대해 신뢰할 수 있는 정확성 통계를 제공할 가능성이 높습니다. 여러 열의 정확성을 함께 평가할 수 있기 때문입니다. 이 데이터의 값은 복합 집계 형식이므로 복합 도메인을 사용하여 정확성을 평가하는 것이 좋습니다.  
  
 정리 작업 중 데이터 프로파일링에 대한 자세한 정보는 [DQS&#40;내부&#41; 기술 자료를 사용하여 데이터 정리](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)에서 [프로파일러 통계](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Profiler)를 참조하세요.  
  
  