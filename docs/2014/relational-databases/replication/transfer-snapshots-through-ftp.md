---
title: FTP를 통해 스냅숏 전송 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 55c30791-cd2a-420b-8ba7-5700e005cb45
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ab22490bfb46f784333a4bb19cd5d966fbec753
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313480"
---
# <a name="transfer-snapshots-through-ftp"></a>FTP를 통해 스냅숏 전송
  기본적으로 스냅숏은 UNC(Universal Naming Convention) 공유로 정의된 폴더에 저장됩니다. 복제 시 UNC 공유 대신 FTP(파일 전송 프로토콜) 공유를 지정할 수도 있습니다. FTP를 사용하려면 FTP 서버를 구성한 다음 FTP를 사용할 하나의 게시와 하나 이상의 구독을 구성합니다. FTP 서버 구성 방법은 인터넷 정보 서비스(IIS) 설명서를 참조하십시오. 게시에 FTP 정보를 지정하면 해당 게시에 대한 구독은 기본적으로 FTP를 사용합니다. FTP는 IIS를 실행하는 컴퓨터가 방화벽에 의해 배포자와 분리되어 있는 경우에만 웹 동기화에 사용됩니다. 이 경우 FTP는 IIS를 실행 중인 컴퓨터와 배포자의 스냅숏을 전송하는 데 사용할 수 있습니다. 스냅숏을 구독자에게 전송할 때는 항상 HTTPS를 사용합니다.  
  
> [!IMPORTANT]  
>  FTP 암호는 저장된 후 구독자, 또는 웹 동기화를 사용하는 경우 IIS를 실행하는 컴퓨터에서 일반 텍스트 형태로 FTP 서버에 전달되므로 FTP 공유 대신 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증 및 UNC 공유를 사용하는 것이 좋습니다. 또한 단일 계정에서 스냅숏 공유에 대한 액세스를 제어하므로 필터링된 병합 게시의 구독자만 자신의 데이터 파티션에서 스냅숏으로 액세스하게 할 수는 없습니다.  
  
 FTP를 통해 스냅숏을 배달하려면 [Deliver a Snapshot Through FTP](publish/deliver-a-snapshot-through-ftp.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [병합 복제에 대한 웹 동기화](web-synchronization-for-merge-replication.md)   
 [스냅숏으로 구독 초기화](initialize-a-subscription-with-a-snapshot.md)   
 [스냅숏 옵션](snapshot-options.md)  
  
  
