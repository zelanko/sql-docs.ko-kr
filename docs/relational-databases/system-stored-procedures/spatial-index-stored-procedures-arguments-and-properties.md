---
description: 공간 인덱스 저장 프로시저의 인수 및 속성
title: 공간 인덱스 저장 프로시저의 인수 및 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], stored procedures
ms.assetid: ee26082b-c0ed-40ff-b5ad-f5f6b00f0475
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 840668495c620ca3cb7a403d3775238b12a52ec8
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809729"
---
# <a name="spatial-index-stored-procedures---arguments-and-properties"></a>공간 인덱스 저장 프로시저-인수 및 속성
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 공간 인덱스 저장 프로시저의 인수와 속성에 대해 설명합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
 특정 공간 인덱스 저장 프로시저의 구문은 다음 항목을 참조하십시오.  
  
-   [Transact-sql&#41;sp_help_spatial_geometry_index &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [Transact-sql&#41;sp_help_spatial_geometry_index_xml &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [Transact-sql&#41;sp_help_spatial_geography_index &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [Transact-sql&#41;sp_help_spatial_geography_index_xml &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="arguments"></a>인수  
`[ @tabname = ] 'tabname'` 공간 인덱스가 지정 된 테이블의 정규화 된 이름 또는 정규화 되지 않은 이름입니다.  
  
 따옴표는 정규화된 테이블이 지정된 경우에만 필요합니다. 데이터베이스 이름을 포함한 정규화된 이름인 경우 반드시 현재 데이터베이스의 이름을 사용해야 합니다. *tabname* 은 **nvarchar**(776) 이며 기본값은 없습니다.  
  
`[ @indexname = ] 'indexname'` 지정 된 공간 인덱스의 이름입니다. *indexname* 는 **sysname** 이며 기본값은 없습니다.  
  
`[ @verboseoutput = ] 'verboseoutput'` 반환 될 속성 이름 및 값의 범위입니다.  
  
 0 = 핵심 속성  
  
 \>0 = 모든 속성  
  
 *verboseoutput* 은 **tinyint** 이며 기본값은 없습니다.  
  
`[ @query_sample = ] 'query_sample'` 는 인덱스의 유용성을 테스트 하는 데 사용할 수 있는 대표적인 쿼리 샘플입니다. 대표 개체 또는 쿼리 창일 수 있습니다. *query_sample* 은 **geometry** 이며 기본값은 없습니다.  
  
`[ @xml_output = ] 'xml_output'` 는 XML 조각에서 결과 집합을 반환 하는 출력 매개 변수입니다. *xml_output* 은 **xml** 이며 기본값은 없습니다.  
  
## <a name="properties"></a>속성  
 아래 표에 표시 된 것 처럼 ** \@ verboseoutput** = 0을 설정 하 여 핵심 속성을 반환 합니다. ** \@ verboseoutput** 는 0을 > 하 여 공간 인덱스의 모든 속성을 반환 합니다.  
  
 **Base_Table_Rows**  
 기본 테이블에 있는 행의 수입니다. 값이 **bigint**입니다.  
  
 **Bounding_Box_xmin**  
 **Geometry** 형식에 대 한 공간 인덱스의 X 최소 경계 상자 속성입니다. **Geography**유형에 대해서는이 속성 값이 NULL입니다. 값이 **float**입니다.  
  
 **Bounding_Box_ymin**  
 **Geometry** 형식에 대 한 공간 인덱스의 Y 최소 경계 상자 속성입니다. **Geography** 유형에 대해서는이 속성 값이 NULL입니다. 값이 **float**입니다.  
  
 **Bounding_Box_xmax**  
 **Geometry** 형식에 대 한 공간 인덱스의 X 최대 경계 상자 속성입니다. **Geography** 유형에 대해서는이 속성 값이 NULL입니다. 값이 **float**입니다.  
  
 **Bounding_Box_ymax**  
 **Geometry** 형식에 대 한 공간 인덱스의 Y 최대 경계 상자 속성입니다. **Geography** 유형에 대해서는이 속성 값이 NULL입니다. 값이 **float**입니다.  
  
 **Grid_Size_Level_1**  
 공간 인덱스의 수준 1 표 밀도입니다.  
  
 16(LOW)  
  
 64(MEDIUM)  
  
 256(HIGH)  
  
 값은 **int**입니다.  
  
 **Grid_Size_Level_2**  
 공간 인덱스의 수준 2 표 밀도입니다.  
  
 16(LOW)  
  
 64(MEDIUM)  
  
 256(HIGH)  
  
 값은 **int**입니다.  
  
 **Grid_Size_Level_3**  
 공간 인덱스의 수준 3 표 밀도입니다.  
  
 16(LOW)  
  
 64(MEDIUM)  
  
 256(HIGH)  
  
 값은 **int**입니다.  
  
 **Grid_Size_Level_4**  
 공간 인덱스의 수준 4 표 밀도입니다.  
  
 16(LOW)  
  
 64(MEDIUM)  
  
 256(HIGH)  
  
 값은 **int**입니다.  
  
 **Cells_Per_Object**  
 개체당 셀 수입니다(인덱스 속성). 값은 **int**입니다.  
  
 **Total_Primary_Index_Rows**  
 인덱스의 행 수입니다. 값이 **bigint**입니다.  
  
 **Total_Primary_Index_Pages**  
 인덱스의 페이지 수입니다. 값이 **bigint**입니다.  
  
 **Average_Number_Of_Index_Rows_Per_Base_Row**  
 인덱스 행의 수 / 기본 테이블 행의 수입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**  
 대표 쿼리 샘플이 **기 하 도형** 인덱스의 경계 상자를 벗어나 루트 셀 (수준 0 셀)에 속하는지 여부를 나타냅니다. 0(수준 0 셀에 없음) 또는 1입니다. 수준 0 셀에 있는 경우 조사된 인덱스는 쿼리 샘플에 적합한 인덱스가 아닙니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_ObjectCells_In_Level0_In_Index**  
 수준 0 ( **기 하 도형**에 대 한 경계 상자 외부의 공간 분할)에 있는 인덱싱된 개체의 셀 인스턴스 수입니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **기 하 도형** 인덱스의 경우 인덱스의 경계 상자가 데이터 도메인 보다 작은 경우 발생 합니다. 수준 0의 개체 수가 많으면 쿼리 창이 경계 상자를 부분적으로 벗어날 때 보조 필터가 필요할 수 있으며 인덱스 성능이 저하 됩니다 (예: **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample** 1). 쿼리 창이 경계 상자 안쪽에 있으면 수준 0의 개체 수가 많은 경우 인덱스의 성능이 향상될 수 있습니다.  
  
 NULL 및 빈 인스턴스는 수준 0에서 계산되지만 성능에 영향을 주지는 않습니다. 수준 0의 셀 수는 기본 테이블에 있는 NULL 인스턴스 및 빈 인스턴스의 수와 동일합니다. **지리** 인덱스의 경우 쿼리 샘플은 1로 계산 되므로 수준 0은 NULL과 빈 인스턴스 + 1 셀의 셀을 포함 합니다.  
  
 **Total_Number_Of_ObjectCells_In_Level1_In_Index**  
 수준 1 정밀도로 공간 분할 인덱싱된 개체의 셀 인스턴스 수입니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_ObjectCells_In_Level2_In_Index**  
 수준 2 정밀도로 공간 분할 인덱싱된 개체의 셀 인스턴스 수입니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_ObjectCells_In_Level3_In_Index**  
 수준 3 정밀도로 공간 분할 인덱싱된 개체의 셀 인스턴스 수입니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_ObjectCells_In_Level4_In_Index**  
 수준 4 정밀도로 공간 분할된 인덱싱된 개체의 셀 인스턴스 수입니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level1_In_Index**  
 공간 분할 수준 1에서 개체가 완전히 검사 하 여 개체의 내부에 있는 셀의 수입니다. (Cell_attributevalue은 2입니다.) 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level2_In_Index**  
 공간 분할 수준 2에서 개체가 완전히 검사 되므로 개체의 내부에 있는 셀의 수입니다. Cell_attribute 값은 2입니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level3_In_Index**  
 공간 분할 수준 3에서 개체에 의해 완전히 포함 되는 셀의 수 이므로 개체의 내부입니다. Cell_attribute 값은 2입니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level4_In_Index**  
 공간 분할 수준 4에서 하나의 개체에 완전히 포함되어 이 개체의 내부에 있는 셀의 수입니다. Cell_attribute 값은 2입니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level1_In_Index**  
 공간 분할 수준 1에서 개체와 교차 하는 셀 수입니다. Cell_attribute 값은 1입니다. 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level2_In_Index**  
 공간 분할 수준 2에서 개체와 교차 하는 셀 수입니다. Cell_attribute 값은 1입니다. 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level3_In_Index**  
 공간 분할 수준 3에서 개체와 교차 하는 셀 수입니다. Cell_attribute 값은 1입니다. 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level4_In_Index**  
 공간 분할 수준 4에서 개체와 교차되는 셀의 수입니다. Cell_attribute 값은 1입니다. 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_For_QuerySample**  
 쿼리 샘플이 경계 상자를 벗어나되 이에 접해 있는 루트 셀 0에 있는지 여부를 나타냅니다. 이 속성은 핵심 속성입니다. 값이 **bigint**입니다.  
  
> [!NOTE]  
>  이 정보는 경계 상자에서 미세한 차이로 누락된 개체가 있는지 여부를 확인하는 경우에만 사용됩니다.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_In_Index**  
 경계 상자에 접한 수준 0에 있는 개체의 수입니다. Cell_attribute 값은 0입니다.  값이 **bigint**입니다.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level1_In_Index**  
 공간 분할 수준 1에서 표 셀 경계를 터치 하는 개체 셀의 수입니다. Cell_attribute 값은 0입니다. 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level2_In_Index**  
 공간 분할 수준 2에서 표 셀 경계를 터치 하는 개체 셀의 수입니다. Cell_attribute 값은 0입니다. 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level3_In_Index**  
 공간 분할 수준 3에서 표 셀 경계를 터치 하는 개체 셀의 수입니다. Cell_attribute 값은 0입니다. 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level4_In_Index**  
 공간 분할 수준 4에서 표 셀 경계에 접한 개체 셀의 수입니다. Cell_attribute 값은 0입니다. 핵심 속성입니다. 값이 **bigint**입니다.  
  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 하나의 개체에 포함된 리프 셀을 포함하는 표의 전체 영역(전체 리프 셀) 비율입니다.  
  
 예를 들어 하나의 개체가 총 100개의 리프 셀에 해당하는 영역을 포함하는 4개의 표 수준에서 10개의 셀로 공간 분할되는 경우가 있습니다. 이 개체에 완전히 포함되는 내부 셀이 3개 있다고 가정할 때 3개의 내부 셀에 포함되는 영역은 42개의 리프 셀에 해당합니다. 따라서 포함된 영역의 비율은 42%입니다. 이 수치는 인덱스의 개체가 얼마나 단편화되어 있는지 알 수 있는 유용한 척도입니다.  
  
 값이 **float**입니다.  
  
 **Intersecting_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 부분적으로 검사 된 셀 이라는 점을 제외 하 고 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**와 동일 합니다. 값이 **float**입니다.  
  
 **Border_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 테두리 셀 이라는 점을 제외 하 고 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage** 와 동일 합니다. 값이 **float**입니다.  
  
 **Average_Cells_Per_Object_Normalized_To_Leaf_Grid**  
 리프 표를 기준으로 평균화되는 개체당 평균 셀입니다. 이 값은 개체의 공간적 크기, 또는 개체가 얼마나 큰지에 대한 지표를 제공합니다. 값이 **float**입니다.  
  
 **Average_Objects_PerLeaf_GridCell**  
 인덱스의 분포도입니다. 리프 셀당 평균 개체의 수입니다. 값이 **float**입니다.  
  
 **Number_Of_SRIDs_Found**  
 인덱스와 열의 고유 SRID 수입니다. 값은 **int**입니다.  
  
 하나의 열에는 두 개 이상의 SRID가 포함될 수 있고 SRID가 서로 다른 개체는 교차되지 않으므로 SRID의 수는 인덱스의 선택도를 나타냅니다.  
  
 **Width_Of_Cell_In_Level1**  
 인덱싱 표에 있는 셀의 Width 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Width_Of_Cell_In_Level2**  
 인덱싱 표에 있는 셀의 Width 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Width_Of_Cell_In_Level3**  
 인덱싱 표에 있는 셀의 Width 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Width_Of_Cell_In_Level4**  
 인덱싱 표에 있는 셀의 Width 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Height_Of_Cell_In_Level1**  
 인덱싱 표에 있는 셀의 Height 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Height_Of_Cell_In_Level2**  
 인덱싱 표에 있는 셀의 Height 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Height_Of_Cell_In_Level3**  
 인덱싱 표에 있는 셀의 Height 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Height_Of_Cell_In_Level4**  
 인덱싱 표에 있는 셀의 Height 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Area_Of_Cell_In_Level1**  
 인덱싱 표에 있는 셀의 Area 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Area_Of_Cell_In_Level2**  
 인덱싱 표에 있는 셀의 Area 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Area_Of_Cell_In_Level3**  
 인덱싱 표에 있는 셀의 Area 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **Area_Of_Cell_In_Level4**  
 인덱싱 표에 있는 셀의 Area 속성입니다. 측정 단위는 인덱스에 의해 제공되며 인덱싱된 데이터의 SRID에 따라 달라집니다. 값이 **float**입니다.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level1**  
 수준 1 셀에의 한 경계 상자의 적용 범위 비율입니다. 값이 **float**입니다.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level2**  
 수준 2 셀에의 한 경계 상자의 적용 범위 비율입니다. 값이 **float**입니다.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level3**  
 수준 3 셀에의 한 경계 상자의 적용 범위 비율입니다. 값이 **float**입니다.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level4**  
 수준 4 셀별 경계 상자의 포함 범위 비율입니다. 값이 **float**입니다.  
  
 **Number_Of_Rows_Selected_By_Primary_Filter**  
 기본 필터에 의해 선택된 행의 수입니다. 이 속성은 핵심 속성입니다. 값이 **bigint입니다.**  
  
 **Number_Of_Rows_Selected_By_Internal_Filter**  
 내부 필터에 의해 선택된 행의 수입니다. 보조 필터는 이 행에 대해 호출되지 않습니다. 이 속성은 핵심 속성입니다. 값이 **bigint입니다.**  
  
 반환 된 숫자는 **Stintersects**때만 적용 됩니다.  
  
 **Number_Of_Times_Secondary_Filter_Is_Called**  
 보조 필터가 호출된 횟수입니다. 이 속성은 핵심 속성입니다. 값이 **bigint입니다.**  
  
 **Percentage_Of_Rows_NotSelected_By_Primary_Filter**  
 기본 테이블에 N개의 행이 있고 기본 필터에 의해 P개가 선택되었다면 이 속성은 (N-P)/N을 비율로 반환합니다. 이 속성은 핵심 속성입니다. 값이 **float입니다.**  
  
 **Percentage_Of_Primary_Filter_Rows_Selected_By_internal_Filter**  
 P개의 행이 기본 필터에 의해 선택되고 S개의 행이 내부 필터에 의해 선택되었다면 이 속성은 S/P를 비율로 반환합니다. 이 비율이 높을수록 인덱스에서 성능에 불리한 보조 필터의 사용은 줄어듭니다. 이 속성은 핵심 속성입니다. 값이 **float입니다.**  
  
 **Number_Of_Rows_Output**  
 쿼리에서 출력한 행의 수입니다. 이 속성은 핵심 속성입니다. 값이 **bigint입니다.**  
  
 **Internal_Filter_Efficiency**  
 출력된 행의 수가 O라면 이 속성은 S/O를 비율로 반환합니다. 이 속성은 핵심 속성입니다. 값이 **float입니다.**  
  
 **Primary_Filter_Efficiency**  
 기본 필터에서 P 행을 선택 하 고 O가 행의 수를 출력 하는 경우이 값은 백분율로 표시 됩니다. 기본 필터의 효율성이 높을수록 보조 필터가 처리해야 하는 거짓 긍정의 수는 줄어듭니다. 이 속성은 핵심 속성입니다. 값이 **float입니다.**  
  
## <a name="permissions"></a>사용 권한  
 사용자는 **public** 역할의 멤버 여야 합니다. 서버 및 개체에 대한 READ ACCESS 권한이 필요합니다. 모든 공간 인덱스 저장 프로시저에 적용됩니다.  
  
## <a name="remarks"></a>설명  
 NULL 값이 포함된 속성은 반환 집합에 포함되지 않습니다.  
  
## <a name="examples"></a>예제  
 예를 보려면 다음 항목을 참조하십시오.  
  
-   [Transact-sql&#41;sp_help_spatial_geometry_index &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [Transact-sql&#41;sp_help_spatial_geometry_index_xml &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [Transact-sql&#41;sp_help_spatial_geography_index &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [Transact-sql&#41;sp_help_spatial_geography_index_xml &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="requirements"></a>요구 사항  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;공간 인덱스 저장 프로시저 &#40;]()   
 [Transact-sql&#41;sp_help_spatial_geometry_index &#40;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [XQuery 기본 사항](../../xquery/xquery-basics.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
