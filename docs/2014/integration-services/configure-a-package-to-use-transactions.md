---
title: 트랜잭션을 사용 하도록 패키지 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], configuring packages to use
ms.assetid: 8bf14957-27b4-456b-81d9-e1a0e0ca94b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 16d1f0f4c24f18327ee31da1fb85a74d19588384
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060857"
---
# <a name="configure-a-package-to-use-transactions"></a>트랜잭션을 사용하도록 패키지 구성
  트랜잭션을 사용하도록 패키지를 구성할 때는 다음과 같은 두 가지 옵션을 사용할 수 있습니다.  
  
-   패키지에서 단일 트랜잭션을 사용합니다. 이 경우 패키지 자체에서 이 트랜잭션을 *시작하고* 패키지에 포함된 개별 태스크와 컨테이너는 이 단일 트랜잭션에 참여합니다.  
  
-   패키지에서 여러 트랜잭션을 사용합니다. 이 경우 패키지가 트랜잭션을 지원하지만 실제로는 패키지에 포함된 개별 태스크와 컨테이너가 트랜잭션을 시작합니다.  
  
 다음 절차에서는 위의 두 옵션을 구성하는 방법에 대해 설명합니다.  
  
## <a name="configuring-a-single-transaction"></a>단일 트랜잭션 구성  
 이 옵션에서는 패키지 자체에서 단일 트랜잭션을 시작합니다. 패키지의 TransactionOption 속성을로 `Required`설정 하 여이 트랜잭션을 시작 하도록 패키지를 구성 합니다.  
  
 그런 다음 이 단일 트랜잭션에 특정 태스크와 컨테이너를 등록합니다. 트랜잭션에 태스크 또는 컨테이너를 등록 하려면 해당 태스크 또는 컨테이너의 TransactionOption 속성을로 `Supported`설정 합니다.  
  
#### <a name="to-configure-a-package-to-use-a-single-transaction"></a>단일 트랜잭션을 사용하도록 패키지를 구성하려면  
  
1.  
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 트랜잭션을 사용하도록 구성할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  제어 흐름 디자인 화면 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
5.  **속성** 창에서 TransactionOption 속성을로 `Required`설정 합니다.  
  
6.  
  **제어 흐름** 탭의 디자인 화면에서 트랜잭션에 등록할 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
7.  **속성** 창에서 TransactionOption 속성을로 `Supported`설정 합니다.  
  
    > [!NOTE]  
    >  트랜잭션에 연결을 참여시키려면 트랜잭션에서 해당 연결을 사용하는 태스크를 등록합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
8.  트랜잭션에 등록할 각 태스크와 컨테이너에 대해 6-7단계를 반복합니다.  
  
## <a name="configuring-multiple-transactions"></a>여러 트랜잭션 구성  
 이 옵션에서는 패키지 자체에서 트랜잭션을 지원하지만 트랜잭션을 시작하지는 않습니다. 패키지의 TransactionOption 속성을로 `Supported`설정 하 여 트랜잭션을 지원 하도록 패키지를 구성 합니다.  
  
 그런 다음 패키지에 포함된 태스크와 컨테이너 중에서 원하는 태스크와 컨테이너를 트랜잭션을 시작하거나 트랜잭션에 참여하도록 구성합니다. 트랜잭션을 시작 하도록 태스크 나 컨테이너를 구성 하려면 해당 태스크 또는 컨테이너의 TransactionOption 속성을로 `Required`설정 합니다.  
  
#### <a name="to-configure-a-package-to-use-multiple-transactions"></a>여러 트랜잭션을 사용하도록 패키지를 구성하려면  
  
1.  
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 트랜잭션을 사용하도록 구성할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  제어 흐름 디자인 화면 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
5.  **속성** 창에서 TransactionOption 속성을로 `Supported`설정 합니다.  
  
    > [!NOTE]  
    >  패키지는 트랜잭션을 지원하지만 트랜잭션은 패키지의 태스크나 컨테이너에 의해 시작됩니다.  
  
6.  
  **제어 흐름** 탭의 디자인 화면에서 트랜잭션을 시작할 패키지에서 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
7.  **속성** 창에서 TransactionOption 속성을로 `Required`설정 합니다.  
  
8.  트랜잭션이 컨테이너에 의해 시작되는 경우 트랜잭션에 등록할 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
9. **속성** 창에서 TransactionOption 속성을로 `Supported`설정 합니다.  
  
    > [!NOTE]  
    >  트랜잭션에 연결을 참여시키려면 트랜잭션에서 해당 연결을 사용하는 태스크를 등록합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
10. 트랜잭션을 시작하는 각 태스크와 컨테이너에 대해 6-9단계를 반복합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 트랜잭션](integration-services-transactions.md)  
  
  
