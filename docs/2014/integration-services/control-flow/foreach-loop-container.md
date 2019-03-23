---
title: Foreach 루프 컨테이너 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.f1
helpviewer_keywords:
- repeating control flow
- Foreach Loop containers
- foreach enumerators [Integration Services]
- containers [Integration Services], Foreach Loop
ms.assetid: dd6cc2ba-631f-4adf-89dc-29ef449c6933
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bb50b4000397ca3dd51be58867e45135d1d587f1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380261"
---
# <a name="foreach-loop-container"></a>Foreach 루프 컨테이너
  Foreach 루프 컨테이너는 패키지의 반복 제어 흐름을 정의합니다. 루프 구현은 프로그래밍 언어에서의 **Foreach** 루프 구조와 유사합니다. 패키지에서 Foreach 열거자를 사용하면 루프를 사용할 수 있습니다.  Foreach 루프 컨테이너는 지정한 열거자의 각 멤버에 대해 제어 흐름을 반복합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 는 다음 열거자 유형을 제공합니다.  
  
-   Foreach ADO 열거자는 테이블의 행을 열거합니다. 예를 들어 ADO 레코드 집합의 행을 가져올 수 있습니다.  
  
     레코드 집합 대상은 `Object` 데이터 형식의 패키지 변수에 저장된 레코드 집합의 메모리에 데이터를 저장합니다. 일반적으로 Foreach 루프 컨테이너를 Foreach ADO 열거자와 함께 사용하여 레코드 집합의 행을 한 번에 하나씩 처리합니다. Foreach ADO 열거자에 대해 지정된 변수는 개체 데이터 형식이어야 합니다. 레코드 집합 대상에 대한 자세한 내용은 [Use a Recordset Destination](../data-flow/recordset-destination.md)을 참조하십시오.  
  
-   Foreach ADO.NET 스키마 행 집합 열거자는 데이터 원본에 대한 스키마 정보를 열거합니다. 예를 들어 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 테이블 목록을 열거하고 가져올 수 있습니다.  
  
-   Foreach File 열거자는 폴더의 파일을 열거합니다. 열거자는 하위 폴더를 포함할 수 있습니다. 예를 들어 Windows 폴더 및 하위 폴더에서 파일 이름 확장명이 *.log인 모든 파일을 읽을 수 있습니다.  
  
-   Foreach From Variable 열거자는 지정한 변수에 포함된 열거 가능 개체를 열거합니다. 열거 가능 개체는 배열, ADO.NET `DataTable`, [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 열거자 등이 될 수 있습니다. 예를 들어 서버 이름을 포함하는 배열 값을 열거할 수 있습니다.  
  
-   Foreach Item 열거자는 컬렉션 항목을 열거합니다. 예를 들어 프로세스 실행 태스크가 사용하는 실행 파일 이름 및 작업 디렉터리를 열거할 수 있습니다.  
  
-   Foreach Nodelist 열거자는 XPath(XML Path Language) 식의 결과 집합을 열거합니다. 예를 들어 식 `/authors/author[@period='classical']`은 classical period의 모든 author 목록을 열거하고 가져옵니다.  
  
-   Foreach SMO 열거자는 SMO([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Object) 개체를 열거합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 뷰 목록을 열거하고 가져올 수 있습니다.  
  
-   Azure 스토리지의 blob 컨테이너에 blob를 열거하는 Foreach Azure Blob 열거자입니다.  
  
-   Foreach ADLS File 열거자는 ADLS 디렉터리의 파일을 열거 합니다.
  
 다음 다이어그램에서는 파일 시스템 태스크가 있는 Foreach 루프 컨테이너를 보여 줍니다. Foreach 루프는 Foreach File 열거자를 사용하며 파일 시스템 태스크는 파일을 복사하도록 구성되어 있습니다. 열거자가 지정한 폴더에 4개 파일이 들어 있으면 루프가 4번 반복되어 4개 파일이 복사됩니다.  
  
 ![폴더를 열거하는 Foreach 루프 컨테이너](../media/ssis-foreachloop.gif "폴더를 열거하는 Foreach 루프 컨테이너")  
  
 변수 및 속성 식의 조합을 사용하여 패키지 개체의 속성을 열거자 컬렉션 값으로 업데이트할 수 있습니다. 먼저 컬렉션 값을 사용자 정의 변수에 매핑한 다음 이 변수를 사용하는 속성 식을 속성에 구현합니다. Foreach File 열거자 컬렉션 값 이라는 변수에 매핑되는 예를 들어 `MyFile` 한 변수는 다음 메일 보내기 태스크의 Subject 속성에 대 한 속성 식에 사용 됩니다. 패키지를 실행하면 루프가 반복될 때마다 Subject 속성이 파일 이름으로 업데이트됩니다. 자세한 내용은 [패키지에서 속성 식 사용](../expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
 열거자 컬렉션 값에 매핑된 변수를 식과 스크립트에 사용할 수도 있습니다.  
  
 Foreach 루프 컨테이너는 여러 개의 태스크와 컨테이너를 포함할 수 있지만 하나의 열거자 유형만 사용할 수 있습니다. Foreach 루프 컨테이너에 여러 개의 태스크가 포함되어 있으면 열거자 컬렉션 값을 각 태스크의 여러 속성에 매핑할 수 있습니다.  
  
 Foreach 루프 컨테이너에 트랜잭션 특성을 설정하여 패키지 제어 흐름의 하위 집합에 대한 트랜잭션을 정의할 수 있습니다. 이렇게 하면 패키지 수준이 아닌 Foreach 루프 수준에서 트랜잭션을 관리할 수 있습니다. 예를 들어 Foreach 루프 컨테이너가 별모양 스키마의 차원 및 팩트 테이블을 업데이트하는 제어 흐름을 반복하는 경우 모든 팩트 테이블이 성공적으로 업데이트되지 않으면 어떤 테이블도 업데이트하지 않도록 트랜잭션을 구성할 수 있습니다. 자세한 내용은 [Integration Services 트랜잭션](../integration-services-transactions.md)을 참조하세요.  
  
## <a name="enumerator-types"></a>열거자 유형  
 열거자는 구성 가능하며 열거자에 따라 다른 정보를 제공해야 합니다.  
  
 다음 표에서는 각 열거자 유형에 필요한 정보를 요약해서 보여 줍니다.  
  
|Enumerator|구성 요구 사항|  
|----------------|--------------------------------|  
|Foreach ADO|ADO 개체 원본 변수와 열거자 모드 지정 변수는 개체 데이터 형식이어야 합니다.|  
|Foreach ADO.NET 스키마 행 집합|데이터베이스에 대한 연결과 열거할 스키마 지정|  
|Foreach File|열거할 폴더 및 파일, 검색된 파일의 파일 이름 형식 및 하위 폴더 포함 여부 지정|  
|Foreach From Variable|열거할 개체가 포함된 변수 지정|  
|Foreach Item|열과 열 데이터 형식을 포함하여 Foreach Item 컬렉션의 항목 정의|  
|Foreach Nodelist|XML 문서의 원본 지정 및 XPath 작업 구성|  
|Foreach SMO|데이터베이스에 대한 연결과 열거할 SMO 개체 지정|  
|Foreach Azure Blob|열거할 blob이 포함 된 Azure blob 컨테이너를 지정 합니다.|  
|Foreach ADLS 파일|일부 필터와 함께 열거할 파일을 포함 하는 ADLS 디렉터리를 지정 합니다.|
  
## <a name="property-expressions-in-foreach-loop-containers"></a>Foreach 루프 컨테이너의 속성 식  
 여러 개의 실행 파일을 동시에 실행하도록 패키지를 구성할 수 있습니다. 패키지가 속성 식을 구현하는 Foreach 루프 컨테이너를 포함하는 경우에는 이 구성 사용 시 주의해야 합니다.  
  
 Foreach 루프 열거자가 사용하는 연결 관리자의 ConnectionString 속성 값을 설정하기 위해 속성 식을 구현하면 유용합니다. ConnectionString의 속성 식은 열거자의 컬렉션 값에 매핑되는 변수에 의해 설정되며 루프가 반복될 때마다 업데이트됩니다.  
  
 루프 태스크의 병렬 실행 타이밍이 불확실해지는 부정적인 결과가 발생하지 않도록 하려면 한 번에 하나의 실행 파일만 실행하도록 패키지를 구성해야 합니다. 예를 들어 한 패키지가 여러 태스크를 동시에 실행할 수 있는 경우 SQL 실행 태스크의 인스턴스 두 개가 동시에 쓰기를 시도하면 폴더에 있는 파일을 열거하고 파일 이름을 검색한 다음 SQL 실행 태스크를 사용하여 파일 이름을 테이블에 삽입하는 Foreach 루프 컨테이너에 쓰기 충돌이 발생할 수 있습니다. 자세한 내용은 [패키지에서 속성 식 사용](../expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Foreach 루프 컨테이너 구성](foreach-loop-container.md)  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
## <a name="related-content"></a>관련 내용  
 bidn.com의 블로그 항목 - [각 노드 목록 열거자에 대한 SSIS](https://go.microsoft.com/fwlink/?LinkId=220671)  
  
## <a name="see-also"></a>관련 항목:  
 [제어 흐름](control-flow.md)   
 [Integration Services 컨테이너](integration-services-containers.md)  
  
  
