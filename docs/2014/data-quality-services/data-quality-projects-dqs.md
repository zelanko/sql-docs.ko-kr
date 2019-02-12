---
title: 데이터 품질 프로젝트(DQS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 8f4fbe5a3990348edc2e8b3716ca869c4166e145
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043284"
---
# <a name="data-quality-projects-dqs"></a>데이터 품질 프로젝트(DQS)
  DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )의 데이터 품질 프로젝트는 기술 자료를 사용하여 *데이터 정리* 및 *데이터 일치* 작업을 수행한 다음 결과 데이터를 SQL Server 데이터베이스 또는 .csv 파일로 내보내 원본 데이터의 품질을 향상시킬 수 있는 수단입니다. 데이터 품질 프로젝트를 정리 프로젝트 또는 일치 프로젝트로 만들어 각 작업을 수행할 수 있습니다. 데이터 정리 및 일치에 대한 정보는 같은 기술 자료에 기본 제공될 수 있으므로 같은 기술 자료를 사용하여 정리 및 일치 프로젝트를 실행할 수 있습니다.  
  
 데이터 품질 프로젝트에는 다음과 같은 이점이 있습니다.  
  
-   DQS 기술 자료의 정보를 사용하여 원본 데이터에 대해 데이터 정리를 수행할 수 있습니다.  
  
-   기술 자료의 일치 정책을 사용하여 원본 데이터에 대해 데이터 일치를 수행할 수 있습니다.  
  
-   정리 및 일치 작업을 안내하고 선택 항목에 따라 SQL Server 데이터베이스 또는 .csv 파일로 데이터를 내보내는 마법사를 제공합니다. 데이터 관리자는 데이터 품질 프로젝트를 사용하여 컴퓨터 기반/대화형 정리 및 데이터 일치 단계를 실행하고 제어할 수 있습니다.  
  
##  <a name="Cleansing"></a> 데이터 품질 프로젝트: 정리 작업  
 정리 데이터 품질 프로젝트를 사용하여 기술 자료에 따라 원본 데이터를 정리할 수 있습니다. DQS의 데이터 정리 작업은 2단계 프로세스입니다.  
  
1.  *컴퓨터 기반* 데이터 정리 프로세스는 기술 자료의 정보에 대해 원본 데이터를 분석하고 변경 내용을 제안합니다. 처리된 데이터는 DQS에 의해 분류(제안, 새로 만들기, 잘못됨, 수정됨 및 올바름)되어 추가로 처리할 수 있도록 사용자에게 표시됩니다.  
  
2.  *대화형* 정리 프로세스에서는 데이터 관리자가 컴퓨터 기반 데이터 정리 프로세스에서 제안된 데이터를 승인, 거부 또는 수정할 수 있습니다.  
  
 데이터 품질 프로젝트의 정리 작업에 대한 자세한 내용은 [Data Cleansing](../../2014/data-quality-services/data-cleansing.md)를 참조하세요.  
  
##  <a name="Matching"></a> 데이터 품질 프로젝트: 일치 작업  
 일치 데이터 품질 프로젝트를 사용하면 정확한 수치 및 근사치 일치를 확인하고 이를 통해 중복 데이터를 제거하는 방식으로 기술 자료의 일치 정책에 따라 일치 작업을 수행하여 데이터 중복을 방지할 수 있습니다. 따라서 일치를 실행하기 전에 데이터를 정리하는 것이 좋습니다. 이를 수행하려면:  
  
1.  데이터 품질 프로젝트를 만들고 **정리** 작업을 선택한 다음 원본 데이터에 대해 데이터 정리 작업을 완료하고 SQL Server 데이터베이스의 테이블로 데이터를 내보냅니다.  
  
2.  일치 정책이 포함된 기술 자료를 사용하여 다른 데이터 품질 프로젝트를 만들고 **일치** 작업을 선택한 다음 **맵** 페이지에서 1단계 중에 정리한 데이터를 내보낸 데이터베이스 및 테이블을 선택합니다.  
  
3.  정리한 데이터에 대해 일치 작업을 완료합니다.  
  
 데이터 품질 프로젝트의 일치 작업에 대한 자세한 내용은 [Data Matching](../../2014/data-quality-services/data-matching.md)를 참조하세요.  
  
##  <a name="ProfilingNotification"></a> 데이터 프로파일링 및 알림  
 데이터 품질 프로젝트에서 정리 및 일치 작업을 실행하는 동안 DQS에 의해 처리되는 데이터의 실시간 통계 및 정보를 확인할 수 있습니다. 데이터 프로파일링을 통해 정리 및 일치 프로세스의 효과를 평가하고 잠재적으로 데이터 정리 또는 일치로 데이터 품질이 개선된 정도를 확인할 수 있습니다. DQS 프로파일링에서는 *완결성* (데이터가 존재하는 정도)과 *정확도* (데이터를 의도된 용도에 맞게 사용할 수 있는 정도)의 두 가지 데이터 품질 차원을 제공합니다. 또한 데이터 프로파일링 정보를 기반으로 데이터 정리 및 데이터 일치 작업을 향상시키기 위해 수행할 수 있는 작업에 대한 알림이 표시됩니다. 데이터 프로파일링 및 알림에 대한 자세한 내용은 [Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|데이터 품질 프로젝트를 만드는 방법에 대해 설명합니다.|[데이터 품질 프로젝트 만들기](../../2014/data-quality-services/create-a-data-quality-project.md)|  
|데이터 품질 프로젝트를 관리하는 방법(열기, 잠금 해제, 이름 바꾸기 및 삭제)에 대해 설명합니다.|[관리 &#40;열기, 잠금 해제, 이름 바꾸기 및 삭제&#41; 데이터 품질 프로젝트](../../2014/data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)|  
|[!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]에서 Integration Services 프로젝트를 여는 방법에 대해 설명합니다.|[Data Quality Client에서 Integration Services 프로젝트 열기](../../2014/data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## <a name="see-also"></a>관련 항목  
 [DQS 기술 자료 및 도메인](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
