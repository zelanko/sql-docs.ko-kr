---
title: 디스크 입/출력 하위 시스템에서 읽기 다시 시도 문제 확인 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: aa5de132741edb085dd944be34e93997456ddecc
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657207"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>읽기 다시 시도 문제에 대한 디스크 입력-출력 하위 시스템 검사
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 이벤트 로그에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지 825를 검사합니다. 이 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 디스크에서 데이터를 읽으려는 첫 번째 시도가 실패했음을 나타냅니다. 이 메시지는 디스크 I/O 하위 시스템에 중요한 문제가 있음을 나타냅니다. 이 메시지는 현재까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문제를 나타내는 것은 아닙니다. 하지만 문제가 해결되지 않을 경우 디스크 문제로 인해 데이터 손실 또는 데이터베이스 손상이 발생할 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 다음은 기본 하드웨어 문제를 확인하고 해결하는 데 도움이 되는 동작입니다.  
  
-   이 메시지의 오류 로그 및 변수 텍스트를 검토하여 문제를 파악합니다.  
  
-   디스크 시스템을 확인합니다. 디스크, 디스크 컨트롤러, 배열 카드 또는 디스크 드라이버에 관련된 문제일 수 있습니다.  
  
-   최신 유틸리티의 디스크 제조업체에 문의하여 디스크 시스템 상태를 확인합니다.  
  
-   최신 드라이버 업데이트에 대해 디스크 제조업체에 문의합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [MSSQLSERVER_825](../errors-events/mssqlserver-825-database-engine-error.md)  
  
 [SQL Server I/O 기본 사항, 2장(SQL Server I/O Basics, Chapter 2)](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))  
  
  
