---
title: Microsoft 복제 충돌 뷰어(트랜잭션 복제) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.cvqueued.f1
ms.assetid: eec59d8e-cadb-4623-a31f-9f42ec09c97f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 293048b191fff03b11b7e28d7778a34793b4c7f2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788393"
---
# <a name="microsoft-replication-conflict-viewer-transactional-replication"></a>Microsoft 복제 충돌 뷰어(트랜잭션 복제)
  복제 충돌 뷰어에서는 지연 업데이트 구독을 사용하는 트랜잭션 복제 및 피어 투 피어 트랜잭션 복제에서 동기화 중 발생한 충돌을 볼 수 있습니다. 자세한 내용은 [트랜잭션 게시의 데이터 충돌 확인&#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)을 참조하세요.  
  
> [!NOTE]  
>  복제 충돌 뷰어에는 병합 복제 및 트랜잭션 복제에서 발생하는 충돌이 표시됩니다. 트랜잭션 복제의 경우 복제 충돌 뷰어를 사용하여 충돌 데이터를 볼 수는 있지만 충돌에 대한 다른 해결 방법을 선택할 수는 없습니다.  
  
## <a name="options"></a>변수  
 복제 충돌 뷰어는 두 개의 섹션으로 나뉘어져 있습니다. 대화 상자의 위쪽 섹션에 선택한 테이블의 충돌 목록이 표시됩니다. 충돌 목록에서 항목을 클릭하면 대화 상자의 아래쪽 섹션에 해당 충돌에 대한 세부 정보가 표시됩니다.  
  
 아래쪽 섹션에서 충돌 데이터는**충돌 시 적용되는 내용** 및 **충돌 시 변경 내용 무시**중 해당하는 열에 표시됩니다. 업데이트된 데이터와 삭제된 데이터 간에 충돌이 있다면 충돌 시 삭제된 쪽을 표시하는 데이터는 없습니다. 이 경우 복제 충돌 뷰어에서는 행이 한 위치에서 삭제되었고 다른 위치에서는 업데이트되었음을 나타내는 메시지를 열 중 하나에 표시합니다. 권장 해결 방법도 표시됩니다.  
  
 **데이터베이스 백업**  
 충돌이 발생한 게시가 포함된 데이터베이스를 선택합니다.  
  
 **게시**  
 충돌이 발생한 테이블이 포함된 게시를 선택합니다.  
  
 **테이블**  
 충돌이 발생한 테이블을 선택합니다.  
  
 **필터 정의**  
 **필터 정의** 대화 상자를 열려면 클릭합니다.  
  
 **필터 적용 또는 제거**  
 **필터 정의** 대화 상자에서 정의한 필터를 적용하거나 제거하려면 클릭합니다.  
  
 **모두 선택**  
 표에 나열된 모든 충돌을 선택하려면 클릭합니다.  
  
 **모두 선택 안 함**  
 표에 나열된 모든 충돌의 선택을 취소하려면 클릭합니다.  
  
 **제거**  
 선택한 충돌을 뷰어에서 제거하고 연결된 메타데이터를 복제 시스템 테이블에서 제거하려면 클릭합니다.  
  
 **모든 열 표시**  
 테이블의 모든 열을 표시하려면 선택합니다.  
  
 **처음 다섯 개의 열 및 충돌하는 데이터를 포함하는 기타 열 표시**  
 처음 5개 열과 충돌이 발생한 기타 모든 열을 표시하려면 선택합니다. 이 옵션은 테이블에 많은 열이 있지만 충돌 해결에 가장 도움이 되는 열만 보려는 경우에 유용합니다. 기본 키 또는 이름 필드와 같이 행을 식별하는 필드가 테이블의 앞쪽 열에 포함되어 있는 경우가 많으므로 처음 5개 열은 항상 이 뷰에 포함됩니다.  
  
 **열 정보 표시**(**…**)  
 테이블 이름, 열 이름, **테이블 이름**, **열 이름**합니다 **데이터 형식**, 및 **열 값**합니다.  
  
 **이 충돌 정보 기록**  
 자세한 충돌 정보를 파일에 기록하려면 이 확인란을 선택합니다. 파일 위치를 지정하려면 **보기** 메뉴를 가리키고 **옵션**을 클릭합니다. 값을 입력하거나 찾아보기 (**...**)를 클릭한 다음 해당 파일로 이동합니다. **확인** 을 클릭하여 **옵션** 대화 상자를 종료합니다.  
  
## <a name="see-also"></a>관련 항목  
 [피어 투 피어 복제에서 충돌 검색](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [트랜잭션 게시의 데이터 충돌 확인&#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
  
