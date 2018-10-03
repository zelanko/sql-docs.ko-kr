---
title: 디스크 사용량 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- database monitoring [SQL Server], disk usage
- disks [SQL Server]
- monitoring performance [SQL Server], disk usage
- server performance [SQL Server], disk usage
- monitoring [SQL Server], disk activity
- excess paging [SQL Server]
- tuning databases [SQL Server], disk usage
- I/O [SQL Server], monitoring
- disks [SQL Server], monitoring activity
- isolating disk activity [SQL Server]
- database performance [SQL Server], disk usage
- monitoring server performance [SQL Server], disk usage
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 06028d8a68a05cf5588b898232c0170f25d3d3b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647271"
---
# <a name="monitor-disk-usage"></a>디스크 사용량 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 Microsoft Windows 운영 체제 I/O(입/출력) 호출을 사용하여 디스크에서 읽기 및 쓰기 작업을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 디스크 I/O가 수행되는 시간과 방법을 관리하지만 기본 I/O 작업은 Windows 운영 체제에서 수행합니다. I/O 하위 시스템에는 시스템 버스, 디스크 컨트롤러 카드, 디스크, 테이프 드라이브, CD-ROM 드라이브 및 기타 여러 I/O 장치가 있습니다. 디스크 I/O는 시스템에서 자주 병목 현상을 일으킵니다.  
  
 디스크 작업 모니터링은 다음 두 가지 핵심 영역으로 구성됩니다.  
  
-   디스크 I/O 모니터링 및 초과 페이징 검색  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 만드는 디스크 작업 격리  
  
 자세한 내용은 [디스크 사용 모니터링](http://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx)을 참조하십시오.  
  
  
