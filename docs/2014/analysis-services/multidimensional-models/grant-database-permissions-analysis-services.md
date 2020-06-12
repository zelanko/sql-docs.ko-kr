---
title: Grant 데이터베이스 사용 권한 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9b4e5ac88a81728d6e29d32b0d330ba8fd408633
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546685"
---
# <a name="grant-database-permissions-analysis-services"></a>데이터베이스 권한 부여(Analysis Services)
  관계형 데이터베이스의 백그라운드에서 Analysis Services 데이터베이스 관리를 수행하려는 경우 알아두어야 할 첫 번째 사항은 데이터 액세스의 측면에서 데이터베이스가 Analysis Services의 기본 보안 개체가 아니라는 점입니다.

 Analysis Services의 기본 쿼리 구조는 해당 특정 개체에 대한 사용자 권한 집합을 포함하는 큐브(또는 테이블 형식 모델)입니다. 데이터베이스 로그인 및 사용자 권한(보통 `db_datareader`)이 데이터베이스 자체에 설정되는 관계형 데이터베이스 엔진과는 대조적으로 Analysis Services 데이터베이스는 일반적으로 데이터 모델에서 기본 쿼리 개체의 컨테이너입니다. 우선적인 목표가 큐브 또는 테이블 형식 모델의 데이터에 액세스하는 것이라면 일단 데이터베이스 사용 권한을 바이패스하고 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) 항목으로 이동해도 됩니다.

 Analysis Services의 데이터베이스 사용 권한은 데이터베이스의 모든 권한과 마찬가지로 관리 기능을 광범위하게 사용하도록 설정하거나 처리 작업을 위임한 경우에 더 세밀하게 설정할 수 있습니다. Analysis Services 데이터베이스의 사용 권한 수준이 다음 그림에 나와 있으며 아래에 설명된 대로 **역할 만들기** 대화 상자의 **일반** 창에서 지정합니다.

 Analysis Services에는 로그인이 없습니다. **멤버 자격** 창에서 역할을 만들고 Windows 계정을 할당하기만 하면 됩니다. 관리자를 비롯하여 모든 사용자는 Windows 계정을 사용하여 Analysis Services에 연결합니다.

 ![데이터베이스 사용 권한을 보여 주는 역할 만들기 대화 상자](../media/ssas-permsdbrole.png "데이터베이스 사용 권한을 보여 주는 역할 만들기 대화 상자")

 데이터베이스 수준에서 지정한 세 가지 유형의 사용 권한이 있습니다.

 **모든 권한(관리자)** - 모든 권한은 모든 기능을 포괄하는 사용 권한으로, 데이터베이스 내 모든 개체를 쿼리하거나 처리하고 역할 보안을 관리하는 기능 등 Analysis Services 데이터베이스에 대한 방대한 기능을 제공합니다. 모든 권한은 데이터베이스 관리자 자격과 같은 의미입니다. `Full Control`을 선택한 경우 `Process Database` 및 `Read Definition` 권한도 선택되며 선택은 취소할 수 없습니다.

> [!NOTE]
>  또한 서버 관리자(서버 관리자 역할의 구성원)는 해당 서버의 모든 데이터베이스에 대해 암시적으로 모든 권한을 갖게 됩니다.

 `Process Database`권한은이 권한은 데이터베이스 수준에서 처리를 위임 하는 데 사용 됩니다. 관리자는 다른 사용자 또는 서비스가 데이터베이스의 모든 개체에 대한 처리 작업을 호출할 수 있는 역할을 만들어 이 작업을 오프로드할 수 있습니다. 또는 특정 개체에 대한 처리를 사용할 수 있는 역할을 만들 수도 있습니다. 자세한 내용은 [처리 권한 부여&#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md) 를 참조하세요.

 `Read Definition`권한은이 권한은 연결 된 데이터를 볼 수 있는 기능을 제외 하 고 개체 메타 데이터를 읽을 수 있는 기능을 부여 합니다. 일반적으로 이 사용 권한은 전용 처리를 위해 만든 역할에 사용되며, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 와 같은 도구를 사용하여 데이터베이스를 대화형으로 처리하는 기능을 추가합니다. `Read Definition` 권한이 없는 `Process Database` 권한은 스크립팅된 시나리오에서만 효과적입니다. SSIS 또는 다른 스케줄러를 통해 처리를 자동화할 계획인 경우 `Process Database` 권한은 없고 `Read Definition` 권한만 있는 역할을 만들 수 있습니다. 그렇지 않으면 동일한 역할에 두 속성을 함께 결합하여 사용자 인터페이스에서 데이터 모델을 시각적으로 표시하는 SQL Server 도구를 통해 무인 및 대화형 처리를 둘 다 지원하는 방법도 고려해 볼 수 있습니다.

## <a name="full-control-administrator-permissions"></a>모든 권한(관리자)
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 데이터베이스 관리자는 모든 권한(관리자)을 갖는 역할에 할당된 임의의 Windows 사용자 ID입니다. 데이터베이스 관리자는 데이터베이스 내에서 다음을 비롯한 모든 작업을 수행할 수 있습니다.

-   개체 처리

-   큐브, 차원, 측정값 그룹, 큐브 뷰 및 데이터 마이닝 모델을 비롯하여 데이터베이스의 모든 개체에 대한 데이터 및 메타데이터 읽기

-   모든 권한을 갖는 역할에 사용자를 추가하는 등 사용자 또는 사용 권한을 추가하여 데이터베이스 역할 생성 또는 수정

-   데이터베이스 역할 또는 역할 멤버 자격 삭제

-   데이터베이스에 어셈블리(또는 저장 프로시저) 등록

 데이터베이스 관리자는 서버에서 데이터베이스를 추가 또는 삭제할 수 없거나, 동일한 서버에서 다른 데이터베이스에 대한 관리자 권한을 부여할 수 없습니다. 이러한 권한은 서버 관리자에게만 있습니다. 이 권한 수준에 대 한 자세한 내용은 [Analysis Services&#41;&#40;서버 관리자 권한 부여](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) 를 참조 하세요.

 모든 역할이 사용자 정의되므로 이러한 용도에 대한 전용 역할(예: 이름이 "dbadmin"인 역할)을 만든 후 Windows 사용자 및 그룹 계정을 적절하게 할당하는 것이 좋습니다.

#### <a name="create-roles-in-ssms"></a>SSMS에서 역할 만들기

1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스에 연결하고 **데이터베이스** 폴더를 열어 데이터베이스를 선택한 후 **역할** | **새 역할**을 마우스 오른쪽 단추로 클릭합니다.

2.  **일반** 창에서 DBAdmin 등의 이름을 입력합니다.

3.  큐브에 대해 **모든 권한(관리자)** 확인란을 선택합니다. `Process Database` 및 `Read Definition` 권한은 자동으로 선택됩니다. 이러한 권한은 모두 `Full Control`을 갖는 역할에 항상 포함됩니다.

4.  **멤버 자격** 창에서 이 역할을 사용하여 Analysis Services에 연결하는 Windows 사용자 및 그룹 계정을 입력합니다.

5.  **확인** 을 클릭하여 역할 만들기를 마칩니다.

## <a name="process-database"></a>Process Database
 데이터베이스 사용 권한을 부여 하는 역할을 정의 하는 경우를 건너뛰고 `Full Control` 간단히 선택할 수 있습니다 `Process Database` . 이 사용 권한은 데이터베이스 수준에서 설정되며, 데이터베이스 내 모든 개체에 대한 처리를 허용합니다. 자세한 내용은 [처리 권한 부여&#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)

## <a name="read-definition"></a>Read Definition
 와 마찬가지로 `Process Database` `Read Definition` 데이터베이스 수준에서 사용 권한을 설정 하면 데이터베이스 내 다른 개체에 연계 효과가 적용 됩니다. 정의 읽기 권한을 더욱 세밀한 수준으로 설정하려는 경우 일반 창에서 데이터베이스 속성인 정의 읽기 선택을 취소해야 합니다. 자세한 내용은 [개체 메타데이터에 대한 정의 읽기 권한 부여&#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md)를 참조하세요.

## <a name="see-also"></a>참고 항목
 [Analysis Services &#40;&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) [프로세스 권한 부여 &#40;Analysis Services](grant-process-permissions-analysis-services.md) 를 사용 하 여 서버 관리자 권한을 부여 합니다&#41;


