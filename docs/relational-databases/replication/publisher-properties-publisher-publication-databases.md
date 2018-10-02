---
title: 게시자 속성 - 게시자, 게시 데이터베이스 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.pubproperties.pubdb.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: 574ea2e7-4e7b-4733-ab52-429ca93c7b0a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0a6ddaceec34bd56757efd6330dd863e2ff94db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775801"
---
# <a name="publisher-properties---publisher-publication-databases"></a>게시자 속성 - 게시자, 게시 데이터베이스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **게시자 속성** 대화 상자의 **게시 데이터베이스** 페이지를 사용하여 **sysadmin** 고정 서버 역할의 사용자가 복제용 데이터베이스를 설정할 수 있습니다. 데이터베이스를 설정한다고 해서 그 데이터베이스가 게시되는 것은 아닙니다. 데이터베이스를 설정하면 설정된 데이터베이스에 대한 **db_owner** 고정 데이터베이스 역할의 사용자가 그 데이터베이스에 하나 이상의 게시를 만들 수 있습니다.  
  
## <a name="options"></a>Options  
 **트랜잭션**  
 **db_owner** 고정 데이터베이스 역할의 사용자가 데이터베이스에 스냅숏 게시 또는 트랜잭션 게시를 만들 수 있게 하려면 이 확인란을 선택합니다.  
  
 **병합**  
 **db_owner** 고정 데이터베이스 역할의 사용자가 데이터베이스에 병합 게시를 만들 수 있게 하려면 이 확인란을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [속성 참조&#40;복제&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
