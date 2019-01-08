---
title: 행 집합 및 SQL Server 커서 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB rowsets, cursors
- SQL Server Native Client OLE DB provider, rowsets
- rowsets [OLE DB], cursors
- properties [OLE DB]
- cursors [OLE DB]
ms.assetid: 26a11e26-2a3a-451e-8f78-fba51e330ecb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d87706d53190552734785b5310cba7ec81056a40
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535451"
---
# <a name="rowsets-and-sql-server-cursors"></a>행 집합 및 SQL Server 커서
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다음 두 가지 방법으로 결과 집합을 소비자에게 반환합니다.  
  
-   다음과 같은 기본 결과 집합  
  
    -   오버헤드를 최소화합니다.  
  
    -   데이터 인출 시 최대 성능을 제공합니다.  
  
    -   정방향 전용, 읽기 전용 기본 커서 기능만 지원합니다.  
  
    -   한 번에 한 행씩 소비자에게 행을 반환합니다.  
  
    -   연결에서 한 번에 하나의 활성 문만 지원합니다.  
  
         문이 실행된 후 소비자가 모든 결과를 검색하거나 문이 취소될 때까지 해당 연결에서 다른 문을 실행할 수 없습니다.  
  
    -   모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지원합니다.  
  
-   다음과 같은 서버 커서  
  
    -   모든 커서 기능을 지원합니다.  
  
    -   소비자에게 행 블록을 반환할 수 있습니다.  
  
    -   단일 연결에서 여러 개의 활성 문을 지원합니다.  
  
    -   커서 기능과 성능의 균형을 조정합니다.  
  
         커서 기능을 지원하면 기본 결과 집합과 비교해서 성능이 저하될 수 있습니다. 소비자가 커서 기능을 사용하여 더 작은 행 집합을 검색할 수 있는 경우 이러한 성능 저하를 상쇄할 수 있습니다.  
  
    -   결과 집합을 두 개 이상 반환하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지원하지 않습니다.  
  
 소비자는 특정 행 집합 속성을 설정하여 행 집합에 다른 커서 동작을 요청할 수 있습니다. 소비자가 이러한 행 집합 속성 중 하나를 설정 하지 않거나 모두 해당 기본값으로 설정 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 기본 결과 집합을 사용 하 여 행 집합을 구현 합니다. 이러한 속성 중 하나라도 기본값이 아닌 값으로 설정 된 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 서버 커서를 사용 하 여 행 집합을 구현 합니다.  
  
 다음과 같은 행 집합 속성을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서를 사용합니다. 일부 속성은 다른 속성과 안전하게 조합할 수 있습니다. 예를 들어 DBPROP_IRowsetScroll 및 DBPROP_IRowsetChange 속성을 나타내는 행 집합은 즉시 업데이트 동작을 표시하는 책갈피 행 집합이 됩니다. 다른 속성은 함께 사용할 수 없습니다. 예를 들어 DBPROP_OTHERINSERT를 나타내는 행 집합은 책갈피를 포함할 수 없습니다.  
  
|속성 ID|값|행 집합 동작|  
|-----------------|-----------|---------------------|  
|DBPROP_SERVERCURSOR|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 순차적이며 정방향으로만 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_CANSCROLLBACKWARDS 또는 DBPROP_CANFETCHBACKWARDS|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_BOOKMARKS 또는 DBPROP_LITERALBOOKMARKS|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 순차적이며 정방향으로만 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_OWNUPDATEDELETE, DBPROP_OWNINSERT 또는 DBPROP_OTHERUPDATEDELETE|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_OTHERINSERT|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 참조된 열에 인덱스가 있으면 명령 텍스트에 ORDER BY 절이 포함될 수 있습니다.<br /><br /> 행 집합에 책갈피가 포함되어 있으면 DBPROP_OTHERINSERT는 VARIANT_TRUE일 수 없습니다. 이 표시 유형 속성과 책갈피를 사용하여 행 집합을 만들려고 하면 오류가 발생합니다.|  
|DBPROP_IRowsetLocate 또는 DBPROP_IRowsetScroll|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. **IRowsetLocate** 인터페이스를 통한 책갈피 및 절대 위치 지정이 행 집합에서 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.<br /><br /> DBPROP_IRowsetLocate 및 DBPROP_IRowsetScroll은 행 집합에 책갈피가 필요합니다. VARIANT_TRUE로 설정된 DBPROP_OTHERINSERT와 책갈피를 사용하여 행 집합을 만들려고 하면 오류가 발생합니다.|  
|DBPROP_IRowsetChange 또는 DBPROP_IRowsetUpdate|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 있습니다. 행 집합은 순차적이며 정방향으로만 스크롤하거나 인출할 수 있습니다. 상대적인 행 위치 지정은 지원됩니다. 업데이트 가능한 커서를 지원하는 모든 명령은 이러한 인터페이스를 지원할 수 있습니다.|  
|DBPROP_IRowsetLocate 또는 DBPROP_IRowsetScroll 및 DBPROP_IRowsetChange 또는 DBPROP_IRowsetUpdate|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 있습니다. 행 집합은 어느 방향으로든 스크롤하거나 인출할 수 있습니다. **IRowsetLocate**를 통한 책갈피 및 절대 위치 지정이 행 집합에서 지원됩니다. 명령 텍스트에는 ORDER BY 절이 포함될 수 있습니다.|  
|DBPROP_IMMOBILEROWS|VARIANT_FALSE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 정방향 스크롤만 지원합니다. 상대적인 행 위치 지정은 지원됩니다. 참조된 열에 인덱스가 있으면 명령 텍스트에 ORDER BY 절이 포함될 수 있습니다.<br /><br /> DBPROP_IMMOBILEROWS는 다른 세션의 명령이나 다른 사용자에 의해 삽입된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 행을 표시할 수 있는 행 집합에서만 사용할 수 있습니다. DBPROP_OTHERINSERT가 VARIANT_TRUE일 수 없는 행 집합에서 속성이 VARIANT_FALSE로 설정된 행 집합을 열려고 하면 오류가 발생합니다.|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|행 집합을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 업데이트할 수 없습니다. 행 집합은 정방향 스크롤만 지원합니다. 상대적인 행 위치 지정은 지원됩니다. 다른 속성으로 제한되지 않은 경우 명령 텍스트에 ORDER BY 절이 포함될 수 있습니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 서버 커서에서 지원 되는 Native Client OLE DB 공급자 행 집합을 쉽게 만들 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 테이블 또는 뷰를 사용 하 여 합니다 **iopenrowset:: Openrowset** 메서드. *rgPropertySets* 매개 변수에 필요한 행 집합 속성 세트를 전달하여 이름으로 테이블이나 뷰를 지정합니다.  
  
 행 집합이 서버 커서에서 지원되도록 소비자가 요구하는 경우 행 집합을 만드는 명령 텍스트가 제한됩니다. 구체적으로, 명령 텍스트는 단일 행 집합 결과를 반환하는 단일 SELECT 문이나 단일 행 집합 결과를 반환하는 단일 SELECT 문을 구현하는 저장 프로시저로 제한됩니다.  
  
 두 테이블에서는 다양한 OLE DB 속성과 커서 모델의 매핑을 보여 줍니다. 또한 특정 유형의 커서 모델을 사용하도록 설정해야 하는 행 집합 속성을 표시합니다.  
  
 테이블의 각 셀에는 특정 커서 모델에 대한 행 집합 속성 값이 포함됩니다. 이 항목의 앞부분에 표시된 모든 행 집합 속성의 데이터 형식은 VT_BOOL이고 기본값은 VARIANT_FALSE입니다. 표에서 사용되는 기호는 다음과 같습니다.  
  
 F = 기본값(VARIANT_FALSE)  
  
 T = VARIANT_TRUE  
  
 \- = VARIANT_TRUE 또는 VARIANT_FALSE  
  
 특정 유형의 커서 모델을 사용하려면 커서 모델에 해당하는 열을 찾아 열에 값 'T'가 포함된 행 집합 속성을 모두 찾습니다. 특정 커서 모델을 사용하려면 이러한 행 집합 속성을 VARIANT_TRUE로 설정합니다. 값이 '-'인 행 집합 속성은 VARIANT_TRUE 또는 VARIANT_FALSE로 설정할 수 있습니다.  
  
|행 집합 속성/커서 모델|Default<br /><br /> result<br /><br /> 집합<br /><br /> (RO)|빠름<br /><br /> 정방향<br /><br /> 전용<br /><br /> (RO)|정적<br /><br /> (RO)|Keyset<br /><br /> 집합<br /><br /> (RO)|  
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
 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서가 지원를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 행 집합 행의 요소 수가 핸들의 배열 매개 변수에 **irowset:: Getnextrows** 또는 **irowsetlocate:: Getrowsat**  메서드 커서 블록 크기를 정의 합니다. 배열의 핸들로 표시된 행이 커서 블록의 멤버입니다.  
  
 책갈피를 지원하는 행 집합의 경우 **IRowsetLocate::GetRowsByBookmark** 메서드를 사용하여 검색된 행 핸들이 커서 블록의 멤버를 정의합니다.  
  
 행 집합을 채우고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서 블록을 형성하는 데 사용된 메서드에 관계없이 커서 블록은 행 집합에 대해 다음 행 인출 메서드를 실행할 때까지 활성화되어 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [행 집합](rowsets.md)  
  
  
