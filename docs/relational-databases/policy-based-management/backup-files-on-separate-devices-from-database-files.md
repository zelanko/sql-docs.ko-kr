---
title: 백업 파일을 데이터베이스 파일과 별개의 디바이스에 두어야 함
description: 정책을 사용하도록 설정하여 SQL Server에서 정책 기반 관리에 따라 데이터베이스 파일 위치와 비교할 때 백업 파일 위치를 확인하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 5b98f8163a3564ccc4aadac6c71c30eb5cf37697
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89285244"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>백업 파일을 데이터베이스 파일과 별개의 디바이스에 두어야 함
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 규칙은 데이터베이스 파일이 백업 파일과 별개의 디바이스에 있는지 검사합니다. 데이터베이스 파일과 백업 파일이 동일한 디바이스에 있는 경우 해당 디바이스에 오류가 발생하면 데이터베이스와 백업을 모두 사용할 수 없게 됩니다. 또한 데이터베이스 파일과 백업 파일을 별개의 디바이스에 두면 데이터베이스의 프로덕션 사용과 백업 작성에 대한 I/O 성능이 모두 최적화됩니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 데이터베이스 데이터 및 로그 디스크가 아닌 다른 디스크를 백업 디스크로 사용하는 것이 좋습니다. 이렇게 하면 데이터 또는 로그 디스크가 실패할 경우 백업에 액세스할 수 있습니다.

데이터베이스 파일과 백업 파일이 동일한 디바이스에 있는 경우 해당 디바이스에 오류가 발생하면 데이터베이스와 백업을 모두 사용할 수 없게 됩니다. 또한 데이터베이스 파일과 백업 파일을 별개의 디바이스에 두면 데이터베이스의 프로덕션 사용과 백업 작성에 대한 I/O 성능이 모두 최적화됩니다.
  
## <a name="see-also"></a>참고 항목 
   
  
 [백업 디바이스](../backup-restore/backup-devices-sql-server.md)  
  
