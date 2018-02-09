---
title: "ADO MD와 함께 ADO를 사용 하 여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3761a5553b13dc65a15862c5e9b27cdc5634b52
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="using-ado-with-ado-md"></a>ADO MD와 함께 ADO 사용
ADO 및 ADO MD는 관련 하지만 별도 개체 모델입니다. ADO는 데이터 원본에 연결, 명령을 실행 하 고, 테이블 형식 데이터와 스키마 메타 데이터를 테이블 형식으로 검색 하 고 공급자 오류 정보 보기에 대 한 개체를 제공 합니다. ADO MD는 다차원 데이터를 검색 하 고 다차원 스키마 메타 데이터를 보기 위한 개체를 제공 합니다.  
  
 Mdp 작업할 때 ADO, ADO MD 또는 둘 다 응용 프로그램과 함께 사용할 수 있습니다. 프로젝트 내에서 두 라이브러리를 참조 하면 MDP에서 제공 하는 기능에 대 한 모든 권한을 갖습니다.  
  
 다차원 데이터 집합 결합, 테이블 형식 보기에 소비자가 자주 유용 합니다. ADO를 사용 하 여이 작업을 수행할 수 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 에 대 한 원본을 지정 프로그램 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 로 ***소스*** 에 대 한 매개 변수는 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 의 메서드는 **레코드 집합**, 아니라에 대 한 소스 ADO MD **셀 집합**합니다.  
  
 개체의 계층 구조가 아닌 테이블 형식 보기에서 스키마 메타 데이터를 보는 데 유용할 수도 있습니다. ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) 에서 메서드는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체에는 사용자가 열 수 있습니다는 **레코드 집합** 스키마 정보를 포함 하는 합니다. ***QueryType*** 의 매개 변수는 **OpenSchema** 메서드에 몇 가지 [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) 와 특별히 관련 된 값입니다. 이러한 값은 다음과 같습니다.  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 ADO 열거형 값에서 ADO MD 속성 또는 메서드를 사용 하려면 프로젝트에는 ADO와 ADO MD 라이브러리를 참조 해야 합니다. ADO를 사용 하 여 예를 들어 **adState** ADO MD를 사용 하 여 열거형 값 [상태](../../../ado/reference/ado-md-api/state-property-ado-md.md) 속성입니다. 라이브러리에 대 한 참조를 설정 하는 방법에 대 한 자세한 내용은 개발 도구의 설명서를 참조 합니다.  
  
 ADO 개체 및 메서드에 대 한 자세한 내용은 참조는 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [다차원 스키마 및 데이터 개요](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [다차원 데이터 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
