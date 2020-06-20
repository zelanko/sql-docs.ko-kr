---
title: 힙 크기 예측 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- estimating heap size
- size [SQL Server], heap
- space [SQL Server], indexes
- heaps
ms.assetid: 81fd5ec9-ce0f-4c2c-8ba0-6c483cea6c75
author: stevestein
ms.author: sstein
ms.openlocfilehash: 814175fa78176d14167355bfe188179552c545c6
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965983"
---
# <a name="estimate-the-size-of-a-heap"></a>힙 크기 예측
  다음 단계에 따라 힙에 데이터를 저장하는 데 필요한 공간의 크기를 예측할 수 있습니다.  
  
1.  테이블의 행 수를 지정합니다.  
  
     ***Num_Rows***  = 테이블의 행 수  
  
2.  고정 길이 및 가변 길이 열 수를 지정하고 이러한 열을 스토리지하는 데 필요한 공간을 계산합니다.  
  
     이러한 각 열 그룹이 데이터 행 내에서 차지하는 공간을 계산합니다. 열 크기는 지정된 데이터 형식과 길이에 따라 달라집니다.  
  
     ***Num_Cols***  = 열의 총 수(고정 길이 및 가변 길이)  
  
     ***Fixed_Data_Size***  = 모든 고정 길이 열의 총 바이트 크기  
  
     ***Num_Variable_Cols***  = 가변 길이 열의 수  
  
     ***Max_Var_Size***  = 모든 가변 길이 열의 전체 바이트 크기  
  
3.  행의 Null 비트맵 부분은 열의 Null 허용 여부 관리를 위해 예약됩니다. 다음과 같이 이 부분의 크기를 계산합니다.  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     이 식의 정수 부분만 사용하고 나머지는 무시해야 합니다.  
  
4.  가변 길이 데이터 크기를 계산합니다.  
  
     테이블에 가변 길이 열이 있는 경우에는 해당 행 안에 열을 저장하는 데 사용되는 공간을 측정합니다.  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     ***Max_Var_Size*** 에 추가된 바이트는 각 가변 길이 열을 추적하기 위한 것입니다. 이 수식에서는 모든 가변 길이 열이 100% 꽉 찬 것으로 가정합니다. 사용할 가변 길이 열 스토리지 공간 비율이 더 적을 것으로 예상되는 경우 해당 비율로 ***Max_Var_Size*** 값을 조정하여 전체 테이블 크기를 보다 정확하게 예측할 수 있습니다.  
  
    > [!NOTE]  
    >  정의된 총 테이블 너비가 8,060바이트를 초과하는 `varchar`, `nvarchar`, `varbinary` 또는 `sql_variant` 열을 결합할 수 있습니다. 이러한 열 각각의 길이는 `varchar` , 또는 열에 대해 8000 바이트 이내로 제한 되어야 합니다 `nvarchar,``varbinary` `sql_variant` . 그러나 결합된 너비는 테이블의 8,060바이트 제한을 초과할 수 있습니다.  
  
     가변 길이 열이 없는 경우에는 ***Variable_Data_Size*** 를 0으로 설정합니다.  
  
5.  전체 행 크기를 계산합니다.  
  
     ***Row_Size***   =  ***Fixed_Data_Size***  +  ***Variable_Data_Size***  +  ***Null_Bitmap*** + 4  
  
     이 수식에서 값 4는 데이터 행의 행 머리글 오버헤드입니다.  
  
6.  페이지당 행 수를 계산합니다. 페이지당 사용 가능한 바이트 수는 8,096바이트입니다.  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     행이 여러 페이지에 걸쳐 배치되지는 않으므로 페이지당 행 수는 가장 근사한 정수 값으로 내림하여 계산해야 합니다. 수식에서 값 2는 페이지의 슬롯 배열에서 행의 입력을 위한 것입니다.  
  
7.  모든 행을 저장하는 데 필요한 페이지 수를 계산합니다.  
  
     ***Num_Pages***  = ***Num_Rows*** / ***Rows_Per_Page***  
  
     예상 페이지 수는 가장 근사한 전체 페이지로 올림되어 계산됩니다.  
  
8.  힙에 데이터를 저장하는 데 필요한 공간의 크기를 계산합니다(페이지당 총 8192바이트임).  
  
     힙 크기(바이트) = 8192 x ***Num_Pages***  
  
 이 계산에서 다음 사항은 고려되지 않습니다.  
  
-   분할  
  
     분할에 따른 공간 오버헤드는 최소 수준이지만 계산하기 복잡합니다. 분할의 포함 여부는 중요하지 않습니다.  
  
-   할당 페이지  
  
     힙에 할당된 페이지를 추적하는 데 사용되는 IAM 페이지가 하나 이상 있지만 공간 오버헤드가 최소 수준이며 사용될 IAM 페이지 수를 정확하게 계산할 수 있는 알고리즘이 없습니다.  
  
-   LOB(Large Object) 값  
  
     LOB 데이터 형식,,, `varchar(max)` `varbinary(max)` `nvarchar(max)` `text` , **ntextxml**및 값을 저장 하는 데 사용 되는 공간을 정확 하 게 결정 하는 알고리즘은 `image` 복잡 합니다. LOB 값의 예상 평균 크기만 전체 힙 크기에 추가해도 됩니다.  
  
-   압축  
  
     압축된 힙 크기를 미리 계산할 수 없습니다.  
  
-   스파스 열  
  
     스파스 열의 공간 요구 사항은 [Use Sparse Columns](../tables/use-sparse-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [힙&#40;클러스터형 인덱스가 없는 테이블&#41;](../indexes/heaps-tables-without-clustered-indexes.md)   
 [클러스터형 및 비클러스터형 인덱스 소개](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [클러스터형 인덱스 만들기](../indexes/create-clustered-indexes.md)   
 [비클러스터형 인덱스 만들기](../indexes/create-nonclustered-indexes.md)   
 [테이블 크기 예측](estimate-the-size-of-a-table.md)   
 [클러스터형 인덱스의 크기 예측](estimate-the-size-of-a-clustered-index.md)   
 [비클러스터형 인덱스의 크기 예측](estimate-the-size-of-a-nonclustered-index.md)   
 [데이터베이스 크기 예측](estimate-the-size-of-a-database.md)  
  
  
