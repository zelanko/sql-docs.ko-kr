---
title: Integration Services 트랜잭션 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 880fd7d655b572f264f5120849cb5a927cdaaa59
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082714"
---
# <a name="integration-services-transactions"></a>Integration Services 트랜잭션
  패키지는 트랜잭션을 사용하여 태스크가 원자 단위로 수행되는 데이터베이스 동작을 바인딩하며 이를 통해 데이터 무결성을 유지 관리합니다. 각 작업을 캡슐화하는 For Loop, Foreach Loop, Sequence 컨테이너 및 태스크 호스트 등의 모든 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 컨테이너는 트랜잭션을 사용하도록 구성할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 트랜잭션 구성을 위해 **NotSupported**, **Supported**및 **Required**의 세 가지 옵션을 제공합니다.  
  
-   **Required** 는 부모 컨테이너가 이미 트랜잭션을 시작한 경우를 제외하고 컨테이너가 트랜잭션을 시작하도록 합니다. 트랜잭션이 이미 있는 경우 컨테이너는 해당 트랜잭션에 참여합니다. 예를 들어 트랜잭션을 지원하도록 구성되지 않은 패키지가 **Required** 옵션을 사용하는 시퀀스 컨테이너를 포함하는 경우 시퀀스 컨테이너가 자체 트랜잭션을 시작합니다. **Required** 옵션을 사용하도록 패키지를 구성한 경우 시퀀스 컨테이너는 패키지 트랜잭션에 참여합니다.  
  
-   **Supported** 는 컨테이너가 트랜잭션을 시작하지 않고 부모 컨테이너에 의해 시작된 트랜잭션에 참여하도록 합니다. 예를 들어 4개의 SQL 실행 태스크가 있는 패키지가 트랜잭션을 시작하고 4개의 태스크가 모두 **Supported** 옵션을 사용하는 경우 하나의 태스크라도 실패하면 SQL 실행 태스크에 의해 수행되는 데이터베이스 업데이트가 롤백됩니다. 패키지가 트랜잭션을 시작하지 않은 경우 4개의 SQL 실행 태스크는 트랜잭션에 의해 바인드되지 않으며 실패한 태스크에 의해 수행된 것을 제외한 어떤 데이터베이스 업데이트도 롤백되지 않습니다.  
  
-   **NotSupported** 는 컨테이너가 트랜잭션을 시작하거나 기존 트랜잭션에 참여하지 않도록 합니다. 부모 컨테이너에 의해 시작된 트랜잭션은 트랜잭션을 지원하지 않도록 구성된 자식 컨테이너에 영향을 미치지 않습니다. 예를 들어 패키지가 트랜잭션을 시작하도록 구성되어 있고 패키지에 있는 For Loop 컨테이너가 **NotSupported** 옵션을 사용하는 경우 For Loop에 있는 모든 태스크는 실패하더라도 롤백될 수 없습니다.  
  
 컨테이너에서 TransactionOption 속성을 설정하여 트랜잭션을 구성할 수 있습니다. 이 속성은 **의** 속성 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]창을 사용하여 설정하거나 프로그래밍 방식으로 설정할 수 있습니다.  
  
> [!NOTE]  
>  `TransactionOption` 속성은 컨테이너에서 요청하는 `IsolationLevel` 속성 값의 적용 여부에 영향을 줍니다. 자세한 내용은 참조에 대 한 설명을 `IsolationLevel` 항목에서 속성 [패키지 속성 설정](set-package-properties.md)합니다.  
  
### <a name="to-configure-a-package-to-use-transactions"></a>트랜잭션을 사용하도록 패키지를 구성하려면  
  
-   [트랜잭션을 사용하도록 패키지 구성](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
## <a name="external-resources"></a>외부 리소스  
  
-   www.mssqltips.com의 블로그 항목 - [SQL Server Integration Services SSIS에서 트랜잭션을 사용하는 방법](http://go.microsoft.com/fwlink/?LinkId=157783)  
  
## <a name="see-also"></a>관련 항목  
 [상속 된 트랜잭션](../../2014/integration-services/inherited-transactions.md)   
 [여러 트랜잭션](../../2014/integration-services/multiple-transactions.md)  
  
  