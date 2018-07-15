---
title: 데이터와 로그 파일을 별개의 드라이브에 배치 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b5c6455ff635ba3000cb7121eb02def995d28fc0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307473"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>데이터와 로그 파일을 별개의 드라이브에 배치
  이 규칙은 데이터와 로그 파일이 별개의 논리적 드라이브에 배치되어 있는지 검사합니다. 데이터와 로그 파일을 동일 장치에 배치할 경우 장치에 경합이 발생하여 성능이 저하될 수 있습니다. 파일을 별개의 장치에 배치하면 데이터와 로그 파일에 대해 I/O 작업이 동시에 수행될 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 새 데이터베이스를 만들 때 데이터와 로그에 대해 별개의 드라이브를 지정합니다. 데이터베이스를 만든 후 파일을 이동하려면 데이터베이스를 오프라인 상태로 설정해야 합니다. 다음 중 한 가지 방법을 사용하여 파일을 이동합니다.  
  
> [!NOTE]  
>  이 정책은 탑재 지점을 통해 개별 물리적 장치를 검색할 수 없습니다.  
  
-   RESTORE DATABASE 문을 WITH MOVE 옵션과 함께 사용하여 백업에서 데이터베이스를 복원합니다.  
  
-   데이터와 로그 장치에 대해 별개의 위치를 지정하여 데이터베이스를 분리하고 다시 연결합니다.  
  
-   ALTER DATABASE 문을 MODIFY FILE 옵션과 함께 실행한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작하여 새 위치를 지정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [데이터베이스 파일 이동](../databases/move-database-files.md)  
  
 [사용자 데이터베이스 이동](../databases/move-user-databases.md)  
  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
