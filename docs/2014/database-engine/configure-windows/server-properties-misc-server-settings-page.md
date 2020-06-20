---
title: 서버 속성(기타 서버 설정 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.miscserversettings.f1
ms.assetid: b170c066-30cd-42dd-8d34-aa129ea09551
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: aef24f7e2a02140e776cf113089ec083d06a86aa
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934909"
---
# <a name="server-properties-misc-server-settings-page"></a>서버 속성(기타 서버 설정 페이지)
  이 페이지를 사용하여 서버 설정을 확인하거나 수정할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **사용자의 기본 언어**  
 새로 생성된 모든 로그인에 대한 기본 언어를 지정합니다.  
  
 **다른 트리거를 발생시키는 트리거 허용**  
 트리거로 다른 트리거를 시작할 수 있는지 동작을 결정합니다. 이 옵션의 선택을 취소하면 트리거로 다른 트리거를 시작할 수 없습니다. 이 옵션을 선택하면 최대 32 수준까지 트리거에 의한 트리거 시작이 가능합니다.  
  
 **쿼리 관리자를 사용하여 장기 실행 쿼리 방지**  
 쿼리가 실행될 수 있는 최대 제한 시간을 지정합니다. 쿼리 비용이란 특정 하드웨어 구성에서 쿼리를 실행하는 데 필요한 예상 소요 시간(초)입니다. 기본적으로 쿼리 관리자는 해제되어 있어 모든 쿼리의 실행이 허용됩니다. 이 옵션을 선택하면 아래의 입력란에 제한 시간을 입력해야 합니다. 0이나 음수가 아닌 값을 지정하면 쿼리 관리자가 그 값을 초과하는 예상 비용을 갖는 쿼리의 실행을 허용하지 않습니다.  
  
 **두 자리 연도를 다음 연도로 해석**  
 두 자리 연도 값 해석에 사용할 100년 간의 날짜 범위를 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 지정된 범위 내에서 마지막 두 자리가 일치하는 연도를 참조하여 두 자리 날짜 값을 해석합니다.  
  
 오른쪽 상자에서 끝 연도를 설정합니다. 끝 연도를 저장하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 자동으로 왼쪽 상자에 시작 연도를 채웁니다.  
  
 **구성 값**  
 이 창의 옵션에 대해 구성된 값을 표시합니다. 이러한 값을 변경한 후에는 **실행 값** 을 클릭하여 변경 사항이 적용되었는지 여부를 확인합니다. 변경 사항이 적용되지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스를 다시 시작해야 합니다.  
  
 **실행 값**  
 이 창의 옵션에 대한 현재 실행 값을 볼 수 있습니다. 이 값은 읽기 전용입니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
