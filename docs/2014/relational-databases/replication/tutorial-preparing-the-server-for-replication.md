---
title: '자습서: 복제용 서버 준비 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9b8ed6778a087c2200012c6df1409b187b39329
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63199079"
---
# <a name="tutorial-preparing-the-server-for-replication"></a>자습서: 복제용 서버 준비
  복제 토폴로지를 구성하려면 보안을 계획해야 합니다. 이 자습서에서는 데이터 복제의 첫 단계인 배포를 구성하는 방법과 복제 토폴로지의 보안을 강화하는 방법을 보여 줍니다. 다른 자습서를 사용하기 전에 먼저 이 자습서를 완료해야 합니다.  
  
> [!NOTE]  
>  서버 간에 데이터를 안전 하 게 복제 하려면 [복제 보안 모범 사례](security/replication-security-best-practices.md)의 모든 권장 사항을 구현 해야 합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 최소의 권한을 사용하여 안전하게 복제를 실행할 수 있도록 서버를 준비하는 방법을 배웁니다. 첫 번째 단원에서는 복제 에이전트를 실행하는 데 사용되는 Windows 서비스 계정을 만드는 방법을 보여 줍니다. 두 번째 단원에서는 게시 스냅샷을 생성하고 저장하는 데 사용되는 폴더를 구성하는 방법을 보여 줍니다. 세 번째 단원에서는 배포를 구성하고 사용 권한을 설정하는 방법을 보여 줍니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서는 기본적인 데이터베이스 작업에는 익숙하지만 복제에 대한 경험은 풍부하지 않은 사용자를 위한 것입니다.  
  
 이 자습서를 사용하려면 시스템에 다음 구성 요소가 설치되어 있어야 합니다.  
  
-   
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 데이터베이스가 있는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다.  
  
 **이 자습서를 완료 하는 데 소요 되는 예상 시간: 30 분**  
  
## <a name="lessons-in-this-tutorial"></a>이 자습서의 단원  
  
-   [1 단원: 복제용 Windows 계정 만들기](lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [2 단원: 스냅숏 폴더 준비](lesson-2-preparing-the-snapshot-folder.md)  
  
-   [3 단원: 배포 구성](lesson-3-configuring-distribution.md)  
  
 [자습서 시작](lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](configure-distribution.md)   
 [SQL Server 복제 보안](security/view-and-modify-replication-security-settings.md)  
  
  
