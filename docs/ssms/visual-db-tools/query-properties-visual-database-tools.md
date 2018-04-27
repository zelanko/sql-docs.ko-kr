---
title: 쿼리 속성(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdtsql.chm:69636
- vdt.ppg.querydesigner.query
ms.assetid: 07495669-6ed5-4004-904e-aae1230be5e4
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96f152b0cc39d70ce702b46fc428bd6fbb9c01dd
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="query-properties-visual-database-tools"></a>쿼리 속성(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
쿼리 속성은 쿼리 및 뷰 디자이너에서 쿼리를 연 경우 속성 창에 표시됩니다. 별도로 언급하지 않는 한 속성 창에서 이러한 속성을 편집할 수 있습니다.  
  
> [!NOTE]  
> 이 항목의 속성은 사전순이 아니라 범주별로 정렬됩니다.  
  
## <a name="options"></a>변수  
**ID 범주**  
확장하면 **이름** 속성이 표시됩니다.  
  
**이름**  
현재 쿼리의 이름을 표시합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]에서는 이를 변경할 수 없습니다.  
  
**Database Name**  
선택한 테이블의 데이터 원본 이름을 표시합니다.  
  
**서버 이름**  
데이터 원본의 서버 이름을 표시합니다.  
  
**쿼리 디자이너 범주**  
확장하면 나머지 속성이 표시됩니다.  
  
**대상 테이블**  
데이터가 삽입되는 테이블의 이름을 지정합니다. 이 목록은 INSERT 쿼리 또는 MAKE TABLE 쿼리를 만드는 경우 나타납니다. INSERT 쿼리를 작성하는 경우 이 목록에서 테이블 이름을 선택하십시오.  
  
MAKE TABLE 쿼리를 작성하는 경우 새 테이블의 이름을 입력하십시오. 다른 데이터 원본에 대상 테이블을 만들려면 대상 데이터 원본의 이름, 소유자(필요한 경우) 및 테이블의 이름을 포함하는 정규화된 테이블 이름을 지정합니다.  
  
> [!NOTE]  
> 쿼리 디자이너는 이 이름이 이미 사용되고 있는지 또는 사용자에게 테이블을 만들 수 있는 권한이 있는지를 확인하지 않습니다.  
  
**고유 값**  
결과 집합에서 중복 항목을 필터링하도록 쿼리를 지정합니다. 이 옵션은 하나 이상의 테이블에 있는 열 중 일부만 사용하고 이 열에 중복 값이 포함되어 있는 경우 또는 둘 이상의 테이블을 조인하는 과정에서 결과 집합에 중복 행이 만들어지는 경우에 유용합니다. 이 옵션을 선택하면 SQL 창에서 DISTINCT를 문에 삽입하는 것과 결과가 같습니다.  
  
**GROUP BY 확장**  
집계 쿼리를 기반으로 하는 쿼리에 대한 추가 옵션을 사용할 수 있음을 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에만 적용됩니다.  
  
**모든 열 출력**  
현재 쿼리에서 모든 테이블의 전체 열이 결과 집합에 포함되도록 지정합니다. 이 옵션을 선택하면 SQL 문에서 SELECT 키워드 다음에 개별 열 이름 대신 별표(*)를 지정하는 것과 결과가 같습니다.  
  
**쿼리 매개 변수 목록**  
쿼리 매개 변수를 표시합니다. 이 매개 변수를 편집하려면 속성을 클릭한 다음 속성의 오른쪽에 있는 줄임표 **(...)** 를 클릭합니다. 일반 OLE DB에만 적용됩니다.  
  
**SQL 주석**  
SQL 문에 대한 설명을 표시합니다. 전체 설명을 보거나 편집하려면 설명을 클릭한 다음 속성의 오른쪽에 있는 줄임표 **(...)** 를 클릭합니다. 쿼리의 사용자나 사용 시기 등과 같은 정보를 주석에 포함할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 이상 버전에만 적용됩니다.  
  
**Top 사양 범주**  
확장하면 **Top**, **Percent**, **식**및 **With Ties** 속성이 표시됩니다.  
  
**(Top)**  
결과 집합에서 처음 *n* 개 행 또는 처음 *n* %에 해당하는 행만 반환하는 TOP 절이 쿼리에 포함되도록 지정합니다. 기본값은 쿼리가 결과 집합에서 처음 10개 행을 반환하는 것입니다.  
  
이 상자는 반환할 행 수를 변경하거나 백분율을 다르게 지정하려는 경우에 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에만 적용됩니다.  
  
**식**  
쿼리에서 반환할 행의 수나 비율을 지정합니다. **Percent** 를 예로 설정한 경우 이 값은 쿼리에서 반환할 행의 비율을 나타내고, **Percent** 를 아니요로 설정한 경우 이 값은 반환할 행의 수를 나타냅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 이상 버전에만 적용됩니다.  
  
**Percent**  
결과 집합의 처음 *n* %에 해당하는 행만 쿼리가 반환하도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 이상 버전에만 적용됩니다.  
  
**With Ties**  
뷰에 WITH TIES 절이 포함되도록 지정합니다. WITH TIES는 백분율을 기반으로 하는 ORDER BY 절과 TOP 절이 뷰에 포함되어 있을 경우 유용합니다. 이 옵션을 설정하는 경우 백분율 값이 ORDER BY 절에서 동일한 값을 가진 행 집합의 중간까지만 포함하면 동일한 값을 가진 행을 모두 포함할 수 있도록 뷰가 확장됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 이상 버전에만 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
[매개 변수를 사용하여 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
