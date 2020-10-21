---
description: Integration Services 트랜잭션
title: Integration Services 트랜잭션 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4180ef12f33562a9c2bbb3349aef0acd1a0d1653
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193835"
---
# <a name="integration-services-transactions"></a>Integration Services 트랜잭션

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  패키지는 트랜잭션을 사용하여 태스크가 원자 단위로 수행되는 데이터베이스 동작을 바인딩하며 이를 통해 데이터 무결성을 유지 관리합니다. 패키지, For Loop, Foreach Loop, Sequence 컨테이너 및 각 작업을 캡슐화하는 태스크 호스트 등의 모든 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 컨테이너 유형은 트랜잭션을 사용하도록 구성할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 트랜잭션 구성을 위해 **NotSupported**, **Supported**및 **Required**의 세 가지 옵션을 제공합니다.  
  
-   **Required** 는 부모 컨테이너가 이미 트랜잭션을 시작한 경우를 제외하고 컨테이너가 트랜잭션을 시작하도록 합니다. 트랜잭션이 이미 있는 경우 컨테이너는 해당 트랜잭션에 참여합니다. 예를 들어 트랜잭션을 지원하도록 구성되지 않은 패키지가 **Required** 옵션을 사용하는 시퀀스 컨테이너를 포함하는 경우 시퀀스 컨테이너가 자체 트랜잭션을 시작합니다. **Required** 옵션을 사용하도록 패키지를 구성한 경우 시퀀스 컨테이너는 패키지 트랜잭션에 참여합니다.  
  
-   **Supported** 는 컨테이너가 트랜잭션을 시작하지 않고 부모 컨테이너에 의해 시작된 트랜잭션에 참여하도록 합니다. 예를 들어 4개의 SQL 실행 태스크가 있는 패키지가 트랜잭션을 시작하고 4개의 태스크가 모두 **Supported** 옵션을 사용하는 경우 하나의 태스크라도 실패하면 SQL 실행 태스크에 의해 수행되는 데이터베이스 업데이트가 롤백됩니다. 패키지가 트랜잭션을 시작하지 않은 경우 4개의 SQL 실행 태스크는 트랜잭션에 의해 바인드되지 않으며 실패한 태스크에 의해 수행된 것을 제외한 어떤 데이터베이스 업데이트도 롤백되지 않습니다.  
  
-   **NotSupported** 는 컨테이너가 트랜잭션을 시작하거나 기존 트랜잭션에 참여하지 않도록 합니다. 부모 컨테이너에 의해 시작된 트랜잭션은 트랜잭션을 지원하지 않도록 구성된 자식 컨테이너에 영향을 미치지 않습니다. 예를 들어 패키지가 트랜잭션을 시작하도록 구성되어 있고 패키지에 있는 For Loop 컨테이너가 **NotSupported** 옵션을 사용하는 경우 For Loop에 있는 모든 태스크는 실패하더라도 롤백될 수 없습니다.  
  
 컨테이너에서 TransactionOption 속성을 설정하여 트랜잭션을 구성할 수 있습니다. 이 속성은 **의** 속성 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]창을 사용하여 설정하거나 프로그래밍 방식으로 설정할 수 있습니다.  
  
> [!NOTE]  
>  **TransactionOption** 속성은 컨테이너에서 요청하는 **IsolationLevel** 속성 값의 적용 여부에 영향을 줍니다. 자세한 내용은 **패키지 속성 설정** 항목의 [IsolationLevel](../integration-services/set-package-properties.md)속성에 대한 설명을 참조하십시오.  
  
## <a name="configure-a-package-to-use-transactions"></a>트랜잭션을 사용하도록 패키지 구성
트랜잭션을 사용하도록 패키지를 구성할 때는 다음과 같은 두 가지 옵션을 사용할 수 있습니다.  
  
-   패키지에서 단일 트랜잭션을 사용합니다. 이 경우 패키지 자체에서 이 트랜잭션을 *시작하고* 패키지에 포함된 개별 태스크와 컨테이너는 이 단일 트랜잭션에 참여합니다.  
  
-   패키지에서 여러 트랜잭션을 사용합니다. 이 경우 패키지가 트랜잭션을 지원하지만 실제로는 패키지에 포함된 개별 태스크와 컨테이너가 트랜잭션을 시작합니다.  
  
 다음 절차에서는 위의 두 옵션을 구성하는 방법에 대해 설명합니다.  
  
### <a name="configure-a-package-to-use-a-single-transaction"></a>단일 트랜잭션을 사용하도록 패키지 구성  
 이 옵션에서는 패키지 자체에서 단일 트랜잭션을 시작합니다. 패키지의 TransactionOption 속성을 **Required**로 설정하여 이 트랜잭션을 시작하도록 패키지를 구성합니다.  
  
 그런 다음 이 단일 트랜잭션에 특정 태스크와 컨테이너를 등록합니다. 트랜잭션에 태스크와 컨테이너를 등록하려면 해당 태스크 또는 컨테이너의 TransactionOption 속성을 **Supported**로 설정합니다.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 트랜잭션을 사용하도록 구성할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  제어 흐름 디자인 화면 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
5.  **속성** 창에서 TransactionOption 속성을 **Required**로 설정합니다.  
  
6.  **제어 흐름** 탭의 디자인 화면에서 트랜잭션에 등록할 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
7.  **속성** 창에서 TransactionOption 속성을 **Supported**로 설정합니다.  
  
    > [!NOTE]  
    >  트랜잭션에 연결을 참여시키려면 트랜잭션에서 해당 연결을 사용하는 태스크를 등록합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
8.  트랜잭션에 등록할 각 태스크와 컨테이너에 대해 6-7단계를 반복합니다.  
  
### <a name="configure-a-package-to-use-multiple-transactions"></a>여러 트랜잭션을 사용하도록 패키지 구성  
 이 옵션에서는 패키지 자체에서 트랜잭션을 지원하지만 트랜잭션을 시작하지는 않습니다. 패키지의 TransactionOption 속성을 **Supported**로 설정하여 트랜잭션을 지원하도록 패키지를 구성합니다.  
  
 그런 다음 패키지에 포함된 태스크와 컨테이너 중에서 원하는 태스크와 컨테이너를 트랜잭션을 시작하거나 트랜잭션에 참여하도록 구성합니다. 트랜잭션을 시작하도록 태스크나 컨테이너를 구성하려면 태스크 또는 컨테이너의 TransactionOption 속성을 **Required**로 설정합니다.   
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 트랜잭션을 사용하도록 구성할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  제어 흐름 디자인 화면 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
5.  **속성** 창에서 TransactionOption 속성을 **Supported**로 설정합니다.  
  
    > [!NOTE]  
    >  패키지는 트랜잭션을 지원하지만 트랜잭션은 패키지의 태스크나 컨테이너에 의해 시작됩니다.  
  
6.  **제어 흐름** 탭의 디자인 화면에서 트랜잭션을 시작할 패키지에서 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
7.  **속성** 창에서 TransactionOption 속성을 **Required**로 설정합니다.  
  
8.  트랜잭션이 컨테이너에 의해 시작되는 경우 트랜잭션에 등록할 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
9. **속성** 창에서 TransactionOption 속성을 **Supported**로 설정합니다.  
  
    > [!NOTE]  
    >  트랜잭션에 연결을 참여시키려면 트랜잭션에서 해당 연결을 사용하는 태스크를 등록합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
10. 트랜잭션을 시작하는 각 태스크와 컨테이너에 대해 6-9단계를 반복합니다.  

## <a name="multiple-transactions-in-a-package"></a>패키지에 여러 트랜잭션 포함
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지 내의 관련 없는 트랜잭션을 한 개의 패키지가 포함하는 것이 가능합니다. 중첩 컨테이너 계층 중간의 컨테이너가 트랜잭션을 지원하지 않으면 위 또는 아래에 위치한 컨테이너에서 별도의 트랜잭션을 시작합니다(트랜잭션을 지원하도록 구성된 경우). 트랜잭션은 중첩 컨테이너 계층의 가장 안쪽 태스크부터 순서대로 패키지에 커밋 또는 롤백합니다. 그러나 내부 트랜잭션이 커밋한 후에는 외부 트랜잭션이 중단되더라도 롤백하지 않습니다.  
  
### <a name="example-of-multiple-transactions-in-a-package"></a>패키지에 여러 트랜잭션 포함의 예 
 예를 들어 한 패키지가 두 개의 Foreach 루프 컨테이너를 포함하고 각 컨테이너가 다시 두 개의 SQL 실행 태스크를 포함하는 경우 시퀀스 컨테이너는 트랜잭션을 지원하지만 Foreach 루프 컨테이너는 지원하지 않고 SQL 실행 태스크는 지원합니다. 이 예에서 각 SQL 실행 태스크는 자체 트랜잭션을 시작하며 시퀀스 태스크에서 트랜잭션이 중단된 경우에도 롤백하지 않습니다.  
  
 시퀀스 컨테이너, Foreach 루프 컨테이너 및 SQL 실행 태스크의 TransactionOption 속성은 다음과 같이 설정됩니다.  
  
-   시퀀스 컨테이너의 TransactionOption 속성은 **Required**로 설정됩니다.  
  
-   Foreach 루프 컨테이너의 TransactionOption 속성은 **NotSupported**로 설정됩니다.  
  
-   SQL 실행 태스크의 TransactionOption 속성은 **Required**로 설정됩니다.  
  
 다음 다이어그램에서는 패키지 내의 관련 없는 트랜잭션 다섯 개를 보여 줍니다. 한 개의 트랜잭션은 시퀀스 컨테이너에서 시작되며 네 개의 트랜잭션은 SQL 실행 태스크에서 시작됩니다.  
  
 ![다중 트랜잭션 구현](../integration-services/media/mw-dts-trans2.gif "다중 트랜잭션 구현")  
 
## <a name="inherited-transactions"></a>상속된 트랜잭션
 패키지 실행 태스크를 사용하면 패키지가 다른 패키지를 실행할 수 있습니다. 패키지 실행 태스크에서 실행하는 패키지인 자식 패키지는 자체의 패키지 트랜잭션을 만들거나 부모 패키지 트랜잭션을 상속할 수 있습니다.  
  
 다음 두 가지 조건에 모두 해당하면 자식 패키지는 부모 패키지 트랜잭션을 상속합니다.  
  
-   패키지 실행 태스크가 패키지를 호출합니다.  
  
-   패키지를 호출한 패키지 실행 태스크가 부모 패키지 트랜잭션도 조인했습니다.  
  
 자식 패키지가 트랜잭션에 조인하지 않으면 자식 패키지 내의 컨테이너 및 태스크가 부모 패키지 트랜잭션에 조인할 수 없습니다.  
  
### <a name="example-of-inherited-transactions"></a>상속된 트랜잭션의 예  
 다음 다이어그램에서 트랜잭션을 사용하는 3개의 패키지가 있습니다. 각 패키지는 여러 태스크를 포함합니다. 트랜잭션 동작을 강조하기 위해 패키지 실행 태스크만 표시했습니다. 패키지 A는 패키지 B와 C를 실행하고 차례로 패키지 B는 패키지 D와 E를 실행하며 패키지 C는 패키지 F를 실행합니다.  
  
 패키지 및 태스크는 다음 트랜잭션 특성을 가집니다.  
  
-   패키지 A 및 C의**트랜잭션 옵션** 은 **필수** 로 설정됩니다.  
  
-   패키지 B 및 D, 패키지 실행 태스크 B, 패키지 실행 D 및 패키지 실행 F의**트랜잭션 옵션** 은 **지원** 으로 설정됩니다.  
  
-   패키지 E, 패키지 실행 태스크 C 및 패키지 실행 E의**트랜잭션 옵션** 은 **지원되지 않음** 으로 설정됩니다.  
  
 ![상속된 트랜잭션의 흐름](../integration-services/media/mw-dts-executepack.gif "상속된 트랜잭션의 흐름")  
  
 패키지 B, D 및 F만 부모 패키지에서 트랜잭션을 상속할 수 있습니다.  
  
 패키지 B 및 D는 패키지 A가 시작한 트랜잭션을 상속합니다.  
  
 패키지 F는 패키지 C가 시작한 트랜잭션을 상속합니다.  
  
 패키지 A와 C는 자체 트랜잭션을 제어합니다.  
  
 패키지 E는 트랜잭션을 사용하지 않습니다.  
 
  
## <a name="external-resources"></a>외부 리소스  
  
-    www.mssqltips.com 의 블로그 항목 - [SQL Server Integration Services SSIS에서 트랜잭션을 사용하는 방법](https://go.microsoft.com/fwlink/?LinkId=157783)  
  
## <a name="see-also"></a>참고 항목  
 [상속된 트랜잭션]()   
 [여러 트랜잭션]()  
  
