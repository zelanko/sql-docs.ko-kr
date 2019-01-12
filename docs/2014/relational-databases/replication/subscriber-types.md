---
title: 구독자 유형 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9445c7b366a43253da4accabaf98d9c5b7f8d92
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134943"
---
# <a name="subscriber-types"></a>구독자 유형
  병합 복제를 사용하여 게시가 지원해야 하는 구독자 유형을 지정할 수 있습니다. 구독자 유형을 선택하면 게시에서 사용할 수 있는 기능을 결정하는 *게시 호환성 수준*이 설정됩니다.  
  
 게시 스냅숏을 만든 후 **게시 속성** 대화 상자의 **일반** 페이지에서 게시 호환성 수준을 높여 제한을 강화할 수 있습니다. 호환성 수준은 낮출 수 없습니다.  
  
## <a name="options"></a>변수  
 이 게시가 지원해야 하는 각 구독자 유형을 선택합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 게시가 모든 기능을 사용할 수 있습니다.  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 게시에서 사용하는 스냅숏 파일이 문자 형식이어야 합니다. 이는 스냅숏 에이전트에서 자동으로 처리됩니다. 또한[!INCLUDE[ssEW](../../includes/ssew-md.md)] 에는 호환성 수준과 관련되지 않은 제한 사항이 많이 있습니다.  
  
 이 옵션을 선택하면 게시에 웹 동기화 옵션을 사용할 수 있습니다. 웹 동기화에 대한 자세한 내용은 [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 및 데이터베이스 개체 게시](publish/publish-data-and-database-objects.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [배포자 및 게시자 속성 보기 및 수정](view-and-modify-distributor-and-publisher-properties.md)   

  
