---
title: UCP를 한 SQL Server 인스턴스에서 다른 인스턴스로 이동(SQL Server 유틸리티) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b402fd9e-0bea-4c38-a371-6ed7fea12e96
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bffc65e8586e8a158c58f7afb5cfb244835e8c86
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115388"
---
# <a name="move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility"></a>UCP를 한 SQL Server 인스턴스에서 다른 인스턴스로 이동(SQL Server 유틸리티)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 UCP(유틸리티 제어 지점)를 한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]인스턴스에서 다른 인스턴스로 이동하는 방법에 대해 설명합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="move-a-ucp-from-one-instance-of-sql-server-to-another"></a>UCP를 한 SQL Server 인스턴스에서 다른 인스턴스로 이동하려면  
  
1.  UCP의 새 호스트 인스턴스가 될 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 새 UCP를 만듭니다. 자세한 내용은 [SQL Server 유틸리티 제어 지점 만들기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)를 참조하세요.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 중 기본이 아닌 정책 설정이 지정된 항목이 있으면 새 UCP에서 그대로 설정할 수 있도록 정책 임계값을 기록하십시오. 새 UCP에 인스턴스가 추가될 때는 기본 정책이 적용됩니다. 기본 정책이 사용될 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 목록 뷰의 **정책 유형** 열에 **전역** 이 표시됩니다.  
  
3.  이전 UCP에서 모든 관리되는 인스턴스를 제거합니다. 자세한 내용은 [SQL Server 유틸리티에서 SQL Server 인스턴스 제거](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)를 참조하세요.  
  
4.  이전 UCP에서 UMDW(유틸리티 관리 데이터 웨어하우스)를 백업합니다. 파일 이름은 Sysutility_mdw_\<GUID>_DATA이며 데이터베이스 기본 위치는 \<시스템 드라이브>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\입니다. 여기서 \<시스템 드라이브>는 일반적으로 C:\ 드라이브입니다. 자세한 내용은 [백업 및 복원으로 데이터베이스 복사](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)를 참조하세요.  
  
5.  UMDW 백업을 새 UCP로 복원합니다. 자세한 내용은 [백업 및 복원으로 데이터베이스 복사](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)를 참조하세요.  
  
6.  인스턴스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 관리할 수 있도록 새 UCP에 등록합니다. 자세한 내용은 [SQL Server 인스턴스 등록&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)를 참조하세요.  
  
7.  필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대한 사용자 지정 정책 정의를 구현합니다.  
  
8.  데이터 수집 및 집계 작업이 완료될 때까지 약 1시간 동안 기다립니다.  
  
9. 데이터를 새로 고치려면 **유틸리티 탐색기**에서 **관리되는 인스턴스** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다. 목록 뷰 데이터가 **유틸리티 탐색기** 내용 창에 표시됩니다. 자세한 내용은 [리소스 상태 정책 결과 보기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 인스턴스 등록&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
  
