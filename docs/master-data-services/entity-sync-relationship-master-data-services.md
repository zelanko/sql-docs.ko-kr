---
title: 엔터티 동기화 관계
description: 엔터티 동기화는 엔터티 버전 간의 반복 가능한 단방향 동기화로, MDS(Master Data Services) 모델 간에 엔터티 데이터를 공유할 수 있습니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0dac91e4f43d244e133511e792f29770949da905
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811947"
---
# <a name="entity-sync-relationship-master-data-services"></a>엔터티 동기화 관계(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  엔터티 동기화는 엔터티 버전 간의 반복 가능한 단방향 동기화입니다. 엔터티 동기화를 통해 여러 모델 간에 엔터티 데이터를 공유할 수 있습니다. 정보의 단일 원본을 모델 하나에 보관하고 다른 모델에서 이 마스터 데이터를 다시 사용할 수 있습니다. 예를 들어 미국의 주 데이터를 모델 엔터티 하나에 저장하여 다른 모델에서 해당 데이터를 다시 사용할 수 있습니다.  
  
 엔터티 동기화를 수행하여 데이터의 일회성 복사본을 만들 수도 있습니다.  
  
 소스 엔터티에 자유 형식 및 파일 특성이 포함되어 있는 모든 리프 멤버는 동기화 실행 중에 대상 엔터티와 동기화됩니다. 이 과정에서 엔터티 스키마와 멤버가 생성, 삭제 및 수정됩니다.  
  
 동기화 관계가 설정되고 나면 동기화 프로세스를 통해서만 대상 엔터티를 수정할 수 있습니다. 언제든지 동기화 관계를 제거하여 대상 엔터티를 편집 가능하도록 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services)&#41;&#40;엔터티 동기화 관계 만들기 및 실행](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [엔터티 동기화 관계 편집 및 삭제&#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
