---
title: 클릭 방문 보고서(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- clickthrough reports
- customizing clickthrough reports
- clickthrough reports, customizing
ms.assetid: cf2c396e-b0c6-41f9-8c45-ddc8406f7e85
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d044b8f245d3c3ce2c092b7b5f2b094122f75f1e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101203"
---
# <a name="clickthrough-reports-ssrs"></a>클릭 광고 보고서(SSRS)
  클릭 광고 보고서는 주 보고서 내에 포함되어 있는 데이터에 대한 세부 정보를 제공하는 보고서입니다. 클릭 광고 보고서는 사용자가 주 보고서에 나타나는 대화형 데이터를 클릭할 때 표시됩니다. 이러한 보고서는 보고서 서버에 의해 자동으로 생성됩니다. 모델 디자이너 결정을 설정 하 여 클릭 광고 보고서에 표시할 항목의 `DefaultDetailAttribute` 및 `DefaultAggregateAttribute` 보고서 모델의 엔터티에 할당 하는 속성입니다.  
  
> [!NOTE]  
>  클릭 광고 보고서의 모든 버전에서 사용할 수 없는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다. 조직에서 실행 중인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전을 잘 모를 경우 데이터베이스 관리자에게 문의하십시오.  
  
## <a name="using-default-templates"></a>기본 템플릿 사용  
 기본적으로 보고서 서버는 엔터티별로 단일 인스턴스 템플릿과 여러 인스턴스 템플릿이라는 두 개의 클릭 광고 템플릿 유형을 생성합니다. 클릭하는 항목에 따라 사용되는 템플릿이 결정됩니다. 보고서를 읽는 사람이 스칼라 특성을 클릭하면 단일 인스턴스 템플릿이 사용되고 집계 특성을 클릭하면 여러 인스턴스 템플릿이 사용됩니다.  
  
#### <a name="single-instance-templates"></a>단일 인스턴스 템플릿  
 단일 인스턴스 템플릿은 대상 엔터티의 모든 특성 및 대상 엔터티를 기준으로 일 대 다 관계에 있는 관련 엔터티에 대해 지정되는 모든 기본 집계 특성을 표시합니다. 단일 인스턴스 템플릿은 다음 이미지와 비슷합니다.  
  
 ![다 대 일 클릭 방문 보고서](../media/manytooneclickthrough.gif "다 대 일 클릭 방문 보고서")  
  
#### <a name="multiple-instance-templates"></a>여러 인스턴스 템플릿  
 여러 인스턴스 템플릿은 대상 엔터티의 기본 세부 특성 및 대상 엔터티를 기준으로 일 대 다 관계에 있는 관련 엔터티에 대해 지정되는 모든 기본 집계 특성만 표시합니다. 여러 인스턴스 템플릿은 다음 이미지와 비슷합니다.  
  
 ![다 대 일 클릭 방문 보고서](../media/onetomanyclickthrough.gif "다 대 일 클릭 방문 보고서")  
  
## <a name="customizing-clickthrough-reports"></a>클릭 광고 보고서 사용자 지정  
 보고서 서버가 생성하는 기본 템플릿을 사용하는 대신 보고서 작성기에서 보고서를 만들어 사용자 지정된 클릭 광고 보고서로 사용할 수 있습니다. 그런 다음 보고서 관리자에서 이 보고서를 드릴스루 보고서로 모델에 연결할 수 있습니다.  
  
 보고서 작성기 보고서를 클릭 광고 보고서로 바꾸려면 보고서 작성기 **속성** 대화 상자에서 **이 보고서에 드릴스루 사용** 옵션을 선택해야 합니다. 이 옵션을 선택하면 드릴스루 매개 변수가 보고서에 추가되고 보고서는 더 이상 보고서 작성기에서 직접 실행될 수 없습니다. 보고서를 보는 사람이 보고서 작성기 보고서의 항목을 클릭하면 보고서 서버에서 자동으로 드릴스루 매개 변수를 계산합니다.  
  
> [!IMPORTANT]  
>  보고서에서 사용되는 기본 엔터티는 보고서를 연결하는 엔터티와 동일한 엔터티여야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서를 클릭 광고 보고서로 모델에 연결](../link-a-report-to-a-model-as-a-clickthrough-report.md)  
  
  
