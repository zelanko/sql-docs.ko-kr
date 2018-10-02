---
title: 개체 종속성 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.objectdependencies.f1
ms.assetid: c63d1160-3f3d-45df-99be-6fe081125fb5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1bdda5d95544df6b7cd7cc4108c3bd21dc8f50d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779161"
---
# <a name="object-dependencies"></a>개체 종속성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
일부 데이터베이스 개체는 다른 데이터베이스 개체에 대해 종속적입니다. 예를 들어 뷰와 저장 프로시저는 뷰나 프로시저에서 반환한 데이터가 들어 있는 테이블의 존재 여부에 종속됩니다. 현재 개체의 **개체 종속성(일반 페이지)** 에는 해당 개체가 정상적으로 작동하는 데 반드시 필요한 다른 데이터베이스 개체와 선택한 개체에 종속된 개체가 모두 표시됩니다. 정의에서 다른 개체를 참조하고 시스템 카탈로그에 해당 정의가 저장되어 있으면 이 엔터티를 *참조 엔터티*라고 합니다. 다른 개체에 의해 참조되는 개체는 *참조된 엔터티*라고 합니다.  
  
현재 개체의 **개체 종속성(고급 페이지)** 에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체와 해당 개체에 종속된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체가 표시됩니다. 개체들은 서로 다른 서버에 저장되어 있을 수도 있습니다.  
  
선택한 개체를 변경하거나 삭제하기 전에 개체의 종속성을 파악하려면 이 대화 상자를 사용하십시오.  
  
## <a name="uielement-list"></a>UIElement 목록  
*<selected object>***에 종속된 개체**  
이 단추를 클릭하면 종속성이 추적되고 선택한 개체에 종속된 개체의 목록이 표시됩니다.  
  
*<selected object>***가** **종속된 개체**  
이 단추를 클릭하면 종속성이 추적되고 선택한 개체가 종속된 개체의 목록이 표시됩니다.  
  
**종속성**  
*<selected object>***에 종속된 개체**를 클릭하면 선택한 개체에 종속된 개체의 계층 뷰가 표시됩니다. *<selected object>***가 **종속된 개체**** 를 클릭하면 선택한 개체가 종속된 개체의 계층 뷰가 표시됩니다.  
  
**이름**  
위의 **종속성** 트리 뷰에서 선택한 개체의 이름을 표시합니다.  
  
**형식**  
위의 **종속성** 트리 뷰에서 선택한 개체의 유형을 표시합니다.  
  
**마지막 동기화 시간**  
> [!NOTE]  
> 이 옵션은 **고급** 페이지에서만 사용할 수 있습니다.  
  
종속성 정보가 마지막으로 업데이트된 날짜 및 시간을 지정합니다.  
  
**종속성 유형**  
> [!NOTE]  
> 이 옵션은 **일반** 페이지에서만 사용할 수 있습니다.  
  
두 개체 간의 종속성 유형을 표시합니다. 다음 중 하나일 수 있습니다.  
  
-   스키마 바운드 종속성  
  
    참조 개체가 존재하는 한 참조된 개체가 삭제되거나 수정되지 않도록 방지하는 두 개체 간의 관계입니다. 스키마 바운드 종속성은 WITH SCHEMABINDING 절을 사용하여 뷰 또는 사용자 정의 함수를 만들거나 테이블이 CHECK 또는 DEFAULT 제약 조건이나 계산 열의 정의를 통해 다른 개체를 참조하면 생성됩니다.  
  
-   비스키마 바운드 종속성  
  
    참조된 개체가 삭제되거나 수정되지 않도록 방지하지 않는 두 개체 간의 관계입니다.  
  
-   사용할 수 없거나 확인되지 않은 엔터티  
  
    종속성 유형을 확인할 수 없음을 나타냅니다. 이는 선택한 개체가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]인스턴스에 있는 경우에만 발생합니다.  
  
