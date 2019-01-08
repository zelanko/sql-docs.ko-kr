---
title: 데이터 기반 구독 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: ba009f62-0d4f-45e7-a27c-36fd5f0cd3a8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 71ab6239172ea39a8adcee9ca017a5408079a8d5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357154"
---
# <a name="data-driven-subscriptions"></a>데이터 기반 구독
  데이터 기반 구독을 통해 런타임에 외부 데이터 원본에서 검색되는 동적 구독 데이터를 사용할 수 있습니다. 데이터 기반 구독에서는 구독이 정의될 때 사용자가 지정한 정적 텍스트와 기본값을 사용할 수도 있습니다. 데이터 기반 구독을 사용하여 수행할 수 있는 작업은 다음과 같습니다.  
  
-   변동이 잦은 구독자 목록에 보고서를 배포합니다. 예를 들어 데이터 기반 구독을 사용하여 구독자가 매월 달라지는 대규모 조직에서 보고서를 배포하거나 기존 사용자 집합에서 그룹 멤버 자격을 결정하는 다른 조건을 사용할 수 있습니다.  
  
-   런타임에 검색되는 보고서 매개 변수 값을 사용하여 보고서 출력을 필터링합니다.  
  
-   보고서 출력 형식과 각 보고서 배달에 사용되는 배달 옵션을 다양하게 변경합니다.  
  
 데이터 기반 구독은 여러 부분으로 구성됩니다. 데이터 기반 구독의 고정 요소는 해당 구독을 만들 때 정의되며 다음을 포함합니다.  
  
-   구독이 정의되는 대상 보고서. 구독은 항상 단일 보고서와 연결됩니다.  
  
-   보고서를 배달하는 데 사용되는 배달 확장 프로그램. 보고서 서버 전자 메일 배달, 파일 공유 배달, 캐시를 미리 로드하는 데 사용되는 Null 배달 공급자, 또는 사용자 지정 배달 확장 프로그램을 지정할 수 있습니다. 단일 구독 내에서 여러 개의 배달 확장 프로그램을 지정할 수는 없습니다.  
  
-   구독자 데이터 원본. 구독을 정의할 때는 구독자 데이터가 들어 있는 데이터 원본에 대한 연결 문자열을 지정해야 합니다. 구독자 데이터 원본은 런타임에 동적으로 지정할 수 없습니다.  
  
-   구독자 데이터를 선택하는 데 사용하는 쿼리는 구독을 정의할 때 지정해야 합니다. 런타임에는 쿼리를 변경할 수 없습니다.  
  
 데이터 기반 구독에 사용되는 동적 값은 구독이 처리될 때 가져올 수 있습니다. 구독에 사용할 수 있는 변수 데이터의 예로는 구독자 이름, 전자 메일 주소, 기본 보고서 출력 형식 등이 있으며 그 밖에도 보고서 매개 변수에 사용할 수 있는 모든 값을 사용할 수 있습니다. 데이터 기반 구독에서 동적 값을 사용하려면 쿼리에서 반환되는 필드와 특정 배달 옵션 및 보고서 매개 변수 간의 매핑을 정의합니다. 변수 데이터는 구독이 처리될 때마다 구독자 데이터 원본에서 가져옵니다.  
  
## <a name="requirements-for-using-data-driven-subscriptions"></a>데이터 기반 구독 사용을 위한 요구 사항  
 모든 버전에서 데이터 기반 구독 기능을 사용할 수 있는 것은 아닙니다. 또한 런타임에 구독 데이터를 검색하는 데 사용할 수 있는 데이터 원본의 종류에도 제한이 있습니다. 다음 목록에서는 요구 사항에 대한 추가 정보를 제공합니다.  
  
-   데이터 기반 구독 기능을 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 대한 자세한 내용은 [SQL Server 2012 버전에서 지원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)을 참조하세요.  
  
-   구독 데이터의 경우 보고서 서버에 대한 스키마 정보를 제공할 수 있는 데이터 원본을 선택합니다. 지원되는 데이터 원본 유형의 예로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터, Oracle, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 데이터, ODBC 데이터 원본 및 OLE DB 데이터 원본이 있습니다. 구독자 데이터 원본 요구 사항에 대한 자세한 내용은 [구독자 데이터에 외부 데이터 원본 사용&#40;데이터 기반 구독&#41;](use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)을 참조하세요.  
  
## <a name="working-with-data-driven-subscriptions"></a>데이터 기반 구독 작업  
 다음 항목은 데이터 기반 구독에 대한 추가 정보를 제공합니다.  
  
|항목|Description|  
|------------|-----------------|  
|[데이터 기반 구독 만들기, 수정 및 삭제](data-driven-subscriptions.md)|데이터 기반 구독을 만들고, 수정하고, 삭제하는 방법을 설명합니다.|  
|[구독자 데이터에 외부 데이터 원본 사용&#40;데이터 기반 구독&#41;](use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)|데이터 기반 구독에 사용할 수 있는 데이터 원본에 대한 정보를 제공합니다.|  
|[데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)|데이터 기반 구독을 만드는 방법에 대한 단계별 학습 지침을 제공합니다.|  
|[보고서 캐시&#40;SSRS&#41;](../report-server/caching-reports-ssrs.md)|데이터 기반 구독과 함께 Null 배달 공급자를 사용하여 캐시를 미리 로드하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [구독 및 배달&#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [데이터 기반 구독 만들기 페이지&#40;보고서 관리자&#41;](../create-data-driven-subscription-page-report-manager.md)   
 [캐시 사전 로드&#40;보고서 관리자&#41;](../report-server/preload-the-cache-report-manager.md)  
  
  
