---
title: 행 집합 및 SQL Server 커서 | Microsoft Docs
description: 행 집합 및 SQL Server 커서
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB rowsets, cursors
- OLE DB Driver for SQL Server, rowsets
- rowsets [OLE DB], cursors
- properties [OLE DB]
- cursors [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d14299161a8b0b23448a5e07cdc9f4a335896331
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="rowsets-and-sql-server-cursors"></a>행 집합 및 SQL Server 커서
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 다음 두 가지 방법으로 결과 집합을 소비자에게 반환합니다.  
  
-   다음과 같은 기본 결과 집합  
  
    -   오버헤드를 최소화합니다.  
  
    -   데이터 인출 시 최대 성능을 제공합니다.  
  
    -   정방향 전용, 읽기 전용 기본 커서 기능만 지원합니다.  
  
    -   한 번에 한 행씩 소비자에게 행을 반환합니다.  
  
    -   연결에서 한 번에 하나의 활성 문만 지원합니다.  
  
         문이 실행된 후 소비자가 모든 결과를 검색하거나 문이 취소될 때까지 해당 연결에서 다른 문을 실행할 수 없습니다.  
  
    -   모든 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 지원합니다.  
  
-   다음과 같은 서버 커서  
  
    -   모든 커서 기능을 지원합니다.  
  
    -   소비자에게 행 블록을 반환할 수 있습니다.  
  
    -   단일 연결에서 여러 개의 활성 문을 지원합니다.  
  
    -   커서 기능과 성능의 균형을 조정합니다.  
  
         커서 기능을 지원하면 기본 결과 집합과 비교해서 성능이 저하될 수 있습니다. 소비자가 커서 기능을 사용하여 더 작은 행 집합을 검색할 수 있는 경우 이러한 성능 저하를 상쇄할 수 있습니다.  
  
    -   결과 집합을 두 개 이상 반환하는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 지원하지 않습니다.  
  
 소비자는 특정 행 집합 속성을 설정하여 행 집합에 다른 커서 동작을 요청할 수 있습니다. 소비자 중 하나라도 이러한 행 집합 속성을 설정 하지 않으면 않거나 모두 기본값으로 설정는 OLE DB Driver for SQL Server 기본 결과 집합을 사용 하 여 행 집합을 구현 합니다. 이러한 속성 중 하나라도 기본값 이외의 값으로 설정 된 OLE DB Driver for SQL Server 서버 커서를 사용 하 여 행 집합을 구현 합니다.  
  
 다음 행 집합 속성의 OLE DB 드라이버를 사용 하도록 SQL Server를 직접 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서입니다. 일부 속성은 다른 속성과 안전하게 조합할 수 있습니다. 예를 들어 DBPROP_IRowsetScroll 및 DBPROP_IRowsetChange 속성을 나타내는 행 집합은 즉시 업데이트 동작을 표시하는 책갈피 행 집합이 됩니다. 다른 속성은 함께 사용할 수 없습니다. 예를 들어 DBPROP_OTHERINSERT를 나타내는 행 집합은 책갈피를 포함할 수 없습니다.  
  
|속성 ID|Value|행 집합 동작|  
|-----------------|-----------|---------------------|  
|DBPROP_SERVERCURSOR|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 순차적이며 정방향으로만 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_CANSCROLLBACKWARDS 또는 DBPROP_CANFETCHBACKWARDS|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_BOOKMARKS 또는 DBPROP_LITERALBOOKMARKS|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 순차적이며 정방향으로만 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_OWNUPDATEDELETE, DBPROP_OWNINSERT 또는 DBPROP_OTHERUPDATEDELETE|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_OTHERINSERT|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 참조된 열에 인덱스가 있으면 명령 텍스트에 ORDER BY 절이 포함될 수 있습니다.<br /><br /> 행 집합에 책갈피가 포함되어 있으면 DBPROP_OTHERINSERT는 VARIANT_TRUE일 수 없습니다. 이 표시 유형 속성과 책갈피를 사용하여 행 집합을 만들려고 하면 오류가 발생합니다.|  
|DBPROP_IRowsetLocate 또는 DBPROP_IRowsetScroll|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. 책갈피와 절대 위치를 통해는 **IRowsetLocate** 인터페이스 행 집합에서 지원 됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.<br /><br /> DBPROP_IRowsetLocate 및 DBPROP_IRowsetScroll은 행 집합에 책갈피가 필요합니다. VARIANT_TRUE로 설정된 DBPROP_OTHERINSERT와 책갈피를 사용하여 행 집합을 만들려고 하면 오류가 발생합니다.|  
|DBPROP_IRowsetChange 또는 DBPROP_IRowsetUpdate|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 있습니다. 행 집합은 순차적이며 정방향으로만 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 업데이트 가능한 커서를 지원하는 모든 명령은 이러한 인터페이스를 지원할 수 있습니다.|  
|DBPROP_IRowsetLocate 또는 DBPROP_IRowsetScroll 및 DBPROP_IRowsetChange 또는 DBPROP_IRowsetUpdate|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 있습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. 책갈피와 절대 위치를 통해 **IRowsetLocate** 행 집합에서 지원 됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_IMMOBILEROWS|VARIANT_FALSE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 정방향 스크롤만 지원합니다. 상대적인 행 위치 지정은 지원됩니다. 참조된 열에 인덱스가 있으면 명령 텍스트에 ORDER BY 절이 포함될 수 있습니다.<br /><br /> DBPROP_IMMOBILEROWS는 다른 세션의 명령이나 다른 사용자에 의해 삽입된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 행을 표시할 수 있는 행 집합에서만 사용할 수 있습니다. DBPROP_OTHERINSERT가 VARIANT_TRUE일 수 없는 행 집합에서 속성이 VARIANT_FALSE로 설정된 행 집합을 열려고 하면 오류가 발생합니다.|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 정방향 스크롤만 지원합니다. 상대적인 행 위치 지정은 지원됩니다. 다른 속성으로 제한되지 않은 경우 명령 텍스트에 ORDER BY 절이 포함될 수 있습니다.|  
  
 OLE DB 드라이버는 서버 커서에서 지 원하는 SQL Server 행 집합을 쉽게 만들 수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본 테이블 또는 뷰를 사용 하 여는 **iopenrowset:: Openrowset** 메서드. 필요한 행 집합을 전달 속성 설정, 테이블 또는 뷰 이름으로 지정 된 *rgPropertySets* 매개 변수입니다.  
  
 행 집합이 서버 커서에서 지원되도록 소비자가 요구하는 경우 행 집합을 만드는 명령 텍스트가 제한됩니다. 구체적으로, 명령 텍스트는 단일 행 집합 결과를 반환하는 단일 SELECT 문이나 단일 행 집합 결과를 반환하는 단일 SELECT 문을 구현하는 저장 프로시저로 제한됩니다.  
  
 두 테이블에서는 다양한 OLE DB 속성과 커서 모델의 매핑을 보여 줍니다. 또한 특정 유형의 커서 모델을 사용하도록 설정해야 하는 행 집합 속성을 표시합니다.  
  
 테이블의 각 셀에는 특정 커서 모델에 대한 행 집합 속성 값이 포함됩니다. 이 항목의 앞부분에 표시된 모든 행 집합 속성의 데이터 형식은 VT_BOOL이고 기본값은 VARIANT_FALSE입니다. 표에서 사용되는 기호는 다음과 같습니다.  
  
 F = 기본값(VARIANT_FALSE)  
  
 T = VARIANT_TRUE  
  
 \- = VARIANT_TRUE 또는 VARIANT_FALSE  
  
 특정 유형의 커서 모델을 사용하려면 커서 모델에 해당하는 열을 찾아 열에 값 'T'가 포함된 행 집합 속성을 모두 찾습니다. 특정 커서 모델을 사용하려면 이러한 행 집합 속성을 VARIANT_TRUE로 설정합니다. 값이 '-'인 행 집합 속성은 VARIANT_TRUE 또는 VARIANT_FALSE로 설정할 수 있습니다.  
  
|행 집합 속성/커서 모델|기본값<br /><br /> result<br /><br /> 집합<br /><br /> (RO)|빠름<br /><br /> 정방향<br /><br /> 전용<br /><br /> (RO)|정적<br /><br /> (RO)|Keyset<br /><br /> 집합<br /><br /> (RO)|  
|--------------------------------------|-------------------------------------------|--------------------------------------------|-----------------------|----------------------------------|  
|DBPROP_SERVERCURSOR|F|T|T|T|  
|DBPROP_DEFERRED|F|F|-|-|  
|DBPROP_IrowsetChange|F|F|F|F|  
|DBPROP_IrowsetLocate|F|F|-|-|  
|DBPROP_IrowsetScroll|F|F|-|-|  
|DBPROP_IrowsetUpdate|F|F|F|F|  
|DBPROP_BOOKMARKS|F|F|-|-|  
|DBPROP_CANFETCHBACKWARDS|F|F|-|-|  
|DBPROP_CANSRCOLLBACKWARDS|F|F|-|-|  
|DBPROP_CANHOLDROWS|F|F|-|-|  
|DBPROP_LITERALBOOKMARKS|F|F|-|-|  
|DBPROP_OTHERINSERT|F|T|F|F|  
|DBPROP_OTHERUPDATEDELETE|F|T|F|T|  
|DBPROP_OWNINSERT|F|T|F|T|  
|DBPROP_OWNUPDATEDELETE|F|T|F|T|  
|DBPROP_QUICKSTART|F|F|-|-|  
|DBPROP_REMOVEDELETED|F|F|F|-|  
|DBPROP_IrowsetResynch|F|F|F|-|  
|DBPROP_CHANGEINSERTEDROWS|F|F|F|F|  
|DBPROP_SERVERDATAONINSERT|F|F|F|-|  
|DBPROP_UNIQUEROWS|-|F|F|F|  
|DBPROP_IMMOBILEROWS|-|-|-|T|  
  
|행 집합 속성/커서 모델|동적(RO)|키 집합(R/W)|동적(R/W)|  
|--------------------------------------|--------------------|---------------------|----------------------|  
|DBPROP_SERVERCURSOR|T|T|T|  
|DBPROP_DEFERRED|-|-|-|  
|DBPROP_IrowsetChange|F|-|-|  
|DBPROP_IrowsetLocate|F|-|F|  
|DBPROP_IrowsetScroll|F|-|F|  
|DBPROP_IrowsetUpdate|F|-|-|  
|DBPROP_BOOKMARKS|F|-|F|  
|DBPROP_CANFETCHBACKWARDS|-|-|-|  
|DBPROP_CANSRCOLLBACKWARDS|-|-|-|  
|DBPROP_CANHOLDROWS|F|-|F|  
|DBPROP_LITERALBOOKMARKS|F|-|F|  
|DBPROP_OTHERINSERT|T|F|T|  
|DBPROP_OTHERUPDATEDELETE|T|T|T|  
|DBPROP_OWNINSERT|T|T|T|  
|DBPROP_OWNUPDATEDELETE|T|T|T|  
|DBPROP_QUICKSTART|-|-|-|  
|DBPROP_REMOVEDELETED|T|-|T|  
|DBPROP_IrowsetResynch|-|-|-|  
|DBPROP_CHANGEINSERTEDROWS|F|-|F|  
|DBPROP_SERVERDATAONINSERT|F|-|F|  
|DBPROP_UNIQUEROWS|F|F|F|  
|DBPROP_IMMOBILEROWS|F|T|F|  
  
 특정 행 집합 속성 집합의 경우 선택되는 커서 모델은 다음과 같이 결정됩니다.  
  
 지정한 행 집합 속성 컬렉션에서 앞의 표에 나열된 속성의 하위 집합을 가져옵니다. 각 행 집합 속성의 플래그 값(필수(T, F) 또는 옵션(-))에 따라 이러한 속성을 두 개의 하위 그룹으로 나눕니다. 각 커서 모델에 대해 첫 번째 표에서 시작하여 왼쪽에서 오른쪽으로 이동합니다. 두 하위 그룹의 속성 값을 이 열의 해당 속성 값과 비교합니다. 필수 속성과 불일치하는 항목이 없고 옵션 속성과 불일치하는 항목 수가 최소인 커서 모델이 선택됩니다. 커서 모델이 두 개 이상 있으면 가장 왼쪽의 항목이 선택됩니다.  
  
## <a name="sql-server-cursor-block-size"></a>SQL Server 커서 블록 크기  
 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서가 SQL Server 행 집합에 대 한 OLE DB 드라이버 지원의 배열 매개 변수를 처리 하는 행에 있는 요소의 수는 **irowset:: Getnextrows** 또는 **irowsetlocate:: Getrowsat** 메서드는 커서 블록 크기를 정의 합니다. 배열의 핸들로 표시된 행이 커서 블록의 멤버입니다.  
  
 책갈피를 지 원하는 행 집합을 사용 하 여 검색 된 행 핸들이 **irowsetlocate:: Getrowsbybookmark** 메서드 커서 블록의 멤버를 정의 합니다.  
  
 행 집합을 채우고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서 블록을 형성하는 데 사용된 메서드에 관계없이 커서 블록은 행 집합에 대해 다음 행 인출 메서드를 실행할 때까지 활성화되어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
