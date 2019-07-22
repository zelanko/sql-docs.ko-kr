---
title: 기본 추적 로그 파일 해제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1407f55e2edab15768fb10288b78dd59ff93ddd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940492"
---
# <a name="default-trace-log-files-disabled"></a>기본 추적 로그 파일 해제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 sp_configure 저장 프로시저 기본 추적이 설정된 옵션의 값을 검사하여 기본 추적이 ON(1) 또는 OFF(0)로 설정되었는지 확인합니다. 이 옵션이 설정된 경우 기본 추적은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 대한 DDL 변경 사항 및 구성 정보를 제공합니다. 이러한 정보는 고객 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 고객 지원 서비스에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]관련 문제를 해결하는 데 도움이 되는 경우가 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 sp_configure 저장 프로시저를 사용하여 기본 추적 값을 1로 설정하여 추적을 설정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
