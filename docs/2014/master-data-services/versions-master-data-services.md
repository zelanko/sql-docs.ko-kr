---
title: 버전(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- version flags [Master Data Services], about version flags
- versions [Master Data Services]
- version flags [Master Data Services]
- versions [Master Data Services], version flags
ms.assetid: 752ec96d-53d7-4160-8ed2-92e0324645f3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: befdb8a5e7de5c4aef86edf5e5bf029954c934c7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960543"
---
# <a name="versions-master-data-services"></a>버전(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 모델 내에 여러 버전의 마스터 데이터를 만들 수 있습니다. 버전은 데이터 유효성을 검사하는 동안 잠그고 데이터 유효성 검사 이후에 커밋할 수 있습니다. 커밋된 버전은 감사 가능한 변경 사항 레코드를 형성합니다. 이러한 각 버전에는 모델의 모든 멤버, 특성 값, 계층 멤버, 계층 관계 및 컬렉션이 포함됩니다.  
  
## <a name="when-to-use-versions"></a>버전을 사용하는 경우  
 버전을 사용하여 수행할 수 있는 작업은 다음과 같습니다.  
  
-   시간이 지남에 따라 변경되는 마스터 데이터의 감사 가능한 레코드를 유지 관리할 수 있습니다.  
  
-   사용자가 변경하지 못하게 하여 모든 데이터가 비즈니스 규칙에 적합하도록 할 수 있습니다.  
  
-   구독 시스템에서 사용할 모델을 잠글 수 있습니다.  
  
-   계층을 바로 구현하지 않고 여러 계층을 테스트할 수 있습니다.  
  
> [!NOTE]  
>  예를 들어 새 엔터티나 도메인 기반 특성을 만드는 경우와 같이 모델의 구조를 변경하면 변경 사항이 모든 버전에 적용됩니다. 이전 버전의 모델을 보면 엔터티 또는 특성이 표시되지만 실제로 존재하는 데이터는 없습니다.  
  
## <a name="version-flags"></a>버전 플래그  
 버전이 사용자 또는 구독 시스템에서 사용할 수 있도록 준비되면 버전을 식별할 플래그를 설정할 수 있습니다. 이 플래그는 필요에 따라 버전 간에 이동할 수 있습니다. 플래그는 사용자 및 구독 시스템이 사용할 모델 버전을 식별하는 데 유용합니다.  
  
## <a name="workflow-for-version-management"></a>버전 관리 워크플로  
 버전 관리에 사용하는 워크플로는 다음과 같습니다.  
  
1.  초기 버전은 모델을 만들고 회사의 마스터 데이터로 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 채우면 자동으로 만들어집니다. 사용 권한에 따라 사용자는 필요한 경우 이 버전을 변경할 수 있습니다.  
  
2.  모델의 버전을 커밋하려면 모델 관리자만 데이터를 업데이트할 수 있도록 버전을 잠급니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](administrators-master-data-services.md)를 참조 하세요. 알림이 구성된 경우 버전의 상태가 변경될 때마다 전자 메일 알림이 모델 관리자에게 전송됩니다. 자세한 내용은 [메일 알림 구성&#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)을 참조하세요.  
  
3.  잠긴 버전의 데이터에 비즈니스 규칙을 적용하고 유효성 검사 문제를 검토합니다. 필요한 경우 누락된 정보를 채우거나 문제의 원인이 되는 트랜잭션을 되돌릴 수 있습니다. 또한 사용자가 변경할 수 있도록 버전의 잠금을 해제할 수 있습니다.  
  
4.  모든 데이터가 유효성 검사를 통과하면 버전을 커밋하고 구독 시스템에서 사용하도록 버전에 플래그를 지정합니다. 커밋된 버전에는 변경 내용을 적용할 수 없습니다.  
  
5.  커밋된 버전을 복사하고 모델의 새 버전으로 작업을 시작할 수 있음을 사용자에게 알립니다.  
  
## <a name="sequential-or-simultaneous-versions"></a>순차 또는 동시 버전  
 모델의 순차 버전 또는 동시 버전을 만들 수 있습니다.  
  
-   **순차 버전.** 버전을 커밋할 때마다 새 복사본을 만들고 해당 버전에 다음 일련 번호를 부여합니다. 예를 들어 모델의 **버전 7** 을 복사하여 복사본의 이름을 **버전 8**로 지정할 수 있습니다.  
  
-   **동시 버전.** 둘 이상의 데이터 버전에서 동시에 작업하려는 경우 모델의 동시 버전을 만듭니다. 이는 정상적인 비즈니스 과정에 따른 조직 개편이나 합병 시 새 마스터 데이터를 기존 구조에 적합하게 만드는 방법을 확인하는 데 유용합니다.  
  
    > [!NOTE]  
    >  모든 버전을 복사할 수 있는지 아니면 커밋된 버전만 복사할 수 있는지는 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 의 설정에 따라 결정됩니다. 동시 버전을 만들려면 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서 모든 버전 복사를 허용하도록 구성해야 합니다. 이 설정은 시스템 설정 테이블에서도 사용 가능합니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|기존 버전의 이름을 변경합니다.|[버전 이름 변경&#40;Master Data Services&#41;](../../2014/master-data-services/change-a-version-name-master-data-services.md)|  
|관리자만 데이터를 편집할 수 있도록 버전을 잠급니다.|[버전 잠금&#40;Master Data Services&#41;](../../2014/master-data-services/lock-a-version-master-data-services.md)|  
|사용자가 데이터를 편집할 수 있도록 버전을 잠금 해제합니다.|[버전 잠금 해제&#40;Master Data Services&#41;](../../2014/master-data-services/unlock-a-version-master-data-services.md)|  
|모든 데이터의 유효성 검사를 마친 후 버전을 커밋합니다.|[버전 커밋&#40;Master Data Services&#41;](../../2014/master-data-services/commit-a-version-master-data-services.md)|  
|버전을 표시하는 새 플래그를 만듭니다.|[버전 플래그 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)|  
|기존 버전 플래그의 이름을 변경합니다.|[버전 플래그 이름 변경&#40;Master Data Services&#41;](../../2014/master-data-services/change-a-version-flag-name-master-data-services.md)|  
|기존 플래그를 버전에 할당합니다.|[버전에 플래그 할당&#40;Master Data Services&#41;](../../2014/master-data-services/assign-a-flag-to-a-version-master-data-services.md)|  
|기존 버전의 새 복사본을 만듭니다.|[버전 복사&#40;Master Data Services&#41;](../../2014/master-data-services/copy-a-version-master-data-services.md)|  
|기존 버전을 삭제합니다.|[버전 삭제&#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-version-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [트랜잭션 되돌리기&#40;Master Data Services&#41;](../../2014/master-data-services/reverse-a-transaction-master-data-services.md)  
  
-   [알림&#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)  
  
-   [비즈니스 규칙&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
