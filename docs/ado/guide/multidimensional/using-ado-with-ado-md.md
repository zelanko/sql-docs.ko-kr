---
title: ADO MD를 사용 하 여 ADO를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2fd684e35c9cebf4a91a0b396e2c8b572e1ecf8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699855"
---
# <a name="using-ado-with-ado-md"></a>ADO MD에서 ADO 사용
ADO 및 ADO MD는 관련 하지만 별도 개체 모델입니다. ADO는 데이터 원본에 연결, 명령을 실행 하 고, 테이블 형식 데이터와 스키마 메타 데이터를 테이블 형식으로 검색 하 고 공급자 오류 정보 보기에 대 한 개체를 제공 합니다. ADO MD 다차원 데이터를 검색 하 고 다차원 스키마 메타 데이터 보기에 대 한 개체를 제공 합니다.  
  
 Mdp 작업할 때에 ADO, ADO MD 또는 응용 프로그램을 사용 하 여 둘 다 사용 하도록 선택할 수 있습니다. 프로젝트 내에서 두 라이브러리를 참조 하면 MDP에서 제공 하는 기능에 대 한 전체 액세스를 해야 합니다.  
  
 다차원 데이터 집합 결합, 테이블 형식 뷰를 소비자에 대 한 자주 유용 합니다. ADO를 사용 하 여 이렇게 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 소스를 지정 하 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 으로 ***원본*** 에 대 한 매개 변수를 [열기](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드의 **레코드 집합**, 아니라 원본 ADO MD **Cellset**합니다.  
  
 개체의 계층 구조가 아닌 테이블 형식 뷰의 스키마 메타 데이터를 보는 데 유용할 수도 있습니다. ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) 메서드는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체에는 사용자가 열 수 있습니다를 **레코드 집합** 스키마 정보를 포함 하는 합니다. 합니다 ***QueryType*** 의 매개 변수를 **OpenSchema** 메서드가 여러 [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) 와 특히 관련 된 값입니다. 이러한 값은 다음과 같습니다.  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 ADO MD 속성 또는 메서드를 사용 하 여 ADO 열거형 값을 사용 하려면 프로젝트가 ADO와 ADO MD 라이브러리를 참조 해야 합니다. 예를 들어 ADO를 사용할 수 있습니다 **adState** ADO MD를 사용 하 여 열거형 [상태](../../../ado/reference/ado-md-api/state-property-ado-md.md) 속성입니다. 라이브러리에 대 한 참조를 설정 하는 방법에 대 한 자세한 내용은 개발 도구 설명서를 참조 하세요.  
  
 ADO 개체 및 메서드에 대 한 자세한 내용은 참조는 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [다차원 스키마 및 데이터 개요](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [다차원 데이터 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
