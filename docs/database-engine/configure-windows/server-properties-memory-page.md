---
title: 서버 속성(메모리 페이지) | Microsoft Docs
description: SQL Server의 서버 메모리 옵션을 파악합니다. 최소 및 최대 서버 메모리, 인덱스 생성 메모리 및 기타 설정에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.memory.f1
ms.assetid: 46a77d4e-ab92-49d3-a14b-423462e50715
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 83f8be52af8507203764cab7197359c1c99663a0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726623"
---
# <a name="server-properties---memory-page"></a>서버 속성 - 메모리 페이지
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 페이지를 사용하여 서버 메모리 옵션을 확인하거나 수정할 수 있습니다. **최소 서버 메모리** 를 0으로 설정하고 **최대 서버 메모리** 를 2147483647MB로 설정하면 운영 체제 및 기타 애플리케이션에서 현재 사용하고 있는 메모리에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 메모리가 항상 최적화됩니다. 컴퓨터와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 로드가 변경됨에 따라 할당되는 메모리도 달라집니다. 아래에 지정된 최소값과 최대값을 설정하여 이 동적 메모리 할당을 추가로 제한할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **최소 서버 메모리(MB)**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 할당된 최소 메모리 양으로 시작되고 이 값 아래로 메모리를 해제하지 않도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 크기와 작업에 기반하여 이 값을 설정합니다. 항상 이 옵션을 적당한 값으로 설정하여 운영 체제가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 너무 많은 메모리를 요구하여 Windows 성능을 저하시키지 않도록 해야 합니다.  
  
 **최대 서버 메모리(MB)**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작될 때와 실행되는 동안 할당할 수 있는 최대 메모리 크기를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 동시에 실행되는 애플리케이션이 여러 개 있는 것을 아는 경우, 이러한 애플리케이션이 충분한 메모리를 사용하여 실행되도록 하려면 이 구성 옵션을 특정 값으로 설정할 수 있습니다. 웹 또는 전자 메일 서버 등의 다른 애플리케이션이 필요할 때만 메모리를 요청하는 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 필요할 때마다 메모리를 해제하므로 이 옵션을 설정하지 않는 편이 좋습니다. 그러나 애플리케이션에서는 시작할 때 사용할 수 있는 모든 메모리를 사용하고, 필요할 때 더 요청하지 않는 경우가 많습니다. 이런 방식으로 동작하는 애플리케이션이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 동시에 같은 컴퓨터에서 실행되는 경우에는 애플리케이션에 필요한 메모리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 할당하지 않도록 이 옵션의 값을 설정합니다. **최대 서버 메모리** 에 지정할 수 있는 최소 메모리 양은 128MB입니다. 이전 32비트 시스템의 경우 64MB입니다.  
  
 **인덱스 생성 메모리(KB, 0 = 동적 메모리)**  
 인덱스 생성 정렬에 사용되는 메모리의 크기(KB)를 지정합니다. 기본값 0을 그대로 사용하면 동적 할당 기능이 설정되고 대부분의 경우 추가 조정 없이 제대로 작동하지만 사용자가 704 ~ 2147483647 사이의 다른 값을 입력할 수도 있습니다.  
  
> [!NOTE]  
>  1 ~ 703 사이의 값은 허용되지 않습니다. 이 범위의 값을 입력하면 필드에 입력된 값이 704로 대체됩니다.  
  
 **쿼리당 최소 메모리(KB)**  
 쿼리 실행에 할당되는 메모리의 크기(KB)를 지정합니다. 512 ~ 2147483647KB 사이의 값을 설정할 수 있습니다. 기본값은 1024KB입니다.  
  
 **구성 값**  
 이 창의 옵션에 대해 구성된 값을 표시합니다. 이러한 값을 변경한 후에는 **실행 값** 을 클릭하여 변경 사항이 적용되었는지 여부를 확인합니다. 변경 사항이 적용되지 않은 경우 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작해야 합니다.  
  
 **실행 값**  
 이 창의 옵션에 대한 현재 실행 값을 표시합니다. 이 값은 읽기 전용입니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
