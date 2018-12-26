---
title: COM 기반 사용자 지정 해결 프로그램 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: 94195797-ad7a-4962-a8e3-b259cd13aa38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 09c5b51db06cc41153441d155c2d5292f505705d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673621"
---
# <a name="advanced-merge-replication-conflict---com-based-custom-resolvers"></a>고급 병합 복제 충돌 - COM 기반 사용자 지정 해결 프로그램
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사용자 지정 해결 프로그램은 기본 해결 메커니즘보다 더 높은 유연성을 제공하며 복제된 데이터를 사용하여 애플리케이션에 필요한 비즈니스 논리를 구현할 수 있습니다. COM 기반 사용자 지정 해결 프로그램은 DLL(동적 연결 라이브러리)이며 **ICustomResolver** COM 인터페이스, 해당 메서드 및 속성, 그리고 충돌 해결을 위해 특별히 디자인된 다른 지원 인터페이스 및 유형 정의를 구현합니다.  
  
> [!NOTE]  
>  가능하면 COM 기반 사용자 지정 해결 프로그램보다 비즈니스 논리 처리기를 사용하는 것이 좋습니다. 비즈니스 논리 처리기에 대한 자세한 내용은 [병합 동기화 중 비즈니스 논리 실행](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)을 참조하세요.  
  
 사용자 지정 COM 해결 프로그램을 작성하려면 replrec.dll에 제공된 형식 라이브러리를 사용합니다. 기본적으로 이 라이브러리는 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM에 설치됩니다.  
  
 사용자 지정 COM 해결 프로그램을 작성하기 전 다음 사항을 결정해야 합니다.  
  
-   해결하려는 행 변경의 유형(예: 업데이트, 삽입 및 삭제) 및 해결 프로그램을 병합 변경 내용을 업로드하는 동안 호출할지 병합 변경 내용을 다운로드하는 동안 호출할지 또는 두 작업 모두를 수행하는 동안 호출할지 여부. 사용자는 하나의 변경 내용, 모든 변경 내용 또는 변경 내용이 조합된 것의 유형을 지정할 수 있습니다. 기본 병합 충돌 해결 프로그램은 사용자 지정 해결 프로그램이 해결하지 못하는 충돌을 처리합니다.  
  
-   충돌 해결 시 열 추적의 사용 여부. 열 추적이 설정되어 있으면 충돌이 존재하는 열의 데이터만 충돌로 플래그가 지정되며, 그렇지 않을 경우에 데이터는 병합됩니다. 그러나 충돌은 행 수준 추적에서와 같은 방법으로 해결됩니다. 즉, 우선 순위 적용 항목이 데이터 전체 행을 덮어씁니다. 그러나 데이터는 게시자나 구독자의 값 또는 게시자 및 구독자가 아닌 위치의 일부 변경된 값이 혼합된 것일 수 있습니다. 자세한 내용은 [병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)을 참조하세요.  
  
 COM 기반 사용자 지정 충돌 해결 프로그램을 구현하려면 [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)을 참조하십시오.  
  
 사용자 지정 해결 프로그램은 전체 게시에 대해서가 아니라 아티클에 대해 지정됩니다. 하나 이상의 아티클에 대해서 동일한 해결 프로그램을 사용할 수 있지만 사용자 지정 해결 프로그램의 논리는 특정 테이블에만 적용되는 경우가 많습니다. 해결 프로그램을 만든 후 아티클에 사용되는 테이블을 수정하면(예: 충돌 해결에 사용되는 열 이름 변경) 사용자 지정 해결 프로그램을 수정하고 다시 컴파일해야 할 수 있습니다.  
  
 사용자 지정 해결 프로그램을 지정하려면 [병합 아티클 해결 프로그램 지정](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Microsoft COM-Based Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)  
  
  
