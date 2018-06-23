---
title: Microsoft Excel용 Master Data Services 추가 기능 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 06f20a19801b43a25f3622424aa8ce76d2c34df2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091099"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Microsoft Excel용 Master Data Services 추가 기능
  와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], 참조 데이터의 마스터 목록을 Excel을 사용 하는 조직에 있는 모든 사용자에 게 배포할 수 있습니다. 데이터 사용자의 보기 및 업데이트 권한은 보안에 따라 결정됩니다.  
  
 MDS의 필터링된 데이터 목록을 Excel에 로드하여 다른 데이터와 같은 방식으로 사용할 수 있습니다. 작업이 끝나면 데이터를 다시 중앙 방식으로 저장되는 MDS에 게시할 수 있습니다.  
  
 관리자의 경우 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 을 사용하여 엔터티 및 특성을 만들고 데이터와 함께 이를 로드할 수 있습니다. 이렇게 하면 데이터를 모델에 로드하기 위해 다른 도구를 사용할 필요가 없습니다.  
  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서는 DQS(Data Quality Services)를 사용하여 데이터를 MDS에 로드하기 전에 일치시킬 수 있습니다. 이렇게 하면 MDS에서 데이터가 중복되지 않도록 방지하는 데 도움이 됩니다.  
  
> [!IMPORTANT]  
>  계속 사용할 수 있습니다는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 의 Master Data Services 추가 기능을 Excel 용 Master Data Services 및 Data Quality Services를 업그레이드 한 후의 SP1 버전 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 합니다. 하지만 SQL Server 2014 CTP2로 업그레이드한 후에는 이전 버전의 Excel용 MDS(Master Data Services) 추가 기능이 모두 작동하지 않습니다. 다운로드할 수 있습니다는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 버전의 Master Data Services 추가 기능을 for Excel에서 [여기](http://go.microsoft.com/fwlink/?LinkId=328664)합니다.  
  
## <a name="terms"></a>용어  
 추가 기능 사용과 관련해서는 다음과 같은 용어가 사용됩니다.  
  
-   *MDS repository* 는 모든 마스터 데이터가 저장되는 위치입니다. 이 위치는 MDS 데이터를 저장하도록 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 저장소의 데이터를 사용하기 위해서는 데이터를 Excel에 로드하고, 작업이 끝나면 변경 내용을 다시 저장소에 게시합니다. 관리자는 새로운 엔터티 및 특성을 저장소에 추가할 수 있습니다.  
  
-   *MDS 관리 데이터* 는 MDS 리포지토리에 저장되며 데이터가 강조 표시된 행으로 표시되는 Excel에 로드하는 데이터입니다. 비 MDS 관리 데이터를 워크시트에 추가할 수 있으며, 이러한 데이터는 MDS 관리 데이터를 새로 고칠 때 영향을 받지 않습니다.  
  
-   *model* 은 데이터의 컨테이너입니다. 이러한 컨테이너는 여러 버전으로 만들 수 있으며 일반적으로 최신 버전이 가장 최근의 내용을 포함합니다. 자세한 내용은 [모델&#40;Master Data Services&#41;](../models-master-data-services.md)을 참조하세요.  
  
-   *entity* 는 데이터 목록입니다. 엔터티는 데이터베이스에 있는 테이블로 생각할 수 있습니다. 예를 들어 **Color** 엔터티는 색 목록을 포함할 수 있습니다. 자세한 내용은 [엔터티&#40;Master Data Services&#41;](../entities-master-data-services.md)를 참조하세요.  
  
-   *member* 는 데이터의 행입니다. 각 엔터티에는 멤버가 포함되어 있습니다. 멤버의 예로는 **Blue**를 들 수 있습니다. 자세한 내용은 [멤버&#40;Master Data Services&#41;](../members-master-data-services.md)를 참조하세요.  
  
-   *attribute* 은 데이터의 열입니다. 각 멤버에는 특성이 포함됩니다. 예를 들어 **Blue** 멤버에 대한 **Code** 특성은 **B**입니다. 특성에 대한 자세한 내용은 [특성&#40;Master Data Services&#41;](../attributes-master-data-services.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 저장소에 대한 연결 만들기|[MDS 리포지토리에 연결&#40;Excel용 MDS 추가 기능&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|MDS 관리 데이터를 Excel로 로드|[MDS에서 Excel로 데이터 로드](export-data-to-excel-from-master-data-services.md)|  
|현재 표시된 MDS 관리 데이터를 이후에 열기 위해 사용할 수 있는 바로 가기 쿼리 저장|[바로 가기 쿼리 파일 저장&#40;Excel용 MDS 추가 기능&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|다른 사용자와 바로 가기 공유|[바로 가기 쿼리 파일을 메일로 보내기&#40;Excel용 MDS 추가 기능&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|멤버에 대해 수행된 모든 변경 내용 보기|[멤버에 대한 모든 주석 또는 트랜잭션 보기&#40;Excel용 MDS 추가 기능&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|새 데이터를 게시하기 전에 중복된 데이터가 있는지 확인|[유사한 데이터 일치&#40;Excel용 MDS 추가 기능&#41;](match-similar-data-mds-add-in-for-excel.md)|  
|워크시트의 데이터를 MDS 저장소에 게시|[Excel에서 MDS로 데이터 게시 &#40;MDS 추가 기능에 Excel 용&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|워크시트의 데이터가 포함된 새 엔터티 만들기 (관리자 전용)|[엔터티 만들기&#40;Excel용 MDS 추가 기능&#41;](create-an-entity-mds-add-in-for-excel.md)|  
|제한된 목록으로도 알려진 도메인 기반 특성 만들기 (관리자 전용)|[도메인 기반 특성 만들기&#40;Excel용 MDS 추가 기능&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Excel용 Master Data Services 추가 기능에서 데이터를 로드하고 게시하기 위한 속성을 설정합니다. (관리자 전용)|[Excel용 Master Data Services 추가 기능의 속성 설정](setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [연결&#40;Excel용 MDS 추가 기능&#41;](connections-mds-add-in-for-excel.md)  
  
-   [데이터 로드 &#40;MDS 추가 기능에 Excel 용&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [바로 가기 쿼리 파일&#40;Excel용 MDS 추가 기능&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Excel용 MDS 추가 기능의 데이터 품질 일치](data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [데이터를 게시 &#40;MDS 추가 기능에 Excel 용&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [모델 작성&#40;Excel용 MDS 추가 기능&#41;](building-a-model-mds-add-in-for-excel.md)  
  
-   [보안&#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  