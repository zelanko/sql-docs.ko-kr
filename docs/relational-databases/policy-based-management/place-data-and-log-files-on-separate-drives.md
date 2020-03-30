---
title: 데이터와 로그 파일을 별개의 드라이브에 배치 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54f469f8ab9f0daaf6f37c8f6bad1878bc716dbd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68086936"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>데이터와 로그 파일을 별개의 드라이브에 배치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 데이터와 로그 파일이 별개의 논리적 드라이브에 배치되어 있는지 검사합니다. 데이터와 로그 파일을 동일 디바이스에 배치할 경우 디바이스에 경합이 발생하여 성능이 저하될 수 있습니다. 파일을 별개의 장치에 배치하면 데이터와 로그 파일에 대해 I/O 작업이 동시에 수행될 수 있습니다.  
  
## <a name="recommendations"></a>권장 사항  
 새 데이터베이스를 만들 때 데이터와 로그에 대해 별개의 드라이브를 지정합니다. 데이터베이스를 만든 후 파일을 이동하려면 데이터베이스를 오프라인 상태로 설정해야 합니다. 다음 중 한 가지 방법을 사용하여 파일을 이동합니다.  
  
> [!NOTE]  
>  이 정책은 탑재 지점을 통해 개별 물리적 디바이스를 검색할 수 없습니다.  
  
-   RESTORE DATABASE 문을 WITH MOVE 옵션과 함께 사용하여 백업에서 데이터베이스를 복원합니다.  
  
-   데이터와 로그 디바이스에 대해 별개의 위치를 지정하여 데이터베이스를 분리하고 다시 연결합니다.  
  
-   ALTER DATABASE 문을 MODIFY FILE 옵션과 함께 실행한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작하여 새 위치를 지정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)  
  
 [사용자 데이터베이스 이동](../../relational-databases/databases/move-user-databases.md)  
  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
