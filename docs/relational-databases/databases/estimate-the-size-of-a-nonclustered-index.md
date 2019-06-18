---
title: 비클러스터형 인덱스의 크기 예측 | Microsoft 문서
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: c183b0e4-ef4c-4bfc-8575-5ac219c25b0a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 80b6c00b0abcd09d4712b82df1d0d138cb37a390
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653166"
---
# <a name="estimate-the-size-of-a-nonclustered-index"></a>비클러스터형 인덱스의 크기 예측

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  다음 단계에 따라 비클러스터형 인덱스를 저장하는 데 필요한 공간을 예측합니다.  
  
1.  2단계와 3단계에서 사용할 변수를 계산합니다.  
  
2.  비클러스터형 인덱스의 리프 수준에 인덱스 정보를 저장하는 데 사용되는 공간을 계산합니다.  
  
3.  비클러스터형 인덱스의 리프가 아닌 수준에서 인덱스 정보를 저장하는 데 사용되는 공간을 계산합니다.  
  
4.  계산된 값을 더합니다.  
  
## <a name="step-1-calculate-variables-for-use-in-steps-2-and-3"></a>1단계. 2단계와 3단계에 사용할 변수 계산  
 다음 단계를 사용하여 인덱스의 상위 수준 저장에 필요한 공간을 예측하는 데 사용되는 변수를 계산할 수 있습니다.  
  
1.  테이블의 행 수를 지정합니다.  
  
     ***Num_Rows***  = 테이블의 행 수  
  
2.  인덱스 키의 고정 길이 및 가변 길이 열 수를 지정하고 이러한 열을 스토리지하는 데 필요한 공간을 계산합니다.  
  
     인덱스의 키 열은 고정 길이 및 가변 길이 열을 포함할 수 있습니다. 내부 수준 인덱스 행 크기를 예측하려면 인덱스 행 내에서 이러한 각 열 그룹이 차지하는 공간을 계산합니다. 열 크기는 지정된 데이터 형식과 길이에 따라 달라집니다.  
  
     ***Num_Key_Cols***  = 키 열의 총 수(고정 길이 및 가변 길이)  
  
     ***Fixed_Key_Size***  = 모든 고정 길이 키 열의 총 바이트 크기  
  
     ***Num_Variable_Key_Cols***  = 가변 길이 키 열의 수  
  
     ***Max_Var_Key_Size***  = 모든 가변 길이 키 열의 최대 바이트 크기  
  
3.  인덱스가 고유하지 않은 경우 필요한 데이터 행 로케이터를 다음과 같이 계산합니다.  
  
     비클러스터형 인덱스가 고유하지 않은 경우 데이터 행 로케이터가 비클러스터형 인덱스 키와 결합되어 각 행에 대한 고유 키 값을 생성합니다.  
  
     비클러스터형 인덱스가 힙에 있는 경우 데이터 행 로케이터는 힙 RID입니다. 크기는 8바이트입니다.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 8  
  
     비클러스터형 인덱스가 클러스터형 인덱스에 있는 경우 데이터 행 로케이터는 클러스터링 키입니다. 비클러스터형 인덱스 키와 결합되어야 하는 열은 비클러스터형 인덱스 키 열 집합에 아직 없는 클러스터링 키의 열입니다.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 비클러스터형 인덱스 키 열 집합에 없는 클러스터링 키 열의 수 + 1(클러스터형 인덱스가 고유하지 않은 경우)  
  
     ***Fixed_Key_Size***  = ***Fixed_Key_Size*** + 비클러스터형 인덱스 키 열 집합에 없는 고정 길이 클러스터링 키 열의 총 바이트 크기  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 비클러스터형 인덱스 키 열 집합에 없는 가변 길이 클러스터링 키 열의 수 + 1(클러스터형 인덱스가 고유하지 않은 경우)  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 비클러스터형 인덱스 키 열 집합에 없는 가변 길이 클러스터링 키 열의 최대 바이트 크기 + 4(클러스터형 인덱스가 고유하지 않은 경우)  
  
4.  행의 Null 비트맵 부분은 열의 Null 허용 여부 관리를 위해 예약됩니다. 다음과 같이 이 부분의 크기를 계산합니다.  
  
     인덱스 키에 Null을 허용하는 열이 있으면 1.3단계에서 설명한 것처럼 필요한 모든 클러스터링 키 열을 포함하여 인덱스 행의 일부가 Null 비트맵용으로 예약됩니다.  
  
     ***Index_Null_Bitmap***  = 2 + ((인덱스 행의 열 수 + 7) / 8)  
  
     위 식의 정수 부분만 사용하고 나머지는 무시해야 합니다.  
  
     Null을 허용하는 키 열이 없으면 ***Index_Null_Bitmap*** 을 0으로 설정합니다.  
  
5.  가변 길이 데이터 크기를 계산합니다.  
  
     인덱스 키에 가변 길이 열이 있는 경우에는 필요한 모든 클러스터형 인덱스 키 열을 포함하여 해당 인덱스 행 안에 열을 저장하는 데 사용되는 공간을 결정합니다.  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     ***Max_Var_Key_Size*** 에 추가된 바이트는 각 변수 열을 추적하기 위한 것입니다. 이 수식에서는 모든 가변 길이 열이 100% 꽉 찬 것으로 가정합니다. 사용할 가변 길이 열 스토리지 공간 비율이 더 적을 것으로 예상되는 경우 해당 비율로 ***Max_Var_Key_Size*** 값을 조정하여 전체 테이블 크기를 보다 정확하게 예측할 수 있습니다.  
  
     가변 길이 열이 없는 경우에는 ***Variable_Key_Size*** 를 0으로 설정합니다.  
  
6.  인덱스 행 크기를 계산합니다.  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1(인덱스 행의 행 머리글 오버헤드) + 6(자식 페이지 ID 포인터)  
  
7.  페이지당 인덱스 행 수를 계산합니다. 페이지당 사용 가능한 바이트 수는 8,096바이트입니다.  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     인덱스 행이 여러 페이지에 걸쳐 배치되지는 않으므로 페이지당 인덱스 행 수는 가장 근사한 정수 값으로 버림하여 계산해야 합니다. 수식에서 값 2는 페이지의 슬롯 배열에서 행의 입력을 위한 것입니다.  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information-in-the-leaf-level"></a>2단계. 리프 수준에 인덱스 정보를 저장하는 데 사용되는 공간 계산  
 다음 단계를 사용하여 인덱스의 리프 수준을 저장하는 데 필요한 공간을 예측할 수 있습니다. 이 단계를 완료하려면 1단계에서 보관된 값이 필요합니다.  
  
1.  리프 수준의 고정 길이 및 가변 길이 열 수를 지정하고 이러한 열을 스토리지하는 데 필요한 공간을 계산합니다.  
  
    > [!NOTE]  
    >  인덱스 키 열과 함께 키가 아닌 열을 포함하여 비클러스터형 인덱스를 확장할 수 있습니다. 이러한 추가 열은 비클러스터형 인덱스의 리프 수준에만 저장됩니다. 자세한 내용은 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)을 참조하세요.  
  
    > [!NOTE]  
    >  정의된 총 테이블 너비가 8,060바이트를 초과하는 **varchar**, **nvarchar**, **varbinary**또는 **sql_variant** 열을 결합할 수 있습니다. 이러한 각 열의 길이는 **varchar**, **varbinary**또는 **sql_variant** 열의 경우 8,000바이트 이내여야 하고 **nvarchar** 열의 경우 4,000바이트 이내여야 합니다. 그러나 결합된 너비는 테이블의 8,060바이트 제한을 초과할 수 있습니다. 이 규정은 포괄 열이 있는 비클러스터형 인덱스 리프 행에도 적용됩니다.  
  
     비클러스터형 인덱스에 포괄 열이 없는 경우 1단계의 값을 사용하되 해당 값에 1.3단계에서 결정된 모든 수정 내용을 적용합니다.  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols***  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size***  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols***  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size***  
  
     비클러스터형 인덱스에 포괄 열이 있는 경우 1.3단계에서 결정된 모든 수정 내용이 적용된 1단계의 값에 적절한 값을 추가합니다. 열 크기는 지정된 데이터 형식과 길이에 따라 달라집니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols*** + 포괄 열의 수  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size*** + 고정 길이 포괄 열의 총 바이트 크기  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols*** + 가변 길이 포괄 열의 수  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size*** + 가변 길이 포괄 열의 최대 바이트 크기  
  
2.  다음과 같이 데이터 행 로케이터를 계산합니다.  
  
     비클러스터형 인덱스가 고유하지 않은 경우 데이터 행 로케이터의 오버헤드는 1.3단계에서 이미 고려되어 추가적인 수정이 필요하지 않습니다. 다음 단계로 이동합니다.  
  
     비클러스터형 인덱스가 고유한 경우 리프 수준의 모든 행에 대해 데이터 행 로케이터를 계산해야 합니다.  
  
     비클러스터형 인덱스가 힙에 있는 경우 데이터 행 로케이터는 힙 RID(크기 8바이트)입니다.  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + 1  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + 1  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + 8  
  
     비클러스터형 인덱스가 클러스터형 인덱스에 있는 경우 데이터 행 로케이터는 클러스터링 키입니다. 비클러스터형 인덱스 키와 결합되어야 하는 열은 비클러스터형 인덱스 키 열 집합에 아직 없는 클러스터링 키의 열입니다.  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + 비클러스터형 인덱스 키 열 집합에 없는 클러스터링 키 열의 수 + 1(클러스터형 인덱스가 고유하지 않은 경우)  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Leaf_Size*** + 비클러스터형 인덱스 키 열 집합에 없는 고정 길이 클러스터링 키 열의 수  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + 비클러스터형 인덱스 키 열 집합에 없는 가변 길이 클러스터링 키 열의 수 + 1(클러스터형 인덱스가 고유하지 않은 경우)  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + 비클러스터형 인덱스 키 열 집합에 없는 가변 길이 클러스터링 키 열의 바이트 크기 + 4(클러스터형 인덱스가 고유하지 않은 경우)  
  
3.  Null 비트맵 크기를 계산합니다.  
  
     ***Leaf_Null_Bitmap***  = 2 + ((***Num_Leaf_Cols*** + 7) / 8)  
  
     위 식의 정수 부분만 사용하고 나머지는 무시해야 합니다.  
  
4.  가변 길이 데이터 크기를 계산합니다.  
  
     인덱스 키에 가변 길이 열이 있는 경우에는 2.2단계에서 이미 설명한 것처럼 필요한 클러스터링 키 열을 포함하여 해당 인덱스 행 내에 열을 저장하는 데 사용되는 공간을 결정합니다.  
  
     ***Variable_Leaf_Size***  = 2 + (***Num_Variable_Leaf_Cols*** x 2) + ***Max_Var_Leaf_Size***  
  
     ***Max_Var_Key_Size*** 에 추가된 바이트는 각 변수 열을 추적하기 위한 것입니다. 이 수식에서는 모든 가변 길이 열이 100% 꽉 찬 것으로 가정합니다. 사용할 가변 길이 열 스토리지 공간 비율이 더 적을 것으로 예상되는 경우 해당 비율로 ***Max_Var_Leaf_Size*** 값을 조정하여 전체 테이블 크기를 보다 정확하게 예측할 수 있습니다.  
  
     가변 길이 열이 없는 경우에는 ***Variable_Leaf_Size*** 를 0으로 설정합니다.  
  
5.  인덱스 행 크기를 계산합니다.  
  
     ***Leaf_Row_Size***  = ***Fixed_Leaf_Size*** + ***Variable_Leaf_Size*** + ***Leaf_Null_Bitmap*** + 1(인덱스 행의 행 머리글 오버헤드)  
  
6.  페이지당 인덱스 행 수를 계산합니다. 페이지당 사용 가능한 바이트 수는 8,096바이트입니다.  
  
     ***Leaf_Rows_Per_Page***  = 8096 / (***Leaf_Row_Size*** + 2)  
  
     인덱스 행이 여러 페이지에 걸쳐 배치되지는 않으므로 페이지당 인덱스 행 수는 가장 근사한 정수 값으로 버림하여 계산해야 합니다. 수식에서 값 2는 페이지의 슬롯 배열에서 행의 입력을 위한 것입니다.  
  
7.  지정한 [채우기 비율](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) 을 기준으로 페이지당 예약된 사용 가능한 행 수를 계산합니다.  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Leaf_Row_Size*** + 2)  
  
     계산에 사용되는 채우기 비율은 백분율이 아닌 정수 값입니다. 행이 여러 페이지에 걸쳐 배치되지는 않으므로 페이지당 행 수는 가장 근사한 정수 값으로 내림하여 계산해야 합니다. 채우기 비율이 클수록 각 페이지에 더 많은 데이터가 저장되고 페이지 수는 줄어듭니다. 수식에서 값 2는 페이지의 슬롯 배열에서 행의 입력을 위한 것입니다.  
  
8.  모든 행을 저장하는 데 필요한 페이지 수를 계산합니다.  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Leaf_Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     예상 페이지 수는 가장 근사한 전체 페이지로 올림되어 계산됩니다.  
  
9. 인덱스 크기를 계산합니다. 페이지당 총 바이트 수는 8,192바이트입니다.  
  
     ***Leaf_Space_Used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-3-calculate-the-space-used-to-store-index-information-in-the-non-leaf-levels"></a>3단계. 리프가 아닌 수준에 인덱스 정보를 저장하는 데 사용되는 공간 계산  
 다음 단계에 따라 중간 및 루트 수준의 인덱스를 저장하는 데 필요한 공간을 예측합니다. 이 단계를 완료하려면 2단계 및 3단계에서 보관된 값이 필요합니다.  
  
1.  인덱스의 리프가 아닌 수준의 수를 계산합니다.  
  
     ***Non-leaf Levels***  = 1 + log( Index_Rows_Per_Page) (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     이 값을 가장 근사한 정수로 올립니다. 비클러스터형 인덱스의 리프 수준은 이 값에 포함되지 않습니다.  
  
2.  인덱스의 비-리프 페이지 수를 계산합니다.  
  
     ***Num_Index_Pages***  = ∑Level (***Num_Leaf_Pages/Index_Rows_Per_Page***^Level)where 1 <= Level <= ***Levels***  
  
     각 피가수를 가장 근사한 정수로 올립니다. 간단한 예로, ***Num_Leaf_Pages*** = 1000 및 ***Index_Rows_Per_Page*** = 25인 인덱스를 가정합니다. 리프 수준 위 첫 번째 인덱스 수준에 인덱스 행이 1000개 저장되고 리프 페이지당 인덱스 행 1개씩, 각 페이지마다 인덱스 행 25개가 들어갈 수 있습니다. 이러한 경우 인덱스 행 1000개를 저장하는 데 40페이지가 필요합니다. 인덱스의 다음 수준에서는 40개 행을 저장해야 하므로 2페이지가 필요합니다. 인덱스의 최종 수준에서는 2개 행을 저장해야 하므로 1페이지가 필요합니다. 결과적으로 비-리프 인덱스 페이지가 43개 필요합니다. 앞의 수식에 이 숫자들을 사용하면 다음 결과가 나옵니다.  
  
     ***Non-leaf_Levels***  = 1 + log(25) (1000 / 25) = 3  
  
     ***Num_Index_Pages*** = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43(예에서 설명한 페이지 수)  
  
3.  인덱스 크기를 계산합니다. 페이지당 총 바이트 수는 8,192바이트입니다.  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-4-total-the-calculated-values"></a>4단계. 계산된 값을 더하기  
 위의 두 단계에서 얻은 값을 더합니다.  
  
 비클러스터형 인덱스 크기(바이트) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 이 계산에서 다음 사항은 고려되지 않습니다.  
  
-   분할  
  
     분할에 따른 공간 오버헤드는 최소 수준이지만 계산하기 복잡합니다. 분할의 포함 여부는 중요하지 않습니다.  
  
-   할당 페이지  
  
     힙에 할당된 페이지를 추적하는 데 사용되는 IAM 페이지가 하나 이상 있지만 공간 오버헤드가 최소 수준이며 사용될 IAM 페이지 수를 정확하게 계산할 수 있는 알고리즘이 없습니다.  
  
-   LOB(Large Object) 값  
  
     LOB 데이터 형식 **varchar(max)** , **varbinary(max)** , **nvarchar(max)** , **text**, **ntext**, **xml**및 **image** 값을 저장하는 데 사용될 공간을 정확하게 측정하는 알고리즘은 복잡합니다. 예상되는 LOB 값의 평균 크기를 더하고 ***Num_Rows***를 곱한 후 해당 값을 총 비클러스터형 인덱스 크기에 더하는 것만으로도 충분합니다.  
  
-   압축  
  
     압축된 인덱스 크기를 미리 계산할 수 없습니다.  
  
-   스파스 열  
  
     스파스 열의 공간 요구 사항은 [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [클러스터형 및 비클러스터형 인덱스 소개](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [비클러스터형 인덱스 만들기](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [클러스터형 인덱스 만들기](../../relational-databases/indexes/create-clustered-indexes.md)   
 [테이블 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [힙 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [데이터베이스 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
