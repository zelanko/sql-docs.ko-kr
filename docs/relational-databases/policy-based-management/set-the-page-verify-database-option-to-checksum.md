---
title: PAGE_VERIFY 데이터베이스 옵션을 CHECKSUM으로 설정 | Microsoft 문서
description: PAGE_VERIFY 옵션이 CHECKSUM인지를 확인합니다. 이 옵션은 데이터-파일 무결성을 위한 SQL Server 데이터베이스 엔진의 체크섬 계산 여부를 제어합니다.
ms.custom: ''
ms.date: 08/19/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4dda2b9138882490b1556b9dbb39f71e35767f5f
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646513"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>PAGE_VERIFY 데이터베이스 옵션을 CHECKSUM으로 설정
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 규칙은 PAGE_VERIFY 데이터베이스 옵션이 CHECKSUM으로 설정되었는지 검사합니다. PAGE_VERIFY 데이터베이스 옵션에 CHECKSUM을 설정하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 페이지를 디스크에 쓸 때 전체 페이지 내용에 대한 체크섬이 계산되어 페이지 헤더에 값이 저장됩니다. 디스크에서 페이지를 읽으면 체크섬이 다시 계산되어 페이지 헤더에 저장된 체크섬 값과 비교됩니다. 이를 통해 높은 수준의 데이터 파일 무결성을 제공할 수 있습니다.  데이터베이스에 대한 PAGE VERIFY CHECKSUM 옵션을 사용하는 경우 SQL Server는 페이지가 디스크에 쓰인 후에 변경된 것을 감지하면 디스크에서 페이지를 다시 읽은 후 [824 메시지](../errors-events/mssqlserver-824-database-engine-error.md)를 보고합니다. 
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 PAGE_VERIFY 데이터베이스 옵션을 CHECKSUM으로 설정합니다. PAGE_VERIFY CHECKSUM 데이터베이스 옵션을 사용하면 시스템 I/O 경로에 의해 발생하는 데이터베이스 일관성 문제를 가장 효과적으로 감지할 수 있습니다.
  
## <a name="for-more-information"></a>참조 항목  
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
