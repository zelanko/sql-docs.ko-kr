---
description: 스냅샷 에이전트(새 게시 마법사)
title: 스냅샷 에이전트(새 게시 마법사) | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 6dab75938bc65b741bd556447d140c57d9557184
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479704"
---
# <a name="snapshot-agent-new-publication-wizard"></a>스냅샷 에이전트(새 게시 마법사)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  스냅샷 에이전트는 새 구독을 초기화하는 데 사용되는 게시 스키마와 데이터가 포함된 파일을 만듭니다. 기본적으로 스냅샷 에이전트는 새 게시 마법사에서 게시가 생성된 후 즉시 실행됩니다. 이후에는 사용자가 지정한 일정에 따라 에이전트가 실행됩니다. 에이전트가 실행될 때마다 새 스냅샷 파일을 만들지 여부는 선택한 복제 유형 및 옵션에 따라 결정됩니다. 자세한 내용은 [스냅샷 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
 매개 변수가 있는 필터를 사용하는 병합 게시의 경우 게시 스냅샷이 완료된 후 각 데이터 파티션의 스냅샷을 만들어야 합니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을(를) 참조하세요.  
  
## <a name="options"></a>옵션  
 **즉시 스냅샷 만들기** (병합 복제) 또는 **즉시 스냅샷을 만들고 구독 초기화에 사용할 수 있도록 유지합니다** (트랜잭션 복제)  
 새 게시 마법사가 완료된 후 즉시 스냅샷을 만들려면 이 확인란을 선택합니다. 스냅샷을 생성하기 전에 **게시 속성** 대화 상자에서 스냅샷 속성을 변경하거나 스냅샷 없이 구독자를 초기화하려면 이 확인란의 선택을 취소합니다. 자세한 내용은 [스냅샷 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  마법사에서 배포 에이전트 또는 병합 에이전트에 대해 해당 작업을 시작하려면 배포자에 연결하라는 메시지를 표시할 수 있습니다.  
  
 **스냅샷 에이전트 실행 시간 예약**  
 스냅샷 에이전트 실행에 대한 기본 일정을 적용하거나 **변경** 을 클릭하여 다른 일정을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [초기 스냅샷 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [스냅샷으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
