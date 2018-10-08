---
title: 구독자 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subscribers.f1
helpviewer_keywords:
- Subscribers [SQL Server replication]
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 16c55f72efc2cd2abe63300fc7cfaecc56776064
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691142"
---
# <a name="subscribers"></a>게시자 속성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  선택한 게시에 대한 구독을 받을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자를 지정합니다.  
  
## <a name="options"></a>Options  
 **구독자**  
 표에서 확인란을 선택하여 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 데이터 원본을 **게시** 페이지에서 선택한 게시에 대한 구독자로 설정할 수 있습니다. 구독자가 나열되어 있지 않은 경우 **구독자 추가** 또는 **SQL Server 구독자 추가**를 클릭합니다.  
  
 **구독 데이터베이스**  
 이 열에 표시되는 정보 및 사용 가능한 동작은 **구독자** 열에 나열된 구독자 유형에 따라 달라집니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자의 경우 **구독 데이터베이스** 목록에서 구독 데이터베이스를 선택하거나 동일한 목록에서 **새 데이터베이스** 명령을 선택하여 새 데이터베이스를 만듭니다.  
  
    > [!NOTE]  
    >  게시자를 구독자로 설정하는 경우 구독 데이터베이스가 게시 데이터베이스와 달라야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자의 경우 구독 데이터베이스가 표시되지 않습니다. **SQL Server 이외 구독자 추가** 대화 상자의 **데이터 원본 이름** 필드에 데이터베이스 및 기타 연결 정보를 지정합니다. **구독자 추가** 를 클릭한 다음 **SQL Server 이외 구독자 추가**를 클릭하여 이 대화 상자를 사용할 수 있습니다.  
  
 **구독자 추가**  
 구독자로 설정할 수 있는 서버 목록에 서버를 추가합니다. 이 단추는 다음 조건이 모두 충족되는 경우 표시됩니다.  
  
-   선택한 게시가 구독 업데이트를 지원하지 않는 스냅숏 또는 트랜잭션 게시입니다.  
  
    > [!NOTE]  
    >  사용자가 구독하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독 및 게시가 있는 게시를[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자가 사용할 수 없을 경우 사용자는[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독을 추가할 수 없습니다.  
  
-   구독이 밀어넣기 구독입니다.  
  
-   선택한 게시의 게시자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전입니다.  
  
 **구독자 추가** 를 클릭하면 **SQL Server 구독자 추가** 및 **SQL Server 이외 구독자 추가**의 두 선택 사항으로 메뉴가 표시됩니다. Oracle 또는 IBM DB2 구독자를 추가하려면 **SQL Server 이외 구독자 추가** 를 클릭합니다.  
  
 **SQL Server 구독자 추가**  
 구독자로 설정할 수 있는 서버 목록에 서버를 추가합니다. 이 단추는 다음 조건 중 하나 이상이 충족되는 경우 표시됩니다.  
  
-   선택한 게시가 병합 게시이거나 구독 업데이트를 지원하는 스냅숏 또는 트랜잭션 게시입니다.  
  
-   구독이 끌어오기 구독입니다.  
  
-   선택한 게시의 게시자가 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]이전 버전입니다. 이전 버전의 경우 이 단추는 다음 조건 중 하나 이상이 충족되는 경우 표시됩니다.  
  
    -   사용자가 게시자에서 **sysadmin** 고정 서버 역할의 멤버입니다.  
  
    -   **게시자 속성** 대화 상자의 **구독자** 페이지에서 구독자가 추가되었습니다.  
  
    -   게시에서 익명 구독을 허용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
