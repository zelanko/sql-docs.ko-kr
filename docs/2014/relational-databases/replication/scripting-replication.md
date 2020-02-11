---
title: 복제 스크립팅 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server replication], replication objects
- merge replication scripting [SQL Server replication]
- replication [SQL Server], scripting
- snapshot replication [SQL Server], scripting
- scripts [SQL Server replication]
- transactional replication, scripting
ms.assetid: e50fac44-54c0-470c-a4ea-9c111fa4322b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55407c52c5fb7bf0c9537eaf8fb7a7d31d2675e1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250531"
---
# <a name="scripting-replication"></a>복제 스크립팅
  토폴로지의 모든 복제 구성 요소는 재해 복구 계획의 일부로 스크립팅되어야 하며 반복 태스크를 자동화하는 데도 스크립트를 사용할 수 있습니다. 스크립트에는 게시 또는 구독과 같은 스크립팅된 복제 구성 요소를 구현하는 데 필요한 Transact-SQL 시스템 저장 프로시저가 포함되어 있습니다. 스크립트는 마법사 (예: 새 게시 마법사) 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 구성 요소를 만든 후에 만들 수 있습니다. 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 **sqlcmd**를 사용하여 스크립트를 확인, 수정 및 실행할 수 있습니다. 백업 파일과 함께 스크립트를 저장하여 복제 토폴로지를 다시 구성할 때 사용할 수 있습니다.  
  
 속성 변경 내용이 적용되면 구성 요소를 다시 스크립팅해야 합니다. 트랜잭션 복제에서 사용자 지정 저장 프로시저를 사용할 경우 각 프로시저의 복사본을 스크립트와 함께 저장해야 합니다. 프로시저가 변경되면 복사본도 업데이트해야 합니다. 일반적으로 프로시저는 스키마가 변경되거나 애플리케이션 요구 사항이 변경될 때 업데이트됩니다. 사용자 지정 프로시저에 대한 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
 매개 변수가 있는 필터를 사용하는 병합 게시의 경우 게시 스크립트에는 데이터 파티션을 만드는 저장 프로시저 호출이 있습니다. 스크립트는 생성된 파티션에 대한 참조와 하나 이상의 파티션을 다시 만드는 방법(필요한 경우)을 제공합니다.  
  
## <a name="example-of-automating-a-task-with-scripts"></a>스크립트로 태스크를 자동화하는 예  
 
  [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]에서 병합 복제를 구현하여 원격 영업 사원에게 데이터를 배포한다고 가정합니다. 판매 담당자는 끌어오기 구독을 사용하여 자신의 지역에 있는 고객과 관련된 모든 데이터를 다운로드합니다. 오프라인으로 작업할 때 판매 담당자는 데이터를 업데이트하고 새로운 고객 및 주문을 입력합니다. 
  [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 에는 별개의 지역에 50개 이상의 판매 담당자가 있기 때문에 새 구독 마법사로 각 구독자에 별개의 구독을 만드는 데 많은 시간이 소요됩니다. 대신 복제 관리자가 다음 단계를 수행할 수 있습니다.  
  
1.  판매 담당자 또는 해당 지역을 기반으로 하여 파티션이 있는 필수 병합 게시를 설정합니다.  
  
2.  하나의 구독자에 대한 끌어오기 구독을 만듭니다.  
  
3.  해당 끌어오기 구독을 기반으로 하여 스크립트를 생성합니다.  
  
4.  구독자의 이름과 같은 값을 변경하여 스크립트를 수정합니다.  
  
5.  여러 구독자에서 스크립트를 실행하여 필요한 끌어오기 구독을 생성합니다.  
  
## <a name="script-replication-objects"></a>복제 개체 스크립팅  
 복제 마법사 또는 **** 의 복제[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 폴더에서 복제 개체를 스크립팅합니다. 마법사에서 스크립팅하는 경우 개체를 만들고 스크립팅하거나 스크립팅만 하도록 선택할 수 있습니다.  
  
> [!IMPORTANT]  
>  암호는 모두 NULL로 스크립팅됩니다. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정해야 합니다.  
  
 복제 마법사의 사용 방법은 다음을 참조하십시오.  
  
-   [게시 및 배포 구성](configure-publishing-and-distribution.md)  
  
-   [게시 만들기](publish/create-a-publication.md)  
  
-   [밀어넣기 구독 만들기](create-a-push-subscription.md)  
  
-   [끌어오기 구독 만들기](create-a-pull-subscription.md)  
  
#### <a name="to-script-an-object-from-a-replication-wizard"></a>복제 마법사에서 개체를 스크립팅하려면  
  
1.  마법사의 **마법사 동작** 페이지에서 마법사에 적합한 확인란을 선택합니다.  
  
    -   **게시를 만드는 단계를 포함 하는 스크립트 파일 생성**  
  
    -   **구독을 만드는 단계를 포함 하는 스크립트 파일 생성**  
  
    -   **배포를 구성 하는 단계를 포함 하는 스크립트 파일 생성**  
  
2.  
  **스크립트 파일 속성** 페이지에서 옵션을 지정합니다.  
  
3.  마법사를 완료합니다.  
  
#### <a name="to-script-an-object-from-management-studio"></a>Management Studio에서 개체를 스크립팅하려면  
  
1.  
  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 배포자, 게시자 또는 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  
  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더나 **로컬 구독** 폴더를 확장합니다.  
  
3.  게시 또는 구독을 마우스 오른쪽 단추로 클릭한 다음 **스크립트 생성**을 클릭합니다.  
  
4.  
  **SQL 스크립트 생성 - \<ReplicationObject>** 대화 상자의 옵션을 지정합니다.  
  
5.  
  **파일로 스크립팅**을 클릭합니다.  
  
6.  
  **스크립트 파일 위치** 대화 상자에 파일 이름을 입력한 다음 **저장**을 클릭합니다. 상태 메시지가 표시됩니다.  
  
7.  **확인**을 클릭 한 다음 **닫기**를 클릭 합니다.  
  
#### <a name="to-script-multiple-objects-from-management-studio"></a>Management Studio에서 여러 개체를 스크립팅하려면  
  
1.  
  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 배포자, 게시자 또는 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  
  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **스크립트 생성**을 클릭합니다.  
  
3.  
  **SQL 스크립트 생성** 대화 상자에서 옵션을 지정합니다.  
  
4.  
  **파일로 스크립팅**을 클릭합니다.  
  
5.  
  **스크립트 파일 위치** 대화 상자에 파일 이름을 입력한 다음 **저장**을 클릭합니다. 상태 메시지가 표시됩니다.  
  
6.  
  **확인** 을 클릭한 다음 **닫기**를 클릭합니다.  
  
  
