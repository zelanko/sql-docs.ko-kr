---
title: 스냅숏 적용 전후에 스크립트 실행 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 59a73607859d9c1858f09698dc30aee9d018ce26
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851111"
---
# <a name="execute-scripts-before-and-after-a-snapshot-is-applied"></a>스냅숏 적용 전후에 스크립트 실행
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에 적용되기 전 또는 후에 실행할 스크립트를 선택적으로 지정합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
> [!NOTE]  
>  이러한 옵션은 **스냅숏 형식** 옵션이 **문자**로 설정된 경우에는 사용할 수 없습니다.  
  
### <a name="to-execute-a-script-before-or-after-a-snapshot-is-applied"></a>스냅숏 적용 전후에 스크립트를 실행하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에서 다음을 수행합니다.  
  
    -   스냅숏이 적용되기 전에 실행할 스크립트를 지정하려면 **찾아보기** 를 클릭하여 스크립트로 이동하거나 **스냅숏 적용 전 다음 스크립트 실행** 입력란에 스크립트의 경로를 입력합니다.  
  
        > [!NOTE]  
        >  배포 에이전트 또는 병합 에이전트에는 지정한 디렉터리에 대한 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\scripts\myscript.sql과 같이 UNC(Universal Naming Convention) 경로로 지정해야 합니다.  
  
    -   스냅숏이 적용된 후에 실행할 스크립트를 지정하려면 **찾아보기** 를 클릭하여 스크립트로 이동하거나 **스냅숏 적용 후 다음 스크립트 실행** 입력란에 스크립트의 UNC 경로를 입력합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [스냅숏 속성 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [스냅숏 적용 전후에 스크립트 실행](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
