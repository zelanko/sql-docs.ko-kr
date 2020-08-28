---
description: ADO MD에서 ADO 사용
title: ADO MD에서 ADO 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: rothja
ms.author: jroth
ms.openlocfilehash: 17d4094959c72389bf1cef71e6547394e676f78f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978584"
---
# <a name="using-ado-with-ado-md"></a>ADO MD에서 ADO 사용
ADO 및 ADO MD는 관련 되지만 별도의 개체 모델입니다. ADO는 데이터 원본에 연결 하 고, 명령을 실행 하 고, 테이블 형식 데이터 및 스키마 메타 데이터를 테이블 형식으로 검색 하 고, 공급자 오류 정보를 볼 수 있는 개체를 제공 합니다. ADO MD 다차원 데이터를 검색 하 고 다차원 스키마 메타 데이터를 볼 개체를 제공 합니다.  
  
 .MDP를 사용 하 여 작업 하는 경우 응용 프로그램에서 ADO, ADO MD 또는 둘 다를 사용 하도록 선택할 수 있습니다. 프로젝트 내에서 두 라이브러리를 모두 참조 하 여 .MDP에서 제공 하는 기능에 대 한 모든 액세스 권한을 갖습니다.  
  
 일반적으로 소비자는 다차원 데이터 집합의 플랫 테이블 뷰를 얻는 것이 유용 합니다. ADO [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체를 사용 하 여이 작업을 수행할 수 있습니다. ADO MD **셀**집합의 원본이 아닌 **레코드 집합**의 [Open](../../reference/ado-api/open-method-ado-recordset.md) 메서드에 대 한 원본 매개 변수로 [셀](../../reference/ado-md-api/cellset-object-ado-md.md) 집합 ***의 원본을 지정*** 합니다.  
  
 또한 개체의 계층 구조가 아닌 테이블 형식 뷰에서 스키마 메타 데이터를 보는 것이 유용할 수 있습니다. [Connection](../../reference/ado-api/connection-object-ado.md) 개체의 ADO [OpenSchema](../../reference/ado-api/openschema-method.md) 메서드를 사용 하면 사용자가 스키마 정보를 포함 하는 **레코드 집합** 을 열 수 있습니다. **OpenSchema** 메서드의 ***QueryType*** 매개 변수에는 mdps와 관련 된 여러 [schemaenum](../../reference/ado-api/schemaenum.md) 값이 있습니다. 이러한 값은 다음과 같습니다.  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 ADO MD 속성이 나 메서드를 사용 하 여 ADO 열거형 값을 사용 하려면 프로젝트에서 ADO 및 ADO MD 라이브러리를 모두 참조 해야 합니다. 예를 들어 ADO MD [State](../../reference/ado-md-api/state-property-ado-md.md) 속성에 ADO **adstate** 열거형 값을 사용할 수 있습니다. 라이브러리에 대 한 참조를 설정 하는 방법에 대 한 자세한 내용은 개발 도구의 설명서를 참조 하세요.  
  
 ADO 개체 및 메서드에 대 한 자세한 내용은 [ADO API 참조](../../reference/ado-api/ado-api-reference.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ADO MD 개체 모델](../../reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) (ADO MD)](./ado-multidimensional-ado-md.md)   
 [다차원 스키마 및 데이터 개요](./overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD를 사용한 프로그래밍](./programming-with-ado-md.md)   
 [다차원 데이터 작업](./working-with-multidimensional-data.md)