---
title: access check cache 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: feed895eeb7b11b4c41c51c4c26859a1057d2733
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158761"
---
# <a name="access-check-cache-server-configuration-options"></a>access check cache 서버 구성 옵션
데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 액세스할 때 액세스 검사는 **access check result cache**라는 내부 구조에 캐시됩니다. 
  
**액세스 검사 캐시 버킷 수** 옵션은 access check result cache에 사용 되는 해시 버킷의 수를 제어 합니다. 

**Access check cache quota** 옵션은 access check result cache에 저장 된 항목 수를 제어 합니다. 최대 항목 수에 도달 하면 가장 오래 된 항목이 access check result cache에서 제거 됩니다.
  
기본값 0은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 이러한 옵션을 관리함을 나타냅니다. 부터 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 의 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 기본값은 다음 내부 구성으로 변환 됩니다.
-   액세스 검사 캐시 버킷 수의 경우 값 0은 x86 아키텍처의 경우 256 버킷을, x64 및 IA-64 아키텍처의 경우 2048 버킷을 설정 합니다.
-   액세스 검사 캐시 할당량의 경우 값 0은 x86 아키텍처의 경우 1024 항목, x64 및 IA-64 아키텍처의 경우 28192048 버킷에 대 한 기본값을 설정 합니다.

드문 경우지만 이러한 옵션을 변경하여 성능을 향상시킬 수 있습니다. 예를 들어 너무 많은 메모리가 사용 되는 경우 액세스 검사 결과 캐시의 크기를 줄일 수 있습니다. 또는 사용 권한을 다시 계산할 때 높은 CPU 사용량이 발생 하는 경우 액세스 검사 결과 캐시의 크기를 늘릴 수 있습니다.

> [!IMPORTANT]
> 이러한 옵션은 Microsoft 고객 지원 서비스에서 안내하는 경우에만 변경하는 것이 좋습니다.
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
