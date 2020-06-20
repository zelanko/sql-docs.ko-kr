---
title: 트랜잭션(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9502a9c0c300e1e239c8837b79c99f4c3e7a7eff
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971023"
---
# <a name="transactions-master-data-services"></a>트랜잭션(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 트랜잭션은 멤버에 대해 동작이 수행될 때마다 기록됩니다. 트랜잭션은 모든 사용자가 보고 관리자가 되돌릴 수 있습니다. 트랜잭션은 동작이 수행된 날짜와 시간, 동작을 수행한 사용자를 그 외 다른 세부 정보와 함께 보여 줍니다. 사용자는 트랜잭션에 주석을 추가하여 트랜잭션이 시작된 이유를 나타낼 수 있습니다.  
  
## <a name="when-transaction-are-recorded"></a>트랜잭션이 기록되는 시기  
 트랜잭션은 멤버에 대해 다음 동작이 수행될 때 기록됩니다.  
  
-   생성, 삭제 또는 다시 활성화될 때  
  
-   특성 값이 변경될 때  
  
-   계층 내에서 이동될 때  
  
 비즈니스 규칙에 의해 속성 값이 변경될 때는 트랜잭션이 기록되지 않습니다.  
  
## <a name="view-and-manage-transactions"></a>트랜잭션 보기 및 관리  
 **탐색기** 기능 영역에서 직접 만든 트랜잭션을 보고 주석(설명)을 추가할 수 있습니다.  
  
 관리자는 **버전 관리** 기능 영역에서 액세스 권한을 가지고 있는 모델의 모든 사용자에 대한 모든 트랜잭션을 보고 되돌릴 수 있습니다.  
  
> [!NOTE]  
>  관리자는 **버전 관리** 기능 영역에 읽기 전용 권한 수준이 적용되지 않는 한, 모든 사용자의 모든 트랜잭션을 볼 수 있습니다. 예를 들어 관리자에 대해 읽기 전용 권한 및 업데이트 권한 수준이 설정된 경우 읽기 전용 권한이 업데이트 권한보다 우선하므로 관리자는 다른 사용자 트랜잭션을 볼 수 없습니다.

## <a name="system-settings"></a>시스템 설정  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에는 레코드가 준비될 때 트랜잭션을 기록할지 여부를 결정하는 설정이 있습니다. 이 설정은 SQL Server 2008 R2에만 영향을 줍니다. 이 설정은 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에서 조정하거나 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 시스템 설정 테이블에서 직접 조정할 수 있습니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](system-settings-master-data-services.md)을 참조하세요.  
  
 이 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 데이터를 가져올 경우 저장 프로시저를 시작할 때 트랜잭션을 기록할지 여부를 지정할 수 있습니다. 자세한 내용은 [준비 저장 프로시저&#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)를 참조하세요.  
  
## <a name="concurrency"></a>동시성  
 특정 엔터티 값이 두 개 이상의 탐색기 세션에 동시에 표시될 경우 동일한 값에 대한 동시 편집이 가능합니다. 동시 편집은 MDS에서 자동으로 검색되지 않습니다. 이러한 동작은 여러 사용자가 여러 세션으로부터(예: 여러 컴퓨터, 여러 브라우저 탭 또는 창, 여러 사용자 계정으로부터) 웹 브라우저에서 MDS 탐색기를 사용할 때 발생할 수 있습니다.  
  
 설정된 트랜잭션에도 불구하고 두 명 이상의 사용자가 오류 없이 동일한 엔터티 값을 업데이트할 수 있습니다. 일반적으로 시간 시퀀스에서 마지막으로 편집된 값이 우선 적용됩니다. 중복된 편집 충돌은 트랜잭션 기록에서 수동으로 관측할 수 있으며 관리자가 수동으로 되돌릴 수 있습니다. 트랜잭션 기록에는 각 세션에서 문제의 특성에 대해 **이전 값** 및 **새 값** 의 개별 트랜잭션이 표시되지만 동일한 이전 값에 대해 여러 **새 값** 이 존재하는 경우 충돌을 자동으로 해결하지 않습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|트랜잭션을 되돌려 동작을 실행 취소합니다(관리자에만 해당).|[트랜잭션 되돌리기&#40;Master Data Services&#41;](../../2014/master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [관리자&#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
-   [주석&#40;Master Data Services&#41;](../../2014/master-data-services/annotations-master-data-services.md)  
  
  
