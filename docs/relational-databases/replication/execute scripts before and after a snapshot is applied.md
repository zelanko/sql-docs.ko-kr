---
title: "스냅숏 적용 전후에 스크립트 실행(SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "스냅숏 [SQL Server 복제], 스크립트"
  - "스크립트 [SQL Server 복제], 스냅숏"
  - "스냅숏 복제 [SQL Server], 스크립트"
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 스냅숏 적용 전후에 스크립트 실행(SQL Server Management Studio)
  앞에 스냅숏이 적용 된 후 또는 실행 하는 선택적 스크립트를 지정 된 **스냅숏** 의 페이지는 **게시 속성-\< 게시>** 대화 상자. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
> [!NOTE]  
>  이 옵션을 사용할 수 없는 경우는 **스냅숏 형식** 옵션을 설정 **문자**합니다.  
  
### 스냅숏 적용 전후에 스크립트를 실행하려면  
  
1.  에 **스냅숏** 의 페이지는 **게시 속성-\< 게시>** 대화 상자:  
  
    -   스냅숏이 적용되기 전에 실행할 스크립트를 지정하려면 **찾아보기** 를 클릭하여 스크립트로 이동하거나 **스냅숏 적용 전 다음 스크립트 실행** 입력란에 스크립트의 경로를 입력합니다.  
  
        > [!NOTE]  
        >  배포 에이전트 또는 병합 에이전트에는 지정한 디렉터리에 대한 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용 하는 경우 지정 해야 하는 공유 디렉터리 범용 명명 규칙 (UNC) 경로와 같은 \\\computername\scripts\myscript.sql 합니다.  
  
    -   스냅숏이 적용된 후에 실행할 스크립트를 지정하려면 **찾아보기** 를 클릭하여 스크립트로 이동하거나 **스냅숏 적용 후 다음 스크립트 실행** 입력란에 스크립트의 UNC 경로를 입력합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 참고 항목  
 [스냅숏 속성 및 #40; 구성 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [스냅숏 적용 전후에 스크립트 실행](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  