---
title: 읽기 다시 시도 문제에 대 한 디스크 입된/출력 하위 시스템 검사 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9726b29ebdd47e447c14e402aa2c5fa345284216
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190653"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>읽기 다시 시도 문제에 대한 디스크 입력-출력 하위 시스템 검사
  이 규칙은 이벤트 로그에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지 825를 검사합니다. 이 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 디스크에서 데이터를 읽으려는 첫 번째 시도가 실패했음을 나타냅니다. 이 메시지는 디스크 I/O 하위 시스템에 중요한 문제가 있음을 나타냅니다. 이 메시지는 현재까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문제를 나타내는 것은 아닙니다. 하지만 문제가 해결되지 않을 경우 디스크 문제로 인해 데이터 손실 또는 데이터베이스 손상이 발생할 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 다음은 기본 하드웨어 문제를 확인하고 해결하는 데 도움이 되는 동작입니다.  
  
-   이 메시지의 오류 로그 및 변수 텍스트를 검토하여 문제를 파악합니다.  
  
-   디스크 시스템을 확인합니다. 디스크, 디스크 컨트롤러, 배열 카드 또는 디스크 드라이버에 관련된 문제일 수 있습니다.  
  
-   최신 유틸리티의 디스크 제조업체에 문의하여 디스크 시스템 상태를 확인합니다.  
  
-   최신 드라이버 업데이트에 대해 디스크 제조업체에 문의합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [MSSQLSERVER_825](../errors-events/mssqlserver-825-database-engine-error.md)  
  
 [SQL Server I/O 기본 사항, 2장(SQL Server I/O Basics, Chapter 2)](http://go.microsoft.com/fwlink/?linkid=69370)  
  
  
