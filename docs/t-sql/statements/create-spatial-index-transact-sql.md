---
title: CREATE SPATIAL INDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SPATIAL INDEX
- CREATE SPATIAL INDEX
- CREATE_SPATIAL_INDEX_TSQL
- SPATIAL_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], creating
- index creation [SQL Server], spatial indexes
- CREATE SPATIAL INDEX statement
- CREATE INDEX statement
ms.assetid: ee6b9116-a7ff-463a-a9f0-b360804d8678
caps.latest.revision: 89
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 05e551350da60132741be91d1a9bc22cc0dd7748
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-spatial-index-transact-sql"></a>CREATE SPATIAL INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지정한 테이블 및 열에 공간 인덱스를 만듭니다. 인덱스는 테이블에 데이터를 넣기 전에 만들 수 있습니다. 정규화된 데이터베이스 이름을 지정하여 다른 데이터베이스에 있는 테이블이나 뷰에 인덱스를 만들 수도 있습니다. 공간 인덱스를 사용하려면 클러스터형 기본 키를 포함할 테이블이 필요합니다. 공간 인덱스에 대한 자세한 내용은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- SQL Server Syntax  
  
CREATE SPATIAL INDEX index_name   
  ON <object> ( spatial_column_name )  
    {  
       <geometry_tessellation> | <geography_tessellation>  
    }   
  [ ON { filegroup_name | "default" } ]  
[;]   
  
<object> ::=  
    [ database_name. [ schema_name ] . | schema_name. ]  table_name  
  
<geometry_tessellation> ::=  
{   
  <geometry_automatic_grid_tessellation>   
| <geometry_manual_grid_tessellation>   
}  
  
<geometry_automatic_grid_tessellation> ::=  
{  
    [ USING GEOMETRY_AUTO_GRID ]  
          WITH  (  
        <bounding_box>  
            [ [,] <tessellation_cells_per_object> [ ,…n] ]  
            [ [,] <spatial_index_option> [ ,…n] ]  
                 )  
}  
  
<geometry_manual_grid_tessellation> ::=  
{  
       [ USING GEOMETRY_GRID ]  
         WITH (  
                    <bounding_box>  
                        [ [,]<tessellation_grid> [ ,…n] ]  
                        [ [,]<tessellation_cells_per_object> [ ,…n] ]  
                        [ [,]<spatial_index_option> [ ,…n] ]  
   )  
}   
  
<geography_tessellation> ::=  
{  
      <geography_automatic_grid_tessellation> | <geography_manual_grid_tessellation>  
}  
  
<geography_automatic_grid_tessellation> ::=  
{  
    [ USING GEOGRAPHY_AUTO_GRID ]  
    [ WITH (  
        [ [,] <tessellation_cells_per_object> [ ,…n] ]  
        [ [,] <spatial_index_option> ]  
     ) ]  
}  
  
<geography_manual_grid_tessellation> ::=  
{  
    [ USING GEOGRAPHY_GRID ]  
    [ WITH (  
                [ <tessellation_grid> [ ,…n] ]  
                [ [,] <tessellation_cells_per_object> [ ,…n] ]  
                [ [,] <spatial_index_option> [ ,…n] ]  
                ) ]  
}  
  
<bounding_box> ::=  
{  
      BOUNDING_BOX = ( {  
       xmin, ymin, xmax, ymax   
       | <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>   
  } )  
}  
  
<named_bb_coordinate> ::= { XMIN = xmin | YMIN = ymin | XMAX = xmax | YMAX=ymax }  
  
<tesselation_grid> ::=  
{   
    GRIDS = ( { <grid_level> [ ,...n ] | <grid_size>, <grid_size>, <grid_size>, <grid_size>  }   
        )  
}  
<tesseallation_cells_per_object> ::=  
{   
   CELLS_PER_OBJECT = n   
}  
  
<grid_level> ::=  
{  
     LEVEL_1 = <grid_size>   
  |  LEVEL_2 = <grid_size>   
  |  LEVEL_3 = <grid_size>   
  |  LEVEL_4 = <grid_size>   
}  
  
<grid_size> ::= { LOW | MEDIUM | HIGH }  
  
<spatial_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
    | DATA_COMPRESSION = { NONE | ROW | PAGE }  
}  
  
```  
  
```  
-- Windows Azure SQL Database Syntax   
  
CREATE SPATIAL INDEX index_name   
    ON <object> ( spatial_column_name )   
    {   
      [ USING <geometry_grid_tessellation> ]   
          WITH ( <bounding_box>   
                [ [,] <tesselation_parameters> [,... n ] ]   
                [ [,] <spatial_index_option> [,... n ] ] )   
     | [ USING <geography_grid_tessellation> ]   
          [ WITH ( [ <tesselation_parameters> [,... n ] ]   
                   [ [,] <spatial_index_option> [,... n ] ] ) ]   
    }  
  
[ ; ]  
  
<object> ::=  
{  
    [database_name. [schema_name ] . | schema_name. ]   
                table_name   
}  
  
<geometry_grid_tessellation> ::=   
{ GEOMETRY_GRID }  
  
<bounding_box> ::=   
BOUNDING_BOX = ( {  
        xmin, ymin, xmax, ymax   
   | <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>   
  } )  
  
<named_bb_coordinate> ::= { XMIN = xmin | YMIN = ymin | XMAX = xmax | YMAX=ymax }  
  
<tesselation_parameters> ::=   
{   
    GRIDS = ( { <grid_density> [ ,... n ] | <density>, <density>, <density>, <density>  } )   
  | CELLS_PER_OBJECT = n   
}  
  
<grid_density> ::=   
{  
     LEVEL_1 = <density>   
  |  LEVEL_2 = <density>   
  |  LEVEL_3 = <density>   
  |  LEVEL_4 = <density>   
}  
  
<density> ::= { LOW | MEDIUM | HIGH }  
  
<geography_grid_tessellation> ::=   
{ GEOGRAPHY_GRID }  
  
<spatial_index_option> ::=   
{  
    IGNORE_DUP_KEY = OFF  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF   
}  
  
```  
  
## <a name="arguments"></a>인수  
 *index_name*  
 인덱스의 이름입니다. 인덱스 이름은 테이블에서 고유해야 하지만 데이터베이스 내에서 고유할 필요는 없습니다. 인덱스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.  
  
 ON \<object> ( *spatial_column_name* )  
 인덱스를 만들 개체(데이터베이스, 스키마 또는 테이블) 및 공간 열의 이름을 지정합니다.  
  
 *spatial_column_name*은 인덱스의 기반이 될 공간 열을 지정합니다. 단일 공간 인덱스 정의에서는 하나의 공간 열만 지정할 수 있지만 **geometry** 또는 **geography** 열에서는 여러 개의 공간 인덱스를 만들 수 있습니다.  
  
 USING  
 공간 인덱스에 대한 공간 분할(tessellation) 구성표를 나타냅니다. 이 매개 변수는 다음 표에 있는 형식별 값을 사용합니다.  
  
|열 데이터 형식|공간 분할 구성표|  
|-------------------------|-------------------------|  
|**geometry**|GEOMETRY_GRID|  
|**geometry**|GEOMETRY_AUTO_GRID|  
|**geography**|GEOGRAPY_GRID|  
|**geography**|GEOGRAPHY_AUTO_GRID|  
  
 공간 인덱스는 **기하학** 또는 **지리**유형의 열에서만 만들 수 있습니다. 그렇지 않으면 오류가 발생합니다. 또한 지정된 형식에 잘못된 매개 변수가 전달되어도 오류가 발생합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 공간 분할을 구현하는 방법은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.  
  
 ON *filegroup_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 주어진 파일 그룹에 지정된 인덱스를 만듭니다. 지정된 위치가 없고 테이블이 분할되지 않은 경우 인덱스는 기본 테이블과 동일한 파일 그룹을 사용합니다. 파일 그룹은 이미 존재해야 합니다.  
  
 ON "default"  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 기본 파일 그룹에 지정된 인덱스를 만듭니다.  
  
 이 컨텍스트에서 default는 키워드가 아닙니다. 이것은 기본 파일 그룹에 대한 식별자이며 ON "default" 또는 ON [default]와 같이 구분되어야 합니다. "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
 **\<object>::=**  
  
 인덱싱할 정규화되거나 정규화되지 않은 개체입니다.  
  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이 속한 스키마의 이름입니다.  
  
 *table_name*  
 인덱싱할 테이블 이름입니다.  
  
 database_name이 현재 데이터베이스이거나 database_name이 tempdb이고 object_name이 #으로 시작하는 경우 Microsoft Azure SQL Database는 세 부분으로 구성된 이름 형식 database_name.[schema_name].object_name을 지원합니다.  
  
### <a name="using-options"></a>USING 옵션  
 GEOMETRY_GRID  
 사용하려는 **geometry** 표 공간 분할 구성표를 지정합니다. GEOMETRY_GRID는 **geometry** 데이터 형식의 열에만 지정할 수 있습니다.  GEOMETRY_GRID는 공간 분할 구성표의 수동 조정을 허용합니다.  
  
 GEOMETRY_AUTO_GRID  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 geometry 데이터 형식의 열에만 지정할 수 있습니다. 이 데이터 형식의 기본값이므로 따로 지정할 필요는 없습니다.  
  
 GEOGRAPHY_GRID  
 geography 표 공간 분할 구성표를 지정합니다. GEOGRAPHY_GRID는 **geography** 데이터 형식의 열에만 지정할 수 있습니다.  
  
 GEOGRAPHY_AUTO_GRID  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 geography 데이터 형식의 열에만 지정할 수 있습니다.  이 데이터 형식의 기본값이므로 따로 지정할 필요는 없습니다.  
  
### <a name="with-options"></a>WITH 옵션  
BOUNDING_BOX  
경계 상자의 네 좌표를 정의하는 숫자로 된 네 튜플을 지정합니다. x-min과 y-min은 왼쪽 아래 모퉁이의 좌표를 지정하며 x-max와 y-max는 오른쪽 위 모퉁이의 좌표를 지정합니다.  
  
 *xmin*  
 경계 상자 왼쪽 아래 모퉁이의 X 좌표를 지정합니다.  
  
 *ymin*  
 경계 상자 왼쪽 아래 모퉁이의 Y 좌표를 지정합니다.  
  
 *xmax*  
 경계 상자 오른쪽 위 모퉁이의 X 좌표를 지정합니다.  
  
 *ymax*  
 경계 상자 오른쪽 위 모퉁이의 Y 좌표를 지정합니다.  
  
 XMIN = *xmin*  
 경계 상자 왼쪽 아래 모퉁이의 X 좌표에 대한 속성 이름 및 값을 지정합니다.  
  
 YMIN =*ymin*  
 경계 상자 왼쪽 아래 모퉁이의 Y 좌표에 대한 속성 이름 및 값을 지정합니다.  
  
 XMAX =*xmax*  
 경계 상자 오른쪽 위 모퉁이의 X 좌표에 대한 속성 이름 및 값을 지정합니다.  
  
 YMAX =*ymax*  
 경계 상자 오른쪽 위 모퉁이의 Y 좌표에 대한 속성 이름 및 값을 지정합니다.  
  
 > [!NOTE]
 > 경계 상자 좌표는 USING GEOMETRY_GRID 절 내에서만 적용됩니다.  
 >
 > *xmax*는 *xmin*보다 커야 하고 *ymax*는 *ymin*보다 커야 합니다. *xmax* > *xmin* 및 *ymax* > *ymin*이라고 가정할 때, 모든 유효한 [float](../../t-sql/data-types/float-and-real-transact-sql.md) 값 표현을 지정할 수 있습니다. 그렇지 않으면 해당 오류가 발생합니다.  
 > 
 > 기본값은 없습니다.  
 >
 > 경계 상자 속성 이름은 데이터베이스 데이터 정렬에 관계없이 대/소문자를 구분하지 않습니다.  
  
 속성 이름을 지정하려면 각 항목을 한 번만 지정해야 합니다. 지정하는 순서에는 제한이 없습니다. 예를 들어 다음 절은 동등합니다.  
  
-   BOUNDING_BOX =( XMIN =*xmin*, YMIN =*ymin*, XMAX =*xmax*, YMAX =*ymax* )  
  
-   BOUNDING_BOX =( XMIN =*xmin*, XMAX =*xmax*, YMIN =*ymin*, YMAX =*ymax*)  
  
GRIDS  
공간 분할 구성표의 각 수준에서 표의 밀도를 정의합니다. GEOMETRY_AUTO_GRID and GEOGRAPHY_AUTO_GRID를 선택한 경우에는 이 옵션을 사용할 수 없습니다.  
  
 공간 분할에 대한 자세한 내용은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.  
  
 GRIDS 매개 변수는 다음과 같습니다.  
  
 LEVEL_1  
 첫째 수준(최상위) 표를 지정합니다.  
  
 LEVEL_2  
 둘째 수준 표를 지정합니다.  
  
 LEVEL_3  
 셋째 수준 표를 지정합니다.  
  
 LEVEL_4  
 넷째 수준 표를 지정합니다.  
  
 LOW  
 지정된 수준의 표에 가장 낮은 밀도를 지정합니다. LOW는 16셀(4x4 표)과 같습니다.  
  
 **MEDIUM**  
 지정된 수준의 표에 중간 밀도를 지정합니다. MEDIUM은 64셀(8x8 표)과 같습니다.  
  
 HIGH  
 지정된 수준의 표에 가장 높은 밀도를 지정합니다. HIGH는 256셀(16x16 표)과 같습니다.  
  
> [!NOTE] 
> 수준 이름을 사용하면 순서에 관계없이 수준을 지정하고 수준을 생략할 수 있습니다. 수준에 이름을 사용하면 지정하는 다른 모든 수준에도 이름을 사용해야 합니다. 수준을 생략하면 해당 밀도의 기본값은 MEDIUM이 됩니다.  
  
> [!WARNING] 
> 잘못된 밀도를 지정하면 오류가 발생합니다.  
  
CELLS_PER_OBJECT =*n*  
공간 분할 프로세스에서 인덱스의 단일 공간 개체에 대해 사용할 수 있는 개체당 공간 분할 셀 수를 지정합니다. *n*은 1과 8192(포함) 사이의 정수입니다. 수가 잘못 전달되거나 지정된 공간 분할의 최대 셀 수보다 클 경우 오류가 발생합니다.  
  
 CELLS_PER_OBJECT의 기본값은 다음과 같습니다.  
  
|USING 옵션|개체당 기본 셀|  
|------------------|------------------------------|  
|GEOMETRY_GRID|**16**|  
|GEOMETRY_AUTO_GRID|**8**|  
|GEOGRAPHY_GRID|**16**|  
|GEOGRAPHY_AUTO_GRID|**12**|  
  
 최상위 수준에서, 개체가 *n*으로 지정된 셀보다 많은 셀을 포함하는 경우 인덱싱 시 전체 최상위 수준 공간 분할을 제공하는 데 필요한 만큼의 셀 수를 사용합니다. 이 경우 개체는 지정된 셀 수보다 많은 수의 셀을 받을 수 있습니다. 여기서 최대 수는 최상위 표에 의해 생성된 셀의 수이며 밀도에 따라 달라집니다.  
  
 CELLS_PER_OBJECT 값은 개체당 공간 분할 규칙에서 사용됩니다. 공간 분할 규칙에 대한 자세한 내용은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.  
  
PAD_INDEX = { ON | **OFF** }  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 인덱스 패딩을 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 *fillfactor*로 지정된 사용 가능한 공간의 비율이 인덱스의 중간 수준 페이지에 적용됨을 나타냅니다.  
  
 OFF 또는 *fillfactor*를 지정되지 않음  
 중간 수준 페이지는 중간 페이지의 키 집합을 고려하며 인덱스가 가질 수 있는 최대 크기의 한 행에 필요한 공간을 충분히 남기고 용량을 거의 채움을 나타냅니다.  
  
 PAD_INDEX는 FILLFACTOR에 지정된 비율을 사용하므로 FILLFACTOR가 지정된 경우에만 PAD_INDEX 옵션을 사용할 수 있습니다. FILLFACTOR에 지정된 비율이 한 행을 저장하기에도 부족하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 내부적으로 허용된 최소 비율을 무시합니다. *fillfactor* 값이 아무리 작더라도 중간 인덱스 페이지의 행 수는 두 개 이상입니다.  
  
FILLFACTOR =*fillfactor*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 인덱스를 만들거나 다시 작성할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. *fillfactor*는 1에서 100 사이의 정수 값이어야 하며 기본값은 0입니다. *fillfactor*가 100또는 0이면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 리프 페이지가 꽉 찬 인덱스를 만듭니다.  
  
> [!NOTE]  
>  채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
 FILLFACTOR 설정은 인덱스를 만들거나 다시 작성하는 경우에만 적용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 페이지에 지정된 비율의 빈 공간을 동적으로 유지하지 않습니다. 채우기 비율 설정을 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 사용하세요.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 클러스터형 인덱스를 만들 때 데이터를 다시 배포하므로 FILLFACTOR가 100 미만인 클러스터형 인덱스를 만들면 데이터가 차지하는 저장 공간 크기에 영향을 줍니다.  
  
 자세한 내용은 [인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)을 참조하세요.  
  
SORT_IN_TEMPDB = { ON | **OFF** }  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 tempdb에 임시 정렬 결과를 저장할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 인덱스 작성에 사용된 중간 정렬 결과가 tempdb에 저장됩니다. 이 경우 사용자 데이터베이스가 아닌 다른 디스크 세트에 tempdb가 있으면 인덱스 생성에 필요한 시간이 단축될 수 있습니다. 그러나 인덱스 작성 중에 사용되는 디스크 공간의 크기는 커집니다.  
  
 OFF  
 중간 정렬 결과가 인덱스와 같은 데이터베이스에 저장됩니다.  
  
 사용자 데이터베이스에서 인덱스를 만드는 데 필요한 공간 외에 tempdb에는 중간 정렬 결과를 저장할 정도의 동일한 공간이 추가로 필요합니다. 자세한 내용은 [인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)을 참조하세요.  
  
IGNORE_DUP_KEY =**OFF**  
인덱스 유형은 고유할 수 없으므로 공간 인덱스에 영향을 미치지 않습니다. 이 옵션을 ON으로 설정하지 마세요. ON으로 설정하면 오류가 발생합니다.  
  
STATISTICS_NORECOMPUTE = { ON | **OFF**}  
배포 통계를 다시 계산할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 이전 통계가 자동으로 다시 계산되지 않습니다.  
  
 OFF  
 자동 통계 업데이트가 설정됩니다.  
  
 자동 통계 업데이트를 복원하려면 STATISTICS_NORECOMPUTE를 OFF로 설정하거나 NORECOMPUTE 절 없이 UPDATE STATISTICS를 실행합니다.  
  
> [!IMPORTANT]  
> 배포 통계 자동 재계산 기능을 해제하면 쿼리 최적화 프로그램에서 테이블과 관련된 쿼리에 대해 최적의 실행 계획을 선택할 수 없습니다.  
  
DROP_EXISTING = { ON | **OFF** }  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 명명된 기존 공간 인덱스를 삭제하고 다시 작성하도록 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 기존 인덱스가 삭제되고 다시 작성됩니다. 지정된 인덱스 이름은 현재 존재하는 인덱스 이름과 같아야 합니다. 그러나 인덱스 정의는 수정할 수 있습니다. 예를 들어 다른 열, 정렬 순서, 파티션 구성표 또는 인덱스 옵션을 지정할 수 있습니다.  
  
 OFF  
 지정된 인덱스 이름이 이미 존재하는 경우 오류가 표시됩니다.  
  
 인덱스 유형은 DROP_EXISTING을 사용하여 변경할 수 없습니다.  
  
ONLINE =**OFF**  
인덱스 작업 중에 쿼리 및 데이터 수정에 기본 테이블 및 관련 인덱스를 사용할 수 없도록 지정합니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서는 공간 인덱스에 대해 온라인 인덱스 작성이 지원되지 않습니다. 이 옵션이 공간 인덱스에 대해 ON으로 설정되어 있으면 오류가 발생합니다. ONLINE 옵션을 생략하거나 ONLINE을 OFF로 설정하세요.  
  
 공간 인덱스를 생성, 다시 작성 또는 삭제하는 오프라인 인덱스 작업은 테이블에 대해 SCH-M(스키마 수정) 잠금을 획득합니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다.  
  
> [!NOTE]  
> 온라인 인덱스 작업은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
ALLOW_ROW_LOCKS = { **ON** | OFF }  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 행 잠금이 사용되지 않습니다.  
  
ALLOW_PAGE_LOCKS = { **ON** | OFF }  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 페이지 잠금이 사용되지 않습니다.  
  
MAXDOP =*max_degree_of_parallelism*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 인덱스 작업 중에 `max degree of parallelism` 구성 옵션을 재정의합니다. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
> [!IMPORTANT]  
> MAXDOP 옵션은 구문으로는 지원되지만 현재 CREATE SPATIAL INDEX는 항상 단일 프로세서만 사용합니다.  
  
 *max_degree_of_parallelism*은 다음 중 하나일 수 있습니다.  
  
 1  
 병렬 계획이 생성되지 않습니다.  
  
 \>1  
 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 현재 시스템 작업에 따라 지정된 수 또는 더 적은 수로 제한합니다.  
  
 0(기본값)  
 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]  
> 병렬 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
DATA_COMPRESSION = {NONE | ROW | PAGE}  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 인덱스에 사용되는 데이터 압축 수준을 결정합니다.  
  
 없음  
 인덱스 데이터 압축 안 함  
  
 ROW  
 인덱스 데이터에 행 압축 사용  
  
 PAGE  
 인덱스 데이터에 페이지 압축 사용  
  
## <a name="remarks"></a>Remarks  
 CREATE SPATIAL INDEX 문에는 각 옵션을 한 번씩만 지정할 수 있으며 옵션을 중복 지정하면 오류가 발생합니다.  
  
 테이블의 각 공간 열에는 최대 249개의 공간 인덱스를 만들 수 있습니다. 예를 들어 특정 공간 열에 두 개 이상의 공간 인덱스를 만들면 한 열에 있는 서로 다른 공간 분할 매개 변수를 인덱싱하는 데 유용할 수 있습니다.  
  
> [!IMPORTANT]  
> 이 밖에도 공간 인덱스를 만드는 데는 많은 제한 사항이 있습니다. 자세한 내용은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.  
  
 인덱스 작성 작업은 사용 가능한 프로세스 병렬 처리를 사용할 수 없습니다.  
  
## <a name="methods-supported-on-spatial-indexes"></a>공간 인덱스에서 지원되는 메서드  
 특정 조건에서 공간 인덱스는 여러 집합 지향 geometry 메서드를 지원합니다. 자세한 내용은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.  
  
## <a name="spatial-indexes-and-partitioning"></a>공간 인덱스 및 분할  
 기본적으로 분할된 테이블에 공간 인덱스를 만들면 인덱스가 테이블의 파티션 구성표에 따라 분할됩니다. 이를 통해 인덱스 데이터 및 관련 행이 동일한 파티션에 저장됩니다.  
  
 이 경우 기본 테이블의 파티션 구성표를 변경하려면 공간 인덱스를 삭제한 후 기본 테이블을 재분할해야 합니다. 이러한 제한을 막으려면 공간 인덱스를 만들 때 "ON filegroup" 옵션을 지정하세요. 자세한 내용은 이 항목 다음에 나오는 "공간 인덱스 및 파일 그룹"을 참조하세요.  
  
## <a name="spatial-indexes-and-filegroups"></a>공간 인덱스 및 파일 그룹  
 기본적으로 공간 인덱스는 인덱스가 지정된 테이블과 같은 파일 그룹으로 분할됩니다. 이는 파일 그룹 지정을 통해 다시 정의할 수 있습니다.  
  
 [ ON { *filegroup_name* | "default" } ]  
  
 공간 인덱스의 파일 그룹을 지정하면 인덱스가 테이블의 파티션 구성표에 관계없이 해당 파일 그룹에 생성됩니다.  
  
## <a name="catalog-views-for-spatial-indexes"></a>공간 인덱스의 카탈로그 뷰  
 공간 인덱스와 관련된 카탈로그 뷰는 다음과 같습니다.  
  
 [sys.spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)  
 공간 인덱스의 주요 인덱스 정보를 나타냅니다.  
  
 [sys.spatial_index_tessellations](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)  
 공간 분할 구성표 및 각 공간 인덱스의 매개 변수에 대한 정보를 나타냅니다.  
  
## <a name="additional-remarks-about-creating-indexes"></a>인덱스 작성에 대한 추가 주의 사항  
 인덱스를 작성하는 방법은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)에서 "주의 사항" 섹션을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 사용자에게 테이블 또는 뷰에 대한 ALTER 권한이 있거나 sysadmin 고정 서버 역할, db_ddladmin 및 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-spatial-index-on-a-geometry-column"></a>1. geometry 열에 공간 인덱스 만들기  
 다음 예에서는 **geometry** 형식 열 `geometry_col`을 포함하는 `SpatialTable` 테이블을 만듭니다. 그런 다음 `SIndx_SpatialTable_geometry_col1`에 공간 인덱스 `geometry_col`을 만듭니다. 이 예에서는 기본 공간 분할 구성표를 사용하며 경계 상자를 지정합니다.  
  
```sql  
CREATE TABLE SpatialTable(id int primary key, geometry_col geometry);  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col1   
   ON SpatialTable(geometry_col)  
   WITH ( BOUNDING_BOX = ( 0, 0, 500, 200 ) );  
```  
  
### <a name="b-creating-a-spatial-index-on-a-geometry-column"></a>2. geometry 열에 공간 인덱스 만들기  
 다음 예에서는 `SIndx_SpatialTable_geometry_col2` 테이블의 `geometry_col`에 두 번째 공간 인덱스 `SpatialTable`를 만듭니다. 이 예에서는 `GEOMETRY_GRID`를 공간 분할 구성표로 지정합니다. 또한 경계 상자를 지정하고 표 수준마다 다른 밀도를 지정하며 개체당 64셀을 지정합니다. 인덱스 패딩은 `ON`으로 설정합니다.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col2  
   ON SpatialTable(geometry_col)  
   USING GEOMETRY_GRID  
   WITH (  
    BOUNDING_BOX = ( xmin=0, ymin=0, xmax=500, ymax=200 ),  
    GRIDS = (LOW, LOW, MEDIUM, HIGH),  
    CELLS_PER_OBJECT = 64,  
    PAD_INDEX  = ON );  
```  
  
### <a name="c-creating-a-spatial-index-on-a-geometry-column"></a>3. geometry 열에 공간 인덱스 만들기  
 다음 예에서는 `SIndx_SpatialTable_geometry_col3` 테이블의 `geometry_col`에 세 번째 공간 인덱스 `SpatialTable`을 만듭니다. 이 예에서는 기본 공간 분할 구성표를 사용하며 경계 상자를 지정하고 셋째와 넷째 수준에 다른 셀 밀도를 사용하며 개체당 셀 수로 기본값을 사용합니다.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col3  
   ON SpatialTable(geometry_col)  
   WITH (  
    BOUNDING_BOX = ( 0, 0, 500, 200 ),  
    GRIDS = ( LEVEL_4 = HIGH, LEVEL_3 = MEDIUM ) );  
```  
  
### <a name="d-changing-an-option-that-is-specific-to-spatial-indexes"></a>4. 공간 인덱스와 관련된 옵션 변경  
 다음 예에서는 새 `SIndx_SpatialTable_geography_col3` 밀도를 지정하고 DROP_EXISTING을 ON으로 설정하여 이전 예에서 만든 공간 인덱스 `LEVEL_3`을 다시 작성합니다.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col3  
   ON SpatialTable(geography_col)  
   WITH ( BOUNDING_BOX = ( 0, 0, 500, 200 ),  
        GRIDS = ( LEVEL_3 = LOW ),  
        DROP_EXISTING = ON );  
```  
  
### <a name="e-creating-a-spatial-index-on-a-geography-column"></a>5. geography 열에 공간 인덱스 만들기  
 다음 예에서는 **geography** 형식 열 `geography_col`을 포함하는 `SpatialTable2` 테이블을 만듭니다. 그런 다음 `SIndx_SpatialTable_geography_col1`에 공간 인덱스 `geography_col`을 만듭니다. 이 예에서는 GEOGRAPHY_AUTO_GRID 공간 분할 구성표의 기본 매개 변수 값을 사용합니다.  
  
```sql  
CREATE TABLE SpatialTable2(id int primary key, object GEOGRAPHY);  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col1   
   ON SpatialTable2(object);  
```  
  
> [!NOTE]  
>  geography 표 인덱스에는 경계 상자를 지정할 수 없습니다.  
  
### <a name="f-creating-a-spatial-index-on-a-geography-column"></a>6. geography 열에 공간 인덱스 만들기  
 다음 예에서는 `SIndx_SpatialTable_geography_col2` 테이블의 `geography_col`에 두 번째 공간 인덱스 `SpatialTable2`를 만듭니다. 이 예에서는 `GEOGRAPHY_GRID`를 공간 분할 구성표로 지정합니다. 또한 수준마다 다른 표 밀도를 지정하고 개체당 64셀을 지정합니다. 인덱스 패딩은 `ON`으로 설정합니다.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col2  
   ON SpatialTable2(object)  
   USING GEOGRAPHY_GRID  
   WITH (  
    GRIDS = (MEDIUM, LOW, MEDIUM, HIGH ),  
    CELLS_PER_OBJECT = 64,  
    PAD_INDEX  = ON );  
```  
  
### <a name="g-creating-a-spatial-index-on-a-geography-column"></a>7. geography 열에 공간 인덱스 만들기  
 다음 예에서는 `SIndx_SpatialTable_geography_col3` 테이블의 `geography_col`에 세 번째 공간 인덱스 `SpatialTable2`을 만듭니다. 이 예에서는 기본 공간 분할 구성표인 GEOGRAPHY_GRID와 기본 CELLS_PER_OBJECT 값(16)을 사용합니다.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col3  
   ON SpatialTable2(object)  
   WITH ( GRIDS = ( LEVEL_3 = HIGH, LEVEL_2 = HIGH ) );  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.spatial_index_tessellations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.spatial_indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
