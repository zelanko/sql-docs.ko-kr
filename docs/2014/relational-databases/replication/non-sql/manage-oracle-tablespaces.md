---
title: Oracle 테이블스페이스 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9a6bf22c7649646506b65628f556b52fead23375
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63022293"
---
# <a name="manage-oracle-tablespaces"></a>Oracle 테이블스페이스 관리
  테이블 스페이스는의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]파일 그룹과 거의 동일한 데이터베이스 저장소 단위입니다. 테이블스페이스를 사용하면 개별 그룹 내에서 데이터베이스 개체를 스토리지하고 관리할 수 있습니다. 자세한 내용은 Oracle 설명서를 참조하십시오.  
  
 테이블을 Oracle 게시의 일부로 구성하는 경우 복제 로깅 정보를 저장할 때 기존 Oracle 테이블스페이스를 사용하도록 선택적으로 지정할 수 있습니다. 지정하지 않으면 복제 개체에 대한 테이블스페이스가 게시자를 구성할 때 구성된 복제 관리 사용자 스키마와 연결된 기본 테이블스페이스가 됩니다.  
  
 **아티클 로깅 테이블에 대해 테이블 스페이스를 지정 하려면 다음을**수행 합니다.  
  
-   
  **아티클 속성** 대화 상자에서 테이블스페이스를 지정합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](../publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
-   
  [sp_changearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)을 사용합니다. 
  **sp_changearticle**을 사용하려면 다음을 지정하십시오.  
  
    -   매개 변수에 **@publisher**대 한 Oracle 게시자의 이름입니다.  
  
    -   매개 변수에 **@publication**대 한 Oracle 게시의 이름입니다.  
  
    -   매개 변수에 **@article**대 한 아티클의 이름입니다.  
  
    -   매개 변수에 **@property**대 한 ' 테이블 스페이스 ' 값입니다.  
  
    -   매개 변수에 **@value**대 한 테이블 스페이스의 이름입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자 구성](configure-an-oracle-publisher.md)   
 [Oracle 게시자에서 생성 된 개체](objects-created-on-the-oracle-publisher.md)  
  
  
