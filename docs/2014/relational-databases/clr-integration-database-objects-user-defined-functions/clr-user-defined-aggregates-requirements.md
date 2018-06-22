---
title: CLR 사용자 정의 집계에 대 한 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
caps.latest.revision: 56
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7d3b1f45813de3d3ad4d3401c132181f0e4b20cb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081593"
---
# <a name="requirements-for-clr-user-defined-aggregates"></a>CLR 사용자 정의 집계 요구 사항
  공용 언어 런타임(CLR) 어셈블리의 형식이 필요한 집계 계약을 구현한다면 해당 형식을 사용자 정의 집계 함수로 등록할 수 있습니다. 이 계약은 `SqlUserDefinedAggregate` 특성과 집계 계약 메서드로 구성됩니다. 집계 계약은 집계의 중간 상태를 저장하는 메커니즘과 새 값을 누적하는 메커니즘을 포함하며 `Init`, `Accumulate`, `Merge` 및 `Terminate`의 4가지 메서드로 구성됩니다. 이러한 요구 사항을 충족할 경우에 사용자 정의 집계를 완전히 활용 할 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 항목의 다음 섹션에서는 사용자 정의 집계를 만드는 방법과 사용하는 방법에 대한 자세한 정보를 제공합니다. 예를 들어 참조 [Invoking CLR User-Defined 집계 함수](clr-user-defined-aggregate-invoking-functions.md)합니다.  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 자세한 내용은 참조 [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626)합니다.  
  
## <a name="aggregation-methods"></a>집계 메서드  
 사용자 정의 집계로 등록된 클래스는 다음과 같은 인스턴스 메서드를 지원해야 합니다. 쿼리 프로세서는 이러한 메서드를 사용하여 집계를 계산합니다.  
  
|메서드|구문|Description|  
|------------|------------|-----------------|  
|`Init`|public void init ();|쿼리 프로세서는 이 메서드를 사용하여 집계 계산을 초기화합니다. 이 메서드는 쿼리 프로세서가 집계하는 각 그룹에 대해 한 번씩 호출됩니다. 쿼리 프로세서는 여러 그룹의 집계를 계산할 때 집계 클래스의 동일한 인스턴스를 다시 사용할 수 있습니다. `Init` 메서드는 이전에 인스턴스를 사용할 때 필요했던 모든 정리를 수행하고 인스턴스를 사용하여 새 집계 계산을 다시 시작할 수 있도록 만들어야 합니다.|  
|`Accumulate`|public void Accumulate (입력 유형 값 [, 입력 유형 값을]).|함수의 매개 변수를 나타내는 1개 이상의 매개 변수. *input_type* 관리 되는 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 해당 하는 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 지정한 데이터 형식 *input_sqltype* 에 `CREATE AGGREGATE` 문을 합니다. 자세한 내용은 참조 [CLR 매개 변수 데이터 매핑](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)합니다.<br /><br /> UDT(사용자 정의 형식)의 경우 input-type이 UDT 형식과 동일합니다. 쿼리 프로세서는 이 메서드를 사용하여 집계 값을 누적시킵니다. 이 메서드는 집계되는 그룹의 각 값에 대해 한 번씩 호출됩니다. 쿼리 프로세서는 항상 집계 클래스의 지정된 인스턴스에서 `Init` 메서드를 호출한 후에만 이 메서드를 호출합니다. 이 메서드 구현은 전달되는 인수 값의 누적을 반영하도록 인스턴스 상태를 업데이트해야 합니다.|  
|`Merge`|public void 병합 (udagg_class value);|이 메서드를 사용하여 이 집계 클래스의 다른 인스턴스를 현재 인스턴스와 병합할 수 있습니다. 쿼리 프로세서는 이 메서드를 사용하여 집계의 다중 부분 계산을 병합합니다.|  
|`Terminate`|공용 return_type Terminate();|이 메서드는 집계 계산을 완료하고 집계 결과를 반환합니다. *return_type* 관리 되는 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 해당 하는 관리 되는 *return_sqltype* 에 지정 된는 `CREATE AGGREGATE` 문. *return_type* 사용자 정의 형식을 수도 있습니다.|  
  
### <a name="table-valued-parameters"></a>테이블 반환 매개 변수  
 프로시저 또는 함수로 전달되는 사용자 정의 테이블 형식인 TVP(테이블 반환 매개 변수)를 사용하면 여러 개의 데이터 행을 서버로 편리하게 전달할 수 있습니다. TVP는 매개 변수 배열과 유사한 기능을 제공하지만 더 유연하며 [!INCLUDE[tsql](../../includes/tsql-md.md)]과 더 밀접하게 통합됩니다. 또한 성능도 향상될 수 있습니다. TVP는 또한 서버와의 왕복 횟수를 줄이는 데 도움이 될 수 있습니다. 스칼라 매개 변수 목록과 같이 서버로 여러 개의 요청을 보내는 대신 서버에 데이터를 TVP로 보낼 수 있습니다. 사용자 정의 테이블 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 실행 중인 관리되는 저장 프로시저 또는 함수에 테이블 반환 매개 변수로 전달되거나 이러한 저장 프로시저 또는 함수에서 테이블 반환 매개 변수로 반환될 수 없습니다. 또한 컨텍스트 연결의 범위 내에서 TVP를 사용할 수 없습니다. 하지만 컨텍스트 연결이 아닌 연결에 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 실행하는 관리되는 저장 프로시저나 함수에서 SqlClient와 함께 TVP를 사용할 수 있습니다. 이 경우 관리되는 프로시저나 함수를 실행하는 서버와 동일한 서버에 연결될 수 있습니다. Tvp에 대 한 자세한 내용은 참조 [테이블 반환 매개 변수 &#40;데이터베이스 엔진&#41;](../tables/use-table-valued-parameters-database-engine.md)합니다.  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|`Accumulate` 메서드의 설명이 업데이트되어 이제 2개 이상의 매개 변수를 사용합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [CLR 사용자 정의 형식](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 사용자 정의 집계 함수 호출](clr-user-defined-aggregate-invoking-functions.md)  
  
  