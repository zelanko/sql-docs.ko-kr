---
title: 인터넷을 통한 복제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web publishing [SQL Server replication], about Web publishing
- Web publishing [SQL Server replication]
- Internet [SQL Server replication]
- Internet [SQL Server replication], publishing
ms.assetid: 04e7f4ed-e244-4bbe-ba12-09c33abea09e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c5a1244ed340dcfd4794c14635d570530b88f5d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716724"
---
# <a name="replication-over-the-internet"></a>인터넷을 통한 복제
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  인터넷으로 데이터를 복제하면 연결이 끊긴 원격 사용자가 필요할 때 인터넷 연결을 사용해서 데이터에 액세스할 수 있습니다. 다음을 사용하여 인터넷을 통해 데이터를 복제합니다.  
  
-   VPN(가상 프라이빗 네트워크). 자세한 내용은 [VPN을 사용하여 인터넷을 통해 데이터 게시](../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md)를 참조하세요.  
  
-   병합 복제를 위한 웹 동기화 옵션. 자세한 내용은 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 참조하세요.  
  
 모든 유형의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 시 VPN을 통해 데이터를 복제할 수 있지만 병합 복제를 사용할 경우 웹 동기화를 고려해야 합니다.  
  
  
