---
title: 병합 복제 충돌 감지 및 해결 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- conflict resolution [SQL Server replication]
- viewing merge replication conflicts
- resolving merge replication conflicts
- articles [SQL Server replication], conflict resolution
- merge replication conflict resolution [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 0d033c76-e8c9-4e35-ab95-4d335abb18c1
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 445314a89fabf4975c303a71ee1ae777b7f574ca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089536"
---
# <a name="detect-and-resolve-merge-replication-conflicts"></a>병합 복제 충돌 감지 및 해결
  게시자와 구독자가 연결되고 동기화가 이루어지면 병합 에이전트는 충돌이 있는지 감지합니다. 충돌이 감지되면 병합 에이전트는 충돌 해결 프로그램을 사용해서 다른 사이트로 수락 및 전파할 데이터를 확인합니다.  
  
> [!NOTE]  
>  구독자와 게시자가 동기화되는 경우에도 충돌은 대체로 구독자 및 게시자에서 수행되는 업데이트가 아닌 여러 구독자에서 수행되는 업데이트 사이에서 발생합니다.  
  
 병합 복제는 충돌을 감지하고 해결하는 다양한 방법을 제공합니다. 대부분의 응용 프로그램에는 기본 방법이 적합합니다.  
  
-   게시자와 구독자 사이에 충돌이 발생하면 게시자 변경 내용이 유지되고 구독자 변경 내용은 삭제됩니다.  
  
-   클라이언트 구독(가져오기 구독의 기본 유형)을 사용하는 두 구독자 사이에 충돌이 발생하면 게시자와 동기화하는 첫 번째 구독자의 변경 내용이 유지되고 두 번째 구독자의 변경 내용은 삭제됩니다. 클라이언트 및 서버 구독을 지정하는 방법에 대한 자세한 내용은 [병합 구독 유형 및 충돌 해결 우선 순위 지정&#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md)을 참조하세요.  
  
-   서버 구독(밀어넣기 구독의 기본 유형)을 사용하는 두 구독자 사이에 충돌이 발생하면 우선 순위가 가장 높은 구독자의 변경 내용이 유지되고 두 번째 구독자의 변경 내용은 삭제됩니다. 우선 순위 값이 같으면 게시자와 동기화하는 첫 번째 구독자의 변경 내용이 유지됩니다.  
  
 병합 복제의 충돌 감지 및 해결에 대한 자세한 내용은 [Advanced Merge Replication Conflict Detection and Resolution](advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [병합 복제를 위한 아티클 옵션](article-options-for-merge-replication.md)   
 [게시 구독](../subscribe-to-publications.md)  
  
  