---
title: "스냅숏 형식 지정(SQL Server Management Studio) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6787eaf33957f318d2c8b73c11b176ea78726b4e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>스냅숏 형식 지정(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] **게시 속성 - \<Publication>** 대화 상자의 **스냅숏** 페이지에서 스냅숏 형식을 지정합니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-specify-snapshot-format"></a>스냅숏 형식을 지정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에서 **네이티브 SQL Server - 모든 구독자는 SQL Server를 실행하는 서버여야 합니다** 또는 **문자 - 게시자 또는 구독자가 SQL Server를 실행하지 않는 경우 필요합니다**를 선택합니다.  
  
    > [!NOTE]  
    >  이 게시가 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 데이터베이스 또는[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외의 데이터베이스에 대한 구독을 지원해야 하는 경우가 아니면 네이티브 형식을 선택하는 것이 좋습니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [스냅숏 속성 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [스냅숏으로 구독 초기화](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
