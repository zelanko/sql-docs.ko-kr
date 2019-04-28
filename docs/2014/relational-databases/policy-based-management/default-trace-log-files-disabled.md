---
title: 기본 추적 로그 파일 해제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2ab57498c9b188818663cfe326287ee3f45a409f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62705359"
---
# <a name="default-trace-log-files-disabled"></a>기본 추적 로그 파일 해제
  이 규칙은 sp_configure 저장 프로시저 기본 추적이 설정된 옵션의 값을 검사하여 기본 추적이 ON(1) 또는 OFF(0)로 설정되었는지 확인합니다. 이 옵션이 설정된 경우 기본 추적은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 대한 DDL 변경 사항 및 구성 정보를 제공합니다. 이러한 정보는 고객 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 고객 지원 서비스에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]관련 문제를 해결하는 데 도움이 되는 경우가 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 sp_configure 저장 프로시저를 사용하여 기본 추적 값을 1로 설정하여 추적을 설정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
