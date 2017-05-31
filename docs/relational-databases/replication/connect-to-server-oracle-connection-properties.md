---
title: "서버에 연결(Oracle), 연결 속성 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.oracleconnection.connectionprops.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f65a185a723debd6ff1e8d2d240409521fe4c50f
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-oracle-connection-properties"></a>서버에 연결(Oracle), 연결 속성
  **서버에 연결** 대화 상자의 **연결 속성** 탭을 사용하여 **게이트웨이** 또는 **전체**게시 옵션을 지정할 수 있습니다. 게시자를 식별한 다음에 이 옵션을 변경하려면 해당 게시자를 삭제하고 다시 구성해야 합니다. 자세한 내용은 [Oracle 게시자 구성](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **게시자 유형**  
 **게이트웨이** 또는 **전체**를 선택합니다. **전체** 옵션은 Oracle 게시에 대해 지원되는 완전한 기능 집합을 스냅숏 및 트랜잭션 게시에 제공하도록 디자인되었습니다. **게이트웨이** 옵션은 복제가 시스템 간의 게이트웨이로 사용되는 경우 성능을 향상시킬 수 있도록 특정 디자인 최적화를 제공합니다. 동일한 테이블을 여러 트랜잭션 게시에 게시하려는 경우에는 **게이트웨이** 옵션을 사용할 수 없습니다. **게이트웨이**를 선택하면 트랜잭션 게시의 경우 특정 테이블이 한 번만 나타날 수 있지만 스냅숏 게시의 경우에는 이러한 제한이 없습니다.  
  
 **제한 시간**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자가 제한 시간 오류가 발생할 때까지 Oracle 게시자에 연결을 시도하는 시간을 지정합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Oracle 게시를 위한 용어 설명](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Performance Tuning for Oracle Publishers](../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
