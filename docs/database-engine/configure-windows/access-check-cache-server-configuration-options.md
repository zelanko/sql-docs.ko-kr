---
title: access check cache 서버 구성 옵션 | Microsoft Docs
description: 액세스 검사 결과 캐시와 캐시 동작을 제어하는 옵션에 대해 알아봅니다. SQL Server에서 이러한 옵션을 변경하는 경우를 알아봅니다.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f5790d5eb416f789bbe67f10d28f18a375b4c572
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158931"
---
# <a name="access-check-cache-server-configuration-options"></a>access check cache 서버 구성 옵션
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 액세스할 때 액세스 검사는 **access check result cache**라는 내부 구조에 캐시됩니다. 
  
**액세스 검사 캐시 버킷 수** 옵션은 액세스 검사 결과 캐시에 사용되는 해시 버킷의 수를 제어합니다. 

**액세스 검사 캐시 할당량** 옵션은 액세스 검사 결과 캐시에 저장된 항목 수를 제어합니다. 최대 항목 수에 도달하면 가장 오래된 항목이 액세스 검사 결과 캐시에서 제거됩니다.
  
기본값 0은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 이러한 옵션을 관리함을 나타냅니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작하여 기본값은 다음 내부 구성으로 변환됩니다.
-   액세스 검사 캐시 버킷 수의 경우 값 0은 기본값인 256개 버킷을 설정합니다.
-   액세스 검사 캐시 할당량의 경우 값 0은 기본값인 1,024개 항목을 설정합니다.

드문 경우지만 이러한 옵션을 변경하여 성능을 향상시킬 수 있습니다. 예를 들어 너무 많은 메모리가 사용되는 경우 액세스 검사 결과 캐시의 크기를 줄일 수 있습니다. 또는 사용 권한이 다시 계산될 때 높은 CPU 사용량이 발생하는 경우 액세스 검사 결과 캐시의 크기를 늘릴 수 있습니다.
 
> [!IMPORTANT]
> 이러한 옵션은 Microsoft 고객 지원 서비스에서 안내하는 경우에만 변경하는 것이 좋습니다. “액세스 검사 캐시 버킷 수” 및 “액세스 검사 캐시 할당량” 값을 변경해야 하는 경우에는 1:4 비율을 사용합니다. 예를 들어 “액세스 검사 캐시 버킷 수” 값을 512로 변경하는 경우 “액세스 검사 캐시 할당량” 값은 2,048로 변경해야 합니다. 
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
