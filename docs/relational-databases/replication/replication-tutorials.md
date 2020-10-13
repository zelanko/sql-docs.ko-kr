---
title: 복제 자습서 | Microsoft 문서
description: 이 자습서를 사용하여 SQL Server에서 복제를 위해 서버를 준비한 다음 트랜잭션 및 병합 복제를 구성하는 방법을 알아볼 수 있습니다.
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- walkthroughs [SQL Server replication]
- replication [SQL Server], tutorials
ms.assetid: 19fbd10e-5b59-4cd0-a988-52d5d9206242
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: ab482e4818d7d60b9876fbf300a39de0b2f9ee40
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868386"
---
# <a name="replication-tutorials"></a>복제 자습서
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
복제는 서버 간에 데이터 또는 데이터의 하위 집합을 이동시키는 강력한 솔루션입니다. 트랜잭션 복제를 사용하여 완전히 연결된 서버 간에 데이터를 복제할 수 있습니다. 병합 복제를 사용하여 가끔 연결되는 서버와 클라이언트 간에 데이터를 복제할 수도 있습니다. 이 문서에서 복제를 위해 서버를 준비하는 데 도움이 되는 자습서를 찾은 다음, 트랜잭션 및 병합 복제 복제를 구성하는 방법을 알아볼 수 있습니다. 
  
복제 자습서에서 "게시자"는 복제되고 있는 원본 데이터가 포함된 서버를 가리킵니다. "구독자"는 대상 서버를 가리킵니다. 게시자와 구독자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 같은 인스턴스를 공유할 수 있지만 반드시 이렇게 해야 하는 것은 아닙니다. 자세한 내용은 [복제 게시 모델 개요](../../relational-databases/replication/publish/replication-publishing-model-overview.md)를 참조하세요.  

이러한 자습서에서는 NODE1\SQL2016을 게시자 및 배포자로 사용하고 NODE2\SQL2016을 구독자로 사용합니다. 
  
> [!NOTE]  
> 이 자습서에 표시된 대부분의 태스크는 프로그래밍 방식으로 수행할 수 있습니다. 자세한 내용은 [복제 개발자 설명서](../../relational-databases/replication/concepts/replication-developer-documentation.md)를 참조하세요.  
  
## <a name="replication-tutorials"></a>복제 자습서  
[자습서: 복제를 위한 SQL Server 준비(게시자, 배포자, 구독자)](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
최소의 권한을 사용하여 복제를 실행할 수 있도록 서버를 준비하는 방법을 배웁니다. 다른 복제 자습서로 넘어가기 전에 이 자습서를 마쳐야 합니다.  
  
[자습서: 두 개의 완전히 연결된 서버 간 복제 구성(트랜잭션)](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

완전히 연결된 서버 간에 데이터를 복제하도록 트랜잭션 복제를 구성하는 방법을 알아봅니다. 이 자습서에는 몇 가지 기본적인 오류 해결 방법도 포함되어 있습니다. 

  
[자습서: 서버와 모바일 클라이언트 간의 복제 구성(병합)](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

한 서버와 가끔 연결되는 하나 이상의 클라이언트 간에 데이터를 교환하도록 병합 복제를 구성하는 방법을 배웁니다.  
  
## <a name="see-also"></a>참고 항목  
[복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md) 

[트랜잭션 복제 개요](./transactional/transactional-replication.md) 

[병합 복제 개요](./merge/merge-replication.md)

