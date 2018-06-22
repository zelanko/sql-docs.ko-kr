---
title: SQL Server 복제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
caps.latest.revision: 57
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e2e6c94d70c3e4fc469653ff5abba17a2b7c22c4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079005"
---
# <a name="sql-server-replication"></a>SQL  Server  복제
  복제는 한 데이터베이스에서 다른 데이터베이스로 데이터와 데이터베이스 개체를 복사 및 배포한 다음 데이터베이스 간에 동기화를 수행하여 일관성을 유지하는 일련의 기술입니다. 복제를 사용하면 LAN 및 WAN, 전화 접속 연결, 무선 연결 및 인터넷을 통해 데이터를 여러 다른 위치로 배포하고 원격 또는 모바일 사용자에게 배포할 수 있습니다.  
  
 트랜잭션 복제는 일반적으로 확장성 및 가용성 향상, 데이터 웨어하우징 및 보고, 여러 사이트의 데이터 통합, 다른 유형의 데이터 통합, 일괄 처리 작업 오프로드 등을 포함하여 높은 처리량이 필요한 서버 간 시나리오에서 사용됩니다. 병합 복제는 주로 데이터 충돌 가능성이 있는 모바일 응용 프로그램이나 분산 서버 응용 프로그램에 사용됩니다. 일반적인 시나리오에는 모바일 사용자와 데이터 교환, 소비자 POS(Point of Sale) 응용 프로그램, 여러 사이트의 데이터 통합 등이 있습니다. 스냅숏 복제는 트랜잭션 및 병합 복제에 초기 데이터 집합을 제공하는 데 사용되며 전체 데이터 새로 고침이 적합한 경우에도 사용할 수 있습니다. 이러한 3가지 복제 유형을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 엔터프라이즈 데이터를 동기화하는 강력하고 유연성 있는 시스템을 제공합니다. SQLCE 3.5 및 SQLCE 4.0에 대한 복제는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 및 [!INCLUDE[win8](../../includes/win8-md.md)]에서 지원됩니다.  
  
 복제 대신 Microsoft Sync Framework를 사용하여 데이터베이스를 동기화할 수도 있습니다. Sync Framework에는 구성 요소뿐 아니라 SQL Server, SQL Server Express, SQL Server Compact, SQL Azure 데이터베이스 간의 동기화를 용이하게 하는 유연하고 직관적인 API를 포함하고 있습니다. 또한 Sync Framework는 SQL Server 데이터베이스와 ADO.NET 호환 기타 데이터베이스 간에 동기화하도록 조정할 수 있는 클래스를 포함합니다. Sync Framework 데이터베이스 동기화 구성 요소에 대한 자세한 설명서는 [데이터베이스 동기화](http://go.microsoft.com/fwlink/?LinkId=209079)를 참조하십시오. Sync Framework에 대한 개요는 [Microsoft Sync Framework 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=209078)를 참조하십시오. Sync Framework와 병합 복제 간의 비교는 [데이터베이스 동기화 개요](http://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)를 참조하십시오.  
  
 **영역별 내용 찾아보기**  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [새로운 기능](what-s-new-replication.md)  
  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [이전 버전과 호환성](replication-backward-compatibility.md)  
  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [복제 기능 및 태스크](replication-features-and-tasks.md)  
  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [기술 참조](technical-reference-replication.md)  
  
  