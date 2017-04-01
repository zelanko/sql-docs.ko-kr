---
title: "대체 스냅숏 폴더 위치 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "스냅숏 [SQL Server 복제], 대체 폴더 위치"
  - "스냅숏 복제 [SQL Server], 대체 폴더 위치"
  - "대체 스냅숏 폴더 [SQL Server 복제]"
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 대체 스냅숏 폴더 위치
  대체 스냅숏 위치를 사용하면 기본 위치가 아닌 위치(일반적으로 배포자에 위치)에 스냅숏 파일을 저장할 수 있습니다. 대체 위치는 다른 서버, 다른 네트워크 드라이브 또는 이동식 미디어(CD-ROM, 이동식 디스크)가 될 수 있습니다.  
  
 대체 스냅숏 위치는 게시의 속성으로 저장됩니다. 대체 스냅숏 위치가 게시 속성이기 때문에 배포 에이전트 및 병합 에이전트에서는 동화 프로세스의 일부인  올바른 스냅숏을 찾을 수 있습니다.  
  
 대체 스냅숏 폴더 위치를 지정하거나 스냅숏 파일을 압축하려면 초기 스냅숏을 즉시 만들지 말고 게시를 만들어 스냅숏 위치에 대한 게시 속성을 설정한 다음 해당 게시에 대해 스냅숏 에이전트를 실행합니다. 초기 스냅숏을 만든 다음 대체 위치를 변경할 경우 게시에 대해 생성된 스냅숏의 위치는 새 대체 위치로 다시 지정할 수 없습니다. 이 경우 게시 설정에 따라 병합 에이전트나 배포 에이전트가 새 대체 위치에서 스냅숏 파일을 찾지 못할 수 있습니다.  
  
> [!NOTE]  
>  대체 위치를 지정 하지 않으면 (사용 하는 **게시 속성** 대화 상자 또는 [sp_changepublication (& a) #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)) 이것이 기본 스냅숏 폴더 위치와 동일 합니다.  
  
> [!CAUTION]  
>  WebSync 및 대체 스냅숏 폴더 위치를 동시에 사용하지 마십시오.  
  
 **대체 스냅숏 위치를 지정하려면**  
  
-   [! INCLUDE [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [Specify an Alternate Snapshot Folder Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   복제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래밍: [스냅숏 속성 구성 및 #40; 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## 참고 항목  
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [스냅숏 옵션](../../relational-databases/replication/snapshot-options.md)  
  
  