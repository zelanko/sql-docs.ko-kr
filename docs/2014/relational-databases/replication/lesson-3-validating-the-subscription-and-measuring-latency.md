---
title: '3단원: 구독 유효성 검사 및 대기 시간 측정 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
author: rothja
ms.author: jroth
ms.openlocfilehash: eba65b6b19054414a13a46ebd2ccb92a28305dde
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065880"
---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>3단원: 구독 유효성 검사 및 대기 시간 측정
  이 단원에서는 추적 프로그램 토큰을 사용하여 구독자에 변경 내용이 복제되는지 확인하고 대기 시간, 즉 게시자에서 변경한 내용이 구독자에게 표시될 때까지 걸리는 시간을 확인합니다. 이 단원을 수행하려면 이전 단원인 [2단원: 트랜잭션 게시에 구독 만들기](lesson-2-creating-a-subscription-to-the-transactional-publication.md)를 완료해야 합니다.  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>추적 프로그램 토큰을 삽입하고 이 토큰에 대한 정보를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결하고 서버 노드를 확장한 다음 **복제** 폴더를 마우스 오른쪽 단추로 클릭하고 **복제 모니터 시작**을 클릭합니다.  
  
     복제 모니터가 시작됩니다.  
  
2.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자 인스턴스를 확장한 다음 **AdvWorksProductTrans** 게시를 클릭합니다.  
  
3.  **추적 프로그램 토큰** 탭을 클릭합니다.  
  
4.  **추적 프로그램 삽입**을 클릭합니다.  
  
5.  **게시자에서 배포자로 연결 시 대기 시간**, **배포자에서 구독자로 연결 시 대기 시간**, **총 대기 시간**열에서 추적 프로그램 토큰에 대한 경과 시간을 확인합니다. **보류** 중 값은 토큰이 지정 된 지점에 도달 하지 않았음을 나타냅니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 단원에서는 추적 프로그램 토큰을 사용하여 데이터 변경 내용이 게시자에서 구독자로 복제되고 있는지 확인했습니다. 게시자의 **Product** 테이블에서 데이터를 삽입, 업데이트 또는 삭제할 수 있으며 이러한 변경 내용을 복제한 다음 구독자에서 **Product** 테이블을 쿼리하여 해당 변경 내용을 볼 수 있습니다.  
  
 이로써 계속 연결된 서버 간 데이터 복제 자습서를 마쳤습니다. 병합 복제를 사용하는 유사한 자습서를 보려면 [Tutorial: Replicating Data with Mobile Clients](tutorial-replicating-data-with-mobile-clients.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
