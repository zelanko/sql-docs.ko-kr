---
title: sp_help_spatial_geometry_histogram (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_histogram
- sp_help_spatial_geometry_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_histogram
ms.assetid: 036aaf61-df3e-40f7-aa4e-62983c5a37bd
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 092a1e6e25bb445b30644b028e82677200376c5c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpspatialgeometryhistogram-transact-sql"></a>sp_help_spatial_geometry_histogram(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  공간 인덱스의 경계 상자 및 표 매개 변수의 키 지정을 용이하게 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_spatial_geometry_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @xmin = ] 'minx' ]   
     [ , [ @ymin = ] 'miny' ]   
     [ ,.[ @xmax = ] 'maxx' ]  
     [ , [ @ymax = ] 'maxy' ]  
     [ , [ @sample = ] 'sample' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@tabname =**] **'***tabname***'**  
 공간 인덱스가 지정된 테이블의 정규화된 이름 또는 정규화되지 않은 이름입니다.  
  
 따옴표는 정규화된 테이블이 지정된 경우에만 필요합니다. 데이터베이스 이름을 포함한 정규화된 이름인 경우 반드시 현재 데이터베이스의 이름을 사용해야 합니다. *tabname* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@colname =** ] **'***colname***'**  
 지정된 공간 열의 이름입니다. *colname* 는 **sysname**, 기본값은 없습니다.  
  
 [  **@resolution =** ] **'***해상도***'**  
 경계 상자의 해상도입니다. 유효한 값은 10부터 5000까지입니다. *해상도* 는 **tinyint**, 기본값은 없습니다.  
  
 [  **@xmin =** ] **'***xmin***'**  
 X 최소 경계 상자 속성입니다. *xmin* 는 **float**, 기본값은 없습니다.  
  
 [  **@ymin =** ] **'***ymin***'**  
 Y 최소 경계 상자 속성입니다. *ymin* 는 **float**, 기본값은 없습니다.  
  
 [  **@xmax =** ] **'***xmax***'**  
 X 최대 경계 상자 속성입니다. *xmax* 는 **float**, 기본값은 없습니다.  
  
 [  **@ymax =** ] **'***ymax***'**  
 Y 최대 경계 상자 속성입니다. *ymax* 는 **float**, 기본값은 없습니다.  
  
 [  **@sample =** ] **'***샘플***'**  
 사용된 테이블의 백분율입니다. 유효한 값은 0에서 100 사이입니다. *샘플* 는 **float**합니다. 기본값은 100입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 테이블 값이 반환됩니다. 다음 표에서는 테이블의 열 내용에 대해 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|각 셀의 고유한 ID를 나타내며 1부터 셉니다.|  
|**셀**|**geometry**|각 셀을 나타내는 사각의 다각형입니다. 셀 셰이프는 공간 인덱싱에 사용된 셀 셰이프와 동일합니다.|  
|**row_count**|**bigint**|셀에 접해 있거나 셀을 포함하는 공간 개체 수를 나타냅니다.|  
  
## <a name="permissions"></a>Permissions  
 사용자의 구성원 이어야 합니다.는 **공용** 역할입니다. 서버 및 개체에 대한 READ ACCESS 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 SSMS 공간 탭은 결과를 그래픽으로 나타냅니다. 공간 창에서 결과를 쿼리하여 결과 항목의 대략적인 개수를 가져올 수 있습니다. 테이블의 개체가 셀 한 개를 넘어갈 수 있으므로 셀 합계는 실제 개체의 개수보다 클 수 있습니다.  
  
 경계 상자를 벗어나거나 경계 상자 테두리에 접해 있는 개체의 수가 포함된 결과 집합에 행이 추가로 삽입될 수 있습니다. **cellid** 행이 행은 0 및 **셀** 이 행이 포함 되어 있는 한 **LineString** 경계 상자를 나타내는입니다. 이 행은 경계 상자 밖의 전체 공간을 나타냅니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 예제 테이블을 만들고 다음 호출 **sp_help_spatial_geometry_histogram** 테이블에 있습니다.  
  
 `USE AdventureWorksDW2012`  
  
 `GO`  
  
 `-- Set database compatibility for circular arc segments`  
  
 `ALTER DATABASE AdventureWorksDW2012`  
  
 `SET COMPATIBILITY_LEVEL = 110;`  
  
 `GO`  
  
 `-- Create table to execute sp_help_spatial_geometry_histogram on`  
  
 `CREATE TABLE TownSites`  
  
 `(`  
  
 `Location geometry NULL,`  
  
 `SiteName nvarchar(50) NULL`  
  
 `)`  
  
 `GO`  
  
 `-- Insert site data into table`  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('POINT(0 0)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Booth Map';`  
  
 `SET @g = geometry::Parse('POLYGON((1 1, 1 2, 2 2, 2 1, 1 1))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Town Hall';`  
  
 `SET @g = geometry::Parse('CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-1 0, 0 -1, 1 0),(1 0, 1 2, -1 0)))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Park';`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(1 5, 2 2, 5 1)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Road';`  
  
 `-- Call proc to see data within bounding box`  
  
 `EXEC sp_help_spatial_geometry_histogram @tabname = TownSites, @colname = Location, @resolution = 64, @xmin = -2, @ymin = -2, @xmax = 3, @ymax = 3, @sample = 100;`  
  
 `GO`  
  
 `DROP TABLE TownSites;`  
  
 `GO`  
  
## <a name="see-also"></a>관련 항목:  
 [공간 인덱스 저장 프로시저 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)  
  
  
