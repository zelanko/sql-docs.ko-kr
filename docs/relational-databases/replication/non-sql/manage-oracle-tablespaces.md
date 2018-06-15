---
title: Oracle 테이블스페이스 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9a9f53d101cc0c201c879d14185d0079a7125a7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32959648"
---
# <a name="manage-oracle-tablespaces"></a>Oracle 테이블스페이스 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  테이블스페이스는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 파일 그룹과 개념이 거의 동일한 데이터베이스 저장소 단위입니다. 테이블스페이스를 사용하면 개별 그룹 내에서 데이터베이스 개체를 저장하고 관리할 수 있습니다. 자세한 내용은 Oracle 설명서를 참조하십시오.  
  
 테이블을 Oracle 게시의 일부로 구성하는 경우 복제 로깅 정보를 저장할 때 기존 Oracle 테이블스페이스를 사용하도록 선택적으로 지정할 수 있습니다. 지정하지 않으면 복제 개체에 대한 테이블스페이스가 게시자를 구성할 때 구성된 복제 관리 사용자 스키마와 연결된 기본 테이블스페이스가 됩니다.  
  
 **아티클 로깅 테이블에 대해 테이블스페이스를 지정하려면**   
  
-   **아티클 속성** 대화 상자에서 테이블스페이스를 지정합니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
-   [sp_changearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)을 사용합니다. **sp_changearticle**을 사용하려면 다음을 지정하십시오.  
  
    -   **@publisher** 매개 변수에 대한 Oracle 게시자의 이름  
  
    -   **@publication** 매개 변수에 대한 Oracle 게시의 이름  
  
    -   **@article** 매개 변수에 대한 아티클의 이름  
  
    -   **@property** 매개 변수에 대한 '테이블스페이스' 값  
  
    -   **@value** 매개 변수에 대한 테이블스페이스의 이름  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  
