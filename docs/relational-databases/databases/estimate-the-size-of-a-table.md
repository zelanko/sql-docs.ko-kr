---
title: 테이블 크기 예측 | Microsoft 문서
description: 이 프로시저를 사용하여 SQL Server에서 테이블에 데이터를 저장하는 데 필요한 공간의 크기를 예측할 수 있습니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- pages [SQL Server], space
- space [SQL Server], tables
- row size [SQL Server]
- size [SQL Server], tables
- column size [SQL Server]
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- disk space [SQL Server], tables
- space allocation [SQL Server], table size
- designing databases [SQL Server], estimating size
- reserved free rows per page [SQL Server]
- calculating table size
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 06cc999eefd3515dc1cda8076d907843bb773931
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474094"
---
# <a name="estimate-the-size-of-a-table"></a>테이블 크기 예측
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  다음 단계를 통해 테이블에 데이터를 저장하는 데 필요한 공간을 추정할 수 있습니다.  
  
1.  [힙 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-heap.md) 또는 [클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)의 설명에 따라 힙 또는 클러스터형 인덱스에 필요한 공간을 계산합니다.  
  
2.  비클러스터형 인덱스의 경우 [비클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)의 설명에 따라 필요한 공간을 계산합니다.  
  
3.  1단계와 2단계에서 계산한 값을 더합니다.  

## <a name="see-also"></a>참고 항목  
 [데이터베이스 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [힙 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [비클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  
