---
title: 변수를 쿼리 매개 변수를 매핑하는 SQL 실행 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameterized SQL commands [Integration Services]
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- Execute SQL task [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 6a164349-dfcf-4995-80bc-d4e7aee52a83
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cc38f51ef997ea2100e356573af46c3d29aafd66
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62890909"
---
# <a name="map-query-parameters-to-variables-in-an-execute-sql-task"></a>쿼리 매개 변수를 SQL 실행 태스크의 변수에 매핑

  이 항목에서는 SQL 실행 태스크에서 매개 변수가 있는 SQL 문을 사용하는 방법과 SQL 문의 변수와 매개 변수 간 매핑을 만드는 방법에 대해 설명합니다.  
  
 다른 연결 형식에 사용할 매개 변수 이름, 매개 변수 표식 및 SQL 실행 태스크에 대한 자세한 내용은 [SQL 실행 태스크](control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)를 참조하세요.  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>쿼리 매개 변수를 변수에 매핑하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 작업하려는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  패키지에 아직 SQL 실행 태스크가 포함되어 있지 않으면 패키지의 제어 흐름에 해당 작업을 추가합니다. 자세한 내용은 참조 하세요. [작업 또는 제어 흐름 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
5.  SQL 실행 태스크를 두 번 클릭합니다.  
  
6.  다음 방법 중 하나로 매개 변수가 있는 SQL 명령을 제공합니다.  
  
    -   직접 입력을 사용하여 SQLStatement 속성에 SQL 명령을 입력합니다.  
  
    -   직접 입력을 사용하여 **쿼리 작성**을 클릭한 후 쿼리 작성기에서 제공하는 그래픽 도구를 사용하여 SQL 명령을 만듭니다.  
  
    -   파일 연결을 사용한 후 SQL 명령이 포함된 파일을 참조합니다.  
  
    -   변수를 사용한 후 SQL 명령이 포함된 변수를 참조합니다.  
  
     매개 변수가 있는 SQL 문에서 사용하는 매개 변수 표식은 SQL 실행 태스크에서 사용하는 연결 형식에 따라 다릅니다.  
  
    |연결 형식|매개 변수 표식|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET 및 SQLMOBILE|@\<매개 변수 이름>|  
    |ODBC|?|  
    |EXCEL 및 OLE DB|?|  
  
     다음 표에서는 연결 관리자 유형별 SELECT 명령의 예를 나열합니다. 매개 변수는 WHERE 절에 필터 값을 제공합니다. 이 예에서는 SELECT를 사용하여 **의** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] 테이블에서 **ProductID** 가 두 매개 변수로 지정된 값보다 크고 작은 제품을 반환합니다.  
  
    |연결 형식|SELECT 구문|  
    |---------------------|-------------------|  
    |EXCEL, ODBC 및 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
     저장 프로시저에서 매개 변수를 사용하는 예는 [SQL 실행 태스크의 매개 변수 및 반환 코드](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)를 참조하십시오.  
  
7.  **매개 변수 매핑**을 클릭합니다.  
  
8.  매개 변수 매핑을 추가하려면 **추가**를 클릭합니다.  
  
9. **매개 변수 이름** 상자에 이름을 제공합니다.  
  
     사용하는 매개 변수 이름은 SQL 실행 태스크에 사용하는 연결 형식에 따라 다릅니다.  
  
    |연결 형식|매개 변수 이름|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, ...|  
    |ADO.NET 및 SQLMOBILE|@\<매개 변수 이름>|  
    |ODBC|1, 2, 3, ...|  
    |EXCEL 및 OLE DB|0, 1, 2, 3, ...|  
  
10. **변수 이름** 목록에서 변수를 선택합니다. 자세한 내용은 [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)을 참조하세요.  
  
11. **방향** 목록에서 매개 변수가 입력, 출력 또는 반환 값인지 여부를 지정합니다.  
  
12. **데이터 형식** 목록에서 매개 변수의 데이터 형식을 설정합니다.  
  
    > [!IMPORTANT]  
    >  매개 변수의 데이터 형식은 변수의 데이터 형식과 호환되어야 합니다.  
  
13. SQL 문의 각 매개 변수에 대해 8에서 11단계를 반복합니다.  
  
    > [!IMPORTANT]  
    >  매개 변수 매핑의 순서는 SQL 문에 표시된 매개 변수의 순서와 동일해야 합니다.  
  
14. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL 실행 태스크](control-flow/execute-sql-task.md)   
 [매개 변수 및 반환 코드는 SQL 실행 태스크](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)   
 [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md)  
  
  
