---
title: 클러스터형 인덱스의 크기 예측 | Microsoft 문서
description: 이 절차를 사용하여 SQL Server에서 클러스터형 인덱스에 데이터를 저장하는 데 필요한 공간의 크기를 예측할 수 있습니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- disk space [SQL Server], indexes
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- space [SQL Server], indexes
- clustered indexes, table size
- nonclustered indexes [SQL Server], table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: 2b5137f8-98ad-46b5-9aae-4c980259bf8d
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || >= sql-server-2016
ms.openlocfilehash: d963a8745d83be039fa2970a24d04a2a882bf7a9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478364"
---
# <a name="estimate-the-size-of-a-clustered-index"></a>클러스터형 인덱스의 크기 예측

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  다음 단계를 사용하여 클러스터형 인덱스에 데이터를 저장하는 데 필요한 공간을 예측할 수 있습니다.  
  
1.  클러스터형 인덱스의 리프 수준에 데이터를 저장하는 데 사용되는 공간을 계산합니다.  
  
2.  클러스터형 인덱스에 대한 인덱스 정보를 저장하는 데 사용되는 공간을 계산합니다.  
  
3.  계산된 값을 더합니다.  
  
## <a name="step-1-calculate-the-space-used-to-store-data-in-the-leaf-level"></a>1단계. 리프 수준에 데이터를 저장하는 데 사용되는 공간 계산  
  
1.  테이블의 행 수를 지정합니다.  
  
     ***Num_Rows** _  = 테이블의 행 수  
  
2.  고정 길이 및 가변 길이 열 수를 지정하고 이러한 열을 스토리지하는 데 필요한 공간을 계산합니다.  
  
     이러한 각 열 그룹이 데이터 행 내에서 차지하는 공간을 계산합니다. 열 크기는 지정된 데이터 형식과 길이에 따라 달라집니다.  
  
     _*_Num_Cols_*_  = 열의 총 수(고정 길이 및 가변 길이)  
  
     _*_Fixed_Data_Size_*_  = 모든 고정 길이 열의 총 바이트 크기  
  
     _*_Num_Variable_Cols_*_  = 가변 길이 열의 수  
  
     _*_Max_Var_Size_*_  = 모든 가변 길이 열의 최대 바이트 크기  
  
3.  클러스터형 인덱스가 고유하지 않은 경우 _고유 식별자* 열을 계산합니다.  
  
     uniqueifier는 Null을 허용하는 가변 길이 열입니다. 고유하지 않은 키 값이 있는 행에서 이 열은 Null이 아니며 크기는 4바이트입니다. 이 값은 인덱스 키의 일부이며 모든 행에 고유 키 값이 있는지 확인하는 데 필요합니다.  
  
     ***Num_Cols** _  = _*_Num_Cols_*_ + 1  
  
     _*_Num_Variable_Cols_*_  = _*_Num_Variable_Cols_*_ + 1  
  
     _*_Max_Var_Size_*_  = _*_Max_Var_Size_*_ + 4  
  
     이러한 수정에서는 모든 값이 고유하지 않다고 가정합니다.  
  
4.  행의 Null 비트맵 부분은 열의 Null 허용 여부 관리를 위해 예약됩니다. 다음과 같이 이 부분의 크기를 계산합니다.  
  
     _*_Null_Bitmap_*_  = 2 + ((_*_Num_Cols_*_ + 7) / 8)  
  
     위 식의 정수 부분만 사용하고 나머지는 무시해야 합니다.  
  
5.  가변 길이 데이터 크기를 계산합니다.  
  
     테이블에 가변 길이 열이 있는 경우에는 해당 행 안에 열을 저장하는 데 사용되는 공간을 측정합니다.  
  
     _*_Variable_Data_Size_*_  = 2 + (_*_Num_Variable_Cols_*_ x 2) + _*_Max_Var_Size_*_  
  
     _*_Max_Var_Size_*_ 에 추가된 바이트는 각 변수 열을 추적하기 위한 것입니다. 이 수식에서는 모든 가변 길이 열이 100% 꽉 찬 것으로 가정합니다. 사용할 가변 길이 열 스토리지 공간 비율이 더 적을 것으로 예상되는 경우 해당 비율로 _*_Max_Var_Size_*_ 값을 조정하여 전체 테이블 크기를 보다 정확하게 예측할 수 있습니다.  
  
    > [!NOTE]  
    >  정의된 총 테이블 너비가 8,060바이트를 초과하는 _*varchar**, **nvarchar**, **varbinary** 또는 **sql_variant** 열을 결합할 수 있습니다. 이러한 각 열의 길이는 **varchar**, **varbinary** 또는 **sql_variant** 열의 경우 8,000바이트 이내여야 하고 **nvarchar** 열의 경우 4,000바이트 이내여야 합니다. 그러나 결합된 너비는 테이블의 8,060바이트 제한을 초과할 수 있습니다.  
  
     가변 길이 열이 없는 경우에는 **_Variable_Data_Size_* _를 0으로 설정합니다.  
  
6.  전체 행 크기를 계산합니다.  
  
     _*_Row_Size_*_  = _*_Fixed_Data_Size_*_ + _*_Variable_Data_Size_*_ + _*_Null_Bitmap_*_ + 4  
  
     값 4는 데이터 행의 행 머리글 오버헤드입니다.  
  
7.  페이지당 행 수를 계산합니다. 페이지당 사용 가능한 바이트 수는 8,096바이트입니다.  
  
     _*_Rows_Per_Page_*_  = 8096 / (_*_Row_Size_*_ + 2)  
  
     행이 여러 페이지에 걸쳐 배치되지는 않으므로 페이지당 행 수는 가장 근사한 정수 값으로 내림하여 계산해야 합니다. 수식에서 값 2는 페이지의 슬롯 배열에서 행의 입력을 위한 것입니다.  
  
8.  지정한 [채우기 비율](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) 을 기준으로 페이지당 예약된 사용 가능한 행 수를 계산합니다.  
  
     _*_Free_Rows_Per_Page_*_  = 8096 x ((100 - _*_Fill_Factor_*_) / 100) / (_*_Row_Size_*_ + 2)  
  
     계산에 사용되는 채우기 비율은 백분율이 아닌 정수 값입니다. 행이 여러 페이지에 걸쳐 배치되지는 않으므로 페이지당 행 수는 가장 근사한 정수 값으로 내림하여 계산해야 합니다. 채우기 비율이 클수록 각 페이지에 더 많은 데이터가 저장되고 페이지 수는 줄어듭니다. 수식에서 값 2는 페이지의 슬롯 배열에서 행의 입력을 위한 것입니다.  
  
9. 모든 행을 저장하는 데 필요한 페이지 수를 계산합니다.  
  
     _*_Num_Leaf_Pages_*_  = _*_Num_Rows_*_ / (_*_Rows_Per_Page_*_ - _*_Free_Rows_Per_Page_*_ )  
  
     예상 페이지 수는 가장 근사한 전체 페이지로 올림되어 계산됩니다.  
  
10. 리프 수준에 데이터를 저장하는 데 필요한 공간을 계산합니다. 페이지당 총 바이트 수는 8,192바이트입니다.  
  
     _*_Leaf_space_used_*_  = 8192 x _*_Num_Leaf_Pages_*_  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information"></a>2단계. 인덱스 정보를 저장하는 데 사용되는 공간 계산  
 다음 단계를 사용하여 인덱스의 상위 수준을 저장하는 데 필요한 공간을 예측할 수 있습니다.  
  
1.  인덱스 키의 고정 길이 및 가변 길이 열 수를 지정하고 이러한 열을 스토리지하는 데 필요한 공간을 계산합니다.  
  
     인덱스의 키 열은 고정 길이 및 가변 길이 열을 포함할 수 있습니다. 내부 수준 인덱스 행 크기를 예측하려면 인덱스 행 내에서 이러한 각 열 그룹이 차지하는 공간을 계산합니다. 열 크기는 지정된 데이터 형식과 길이에 따라 달라집니다.  
  
     _*_Num_Key_Cols_*_ = 키 열의 총수(고정 길이 및 가변 길이)  
  
     _*_Fixed_Key_Size_*_ = 모든 고정 길이 키 열의 총 바이트 크기  
  
     _*_Num_Variable_Key_Cols_*_ = 가변 길이 키 열의 수  
  
     _*_Max_Var_Key_Size_*_ = 모든 가변 길이 키 열의 최대 바이트 크기  
  
2.  인덱스가 고유하지 않은 경우 필요한 uniqueifier를 계산합니다.  
  
     uniqueifier는 Null을 허용하는 가변 길이 열입니다. 고유하지 않은 인덱스 키 값이 있는 행에서 이 열은 Null이 아니며 크기는 4바이트입니다. 이 값은 인덱스 키의 일부이며 모든 행에 고유 키 값이 있는지 확인하는 데 필요합니다.  
  
     _*_Num_Key_Cols_*_  = _*_Num_Key_Cols_*_ + 1  
  
     _*_Num_Variable_Key_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + 1  
  
     _*_Max_Var_Key_Size_*_  = _*_Max_Var_Key_Size_*_ + 4  
  
     이러한 수정에서는 모든 값이 고유하지 않다고 가정합니다.  
  
3.  Null 비트맵 크기를 계산합니다.  
  
     인덱스 키에 Null을 허용하는 열이 있으면 인덱스 행의 일부가 Null 비트맵용으로 예약됩니다. 다음과 같이 이 부분의 크기를 계산합니다.  
  
     _*_Index_Null_Bitmap_*_  = 2 + ((인덱스 행의 열 수 + 7) / 8)  
  
     위 식의 정수 부분만 사용하고 나머지는 무시해야 합니다.  
  
     Null을 허용하는 키 열이 없으면 _*_Index_Null_Bitmap_*_ 을 0으로 설정합니다.  
  
4.  가변 길이 데이터 크기를 계산합니다.  
  
     인덱스에 가변 길이 열이 있는 경우에는 해당 인덱스 행 안에 열을 저장하는 데 사용되는 공간을 결정합니다.  
  
     _*_Variable_Key_Size_*_  = 2 + (_*_Num_Variable_Key_Cols_*_ x 2) + _*_Max_Var_Key_Size_*_  
  
     _*_Max_Var_Key_Size_*_ 에 추가된 바이트는 각 가변 길이 열을 추적하기 위한 것입니다. 이 수식에서는 모든 가변 길이 열이 100% 꽉 찬 것으로 가정합니다. 사용할 가변 길이 열 스토리지 공간 비율이 더 적을 것으로 예상되는 경우 해당 비율로 _*_Max_Var_Key_Size_*_ 값을 조정하여 전체 테이블 크기를 보다 정확하게 예측할 수 있습니다.  
  
     가변 길이 열이 없는 경우에는 _*_Variable_Key_Size_*_ 를 0으로 설정합니다.  
  
5.  인덱스 행 크기를 계산합니다.  
  
     _*_Index_Row_Size_*_  = _*_Fixed_Key_Size_*_ + _*_Variable_Key_Size_*_ + _*_Index_Null_Bitmap_*_ + 1(인덱스 행의 행 머리글 오버헤드) + 6(자식 페이지 ID 포인터)  
  
6.  페이지당 인덱스 행 수를 계산합니다. 페이지당 사용 가능한 바이트 수는 8,096바이트입니다.  
  
     _*_Index_Rows_Per_Page_*_  = 8096 / (_*_Index_Row_Size_*_ + 2)  
  
     인덱스 행이 여러 페이지에 걸쳐 배치되지는 않으므로 페이지당 인덱스 행 수는 가장 근사한 정수 값으로 버림하여 계산해야 합니다. 수식에서 값 2는 페이지의 슬롯 배열에서 행의 입력을 위한 것입니다.  
  
7.  인덱스의 수준 수를 계산합니다.  
  
     _*_Non-leaf_Levels_*_  = 1 + log (Index_Rows_Per_Page) (_*_Num_Leaf_Pages_*_ / _*_Index_Rows_Per_Page_*_)  
  
     이 값을 가장 근사한 정수로 올립니다. 클러스터형 인덱스의 리프 수준은 이 값에 포함되지 않습니다.  
  
8.  인덱스의 비-리프 페이지 수를 계산합니다.  
  
     _*_Num_Index_Pages =_*_ ∑Level _*_ (Num_Leaf_Pages / (Index_Rows_Per_Page_ *_^Level_* _))_ *_  
  
     여기서 1 <= Level <= _*_Non-leaf_Levels_*_ 임  
  
     각 피가수를 가장 근사한 정수로 올립니다. 간단한 예로, _*_Num_Leaf_Pages_*_ = 1000 및 _*_Index_Rows_Per_Page_*_ = 25인 인덱스를 가정합니다. 리프 수준 위 첫 번째 인덱스 수준에 인덱스 행이 1000개 저장되고 리프 페이지당 인덱스 행 1개씩, 각 페이지마다 인덱스 행 25개가 들어갈 수 있습니다. 이러한 경우 인덱스 행 1000개를 저장하는 데 40페이지가 필요합니다. 인덱스의 다음 수준에서는 40개 행을 저장해야 하므로 2페이지가 필요합니다. 인덱스의 최종 수준에서는 2개 행을 저장해야 하므로 한 페이지가 필요합니다. 결과적으로 비-리프 인덱스 페이지 43개가 필요합니다. 앞의 수식에 이 숫자들을 사용하면 다음과 같은 결과가 나옵니다.  
  
     _*_Non-leaf_Levels_*_  = 1 + log(25) (1000 / 25) = 3  
  
     _*_Num_Index_Pages_*_ = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43(예에서 설명한 페이지 수)  
  
9. 인덱스 크기를 계산합니다. 페이지당 총 바이트 수는 8,192바이트입니다.  
  
     _*_Index_Space_Used_*_  = 8192 x _*_Num_Index_Pages_*_  
  
## <a name="step-3-total-the-calculated-values"></a>3단계. 계산된 값을 더하기  
 위의 두 단계에서 얻은 값을 더합니다.  
  
 클러스터형 인덱스 크기(바이트) = _*_Leaf_Space_Used_*_ + _*_Index_Space_used_*_  
  
 이 계산에서 다음 사항은 고려되지 않습니다.  
  
-   분할  
  
     분할에 따른 공간 오버헤드는 최소 수준이지만 계산하기 복잡합니다. 분할의 포함 여부는 중요하지 않습니다.  
  
-   할당 페이지  
  
     힙에 할당된 페이지를 추적하는 데 사용되는 IAM 페이지가 하나 이상 있지만 공간 오버헤드가 최소 수준이며 사용될 IAM 페이지 수를 정확하게 계산할 수 있는 알고리즘이 없습니다.  
  
-   LOB(Large Object) 값  
  
     LOB 데이터 형식 _*varchar(max)**, **varbinary(max)** , **nvarchar(max)** , **text**, **ntext**, **xml** 및 **image** 값을 저장하는 데 사용될 공간을 정확하게 측정하는 알고리즘은 복잡합니다. 예상되는 LOB 값의 평균 크기를 더하고 **_Num_Rows_** 를 곱한 후 해당 값을 총 클러스터형 인덱스 크기에 더하는 것만으로도 충분합니다.  
  
-   압축  
  
     압축된 인덱스 크기를 미리 계산할 수 없습니다.  
  
-   스파스 열  
  
     스파스 열의 공간 요구 사항은 [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [클러스터형 및 비클러스터형 인덱스 소개](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [테이블 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [클러스터형 인덱스 만들기](../../relational-databases/indexes/create-clustered-indexes.md)   
 [비클러스터형 인덱스 만들기](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [비클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [힙 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [데이터베이스 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
