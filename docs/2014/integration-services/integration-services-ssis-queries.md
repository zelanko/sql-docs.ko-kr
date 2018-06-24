---
title: Integration Services(SSIS) 쿼리 | Microsoft Docs
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
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4188992529956ca06b22389dc4aadf1cc6ff6b7a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080215"
---
# <a name="integration-services-ssis-queries"></a>Integration Services(SSIS) 쿼리
  SQL 쿼리는 SQL 실행 태스크, OLE DB 원본, OLE DB 대상 및 조회 변환에서 사용될 수 있습니다. SQL 실행 태스크에서 SQL 문은 데이터베이스 개체 및 데이터를 생성, 업데이트 및 삭제할 수 있으며 저장 프로시저를 실행하고 SELECT 문을 수행할 수 있습니다. OLE DB 원본 및 조회 변환에서 일반적으로 SQL 문은 SELECT 문 또는 EXEC 문입니다. 후자는 결과 집합을 반환하는 저장 프로시저를 가장 자주 실행합니다.  
  
 쿼리 유효성 여부를 확인하기 위해 구문 분석을 수행할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 연결을 사용하는 쿼리를 구문 분석하는 경우 쿼리를 구문 분석하고 실행한 다음 구문 분석 결과에 실행 결과(성공 또는 실패)를 할당합니다. 쿼리가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]이외의 데이터로의 연결을 사용하는 경우 문은 구문 분석만 됩니다.  
  
 SQL 문은 디자이너에 직접 입력하여 정의하거나 해당 문을 포함하는 파일 연결 또는 변수를 지정하여 정의할 수 있습니다.  
  
## <a name="direct-input-sql"></a>SQL 직접 입력  
 쿼리 작성기는 SQL 실행 태스크, OLE DB 원본, OLE DB 대상 및 조회 변환의 사용자 인터페이스에서 사용할 수 있습니다. 쿼리 작성기를 사용하면 다음과 같은 이점이 있습니다.  
  
-   시각적으로 또는 SQL 명령으로 작업합니다.  
  
     쿼리 작성기는 쿼리를 시각적으로 구성하는 그래픽 창과 쿼리의 SQL 텍스트를 표시하는 텍스트 창을 포함합니다. 그래픽 또는 텍스트 창에서 작업할 수 있습니다. 쿼리 작성기는 뷰를 동기화하므로 쿼리 텍스트와 그래픽 표현이 항상 일치합니다.  
  
-   관련 테이블을 조인합니다.  
  
     둘 이상의 테이블을 쿼리에 추가하면 쿼리 작성기는 테이블이 관련되는 방법과 적절한 조인 명령을 생성하는 방법을 자동으로 결정합니다.  
  
-   데이터베이스를 쿼리 또는 업데이트할 수 있습니다.  
  
     쿼리 작성기에서 Transact-SQL SELECT 문을 사용하여 데이터를 반환하거나 데이터베이스에서 레코드를 업데이트, 추가 또는 삭제하는 쿼리를 작성할 수 있습니다.  
  
-   결과를 보고 즉시 편집합니다.  
  
     쿼리를 실행하고 레코드 집합을 표 형태로 사용하여 데이터베이스의 레코드를 스크롤하고 편집할 수 있습니다.  
  
 쿼리 작성기의 시각적 기능은 SELECT 문 작성으로 제한되지만 텍스트 창에 DELETE 및 UPDATE 문과 같은 다른 유형의 문을 위한 SQL을 입력할 수 있습니다. 이때 입력한 SQL 문을 반영하도록 그래픽 창이 자동으로 업데이트됩니다.  
  
 태스크 또는 데이터 흐름 구성 요소 대화 상자나 속성 창에 쿼리를 입력하여 직접 입력을 제공할 수 있습니다.  
  
 자세한 내용은 [Query Builder](../../2014/integration-services/query-builder.md)을 참조하세요.  
  
## <a name="sql-in-files"></a>파일 내의 SQL  
 SQL 실행 태스크의 SQL 문을 별도의 파일에 보관할 수 있습니다. 예를 들어 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 작성기와 같은 도구를 사용하여 쿼리를 작성하고 파일로 저장한 다음 패키지를 실행할 때 파일에서 쿼리를 읽을 수 있습니다. 이 파일에는 실행할 SQL 문과 주석만 포함될 수 있습니다. 파일에 저장된 SQL 문을 사용하려면 파일 이름 및 위치를 지정하는 파일 연결을 제공해야 합니다. 자세한 내용은 [File Connection Manager](connection-manager/file-connection-manager.md)를 참조하세요.  
  
## <a name="sql-in-variables"></a>변수 내의 SQL  
 SQL 실행 태스크의 SQL 문 원본이 변수인 경우 쿼리를 포함하는 변수의 이름을 지정하십시오. 쿼리 텍스트는 변수의 Value 속성에 포함됩니다. 변수의 ValueType 속성을 문자열 데이터 형식으로 설정한 다음 Value 속성에 SQL 문을 입력하거나 복사합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)을 참조하세요.  
  
  