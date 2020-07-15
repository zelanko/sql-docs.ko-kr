---
title: 데이터베이스 크기 예측 | Microsoft 문서
description: SQL Server에서 데이터베이스를 디자인할 때 크기를 추정하면 성능 및 디스크 공간에 필요한 하드웨어 구성을 결정하는 데 도움이 될 수 있습니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], database size
- calculating database size
- increasing database size
- database size [SQL Server], estimating
- predicting database size
- size [SQL Server], databases
- estimating database size
- designing databases [SQL Server], estimating size
ms.assetid: 5b240161-eba4-44b0-946c-61a8fc00fc8c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 444513824770954f44919051d96a0a573f63b84f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008206"
---
# <a name="estimate-the-size-of-a-database"></a>데이터베이스 크기 예측
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  데이터베이스를 디자인할 때는 데이터베이스가 데이터로 가득 찰 때 얼마나 커질 수 있는지를 추정해야 합니다. 데이터베이스의 크기를 추정하면 다음을 수행하는 데 필요한 하드웨어 구성을 결정하는 데 도움이 됩니다.  
  
-   애플리케이션에서 필요한 성능을 확보합니다.  
  
-   데이터 및 인덱스를 저장하는 데 필요한 물리적 디스크 공간을 충분히 확보합니다.  
  
 또한 데이터베이스의 크기를 추정하면 데이터베이스 디자인을 수정해야 할지 여부를 결정할 수 있습니다. 예를 들어 예상 크기가 회사에서 실제로 구현하기에 너무 큰 경우에는 정규화가 더 필요하다는 것을 알 수 있습니다. 반대로 예상 크기가 생각보다 더 작을 수도 있습니다. 이 경우 데이터베이스를 비정규화하여 쿼리 성능을 높일 수 있습니다.  
  
 데이터베이스의 크기를 추정하려면 각 테이블의 크기를 따로 추정한 다음 그 값을 더하면 됩니다. 테이블의 크기는 테이블에 인덱스가 있는지 여부와 인덱스 유형에 따라 달라집니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[테이블 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-table.md)|테이블 및 연결된 인덱스에 데이터를 저장하는 데 필요한 공간을 예측하는 단계와 필요한 계산을 설명합니다.|  
|[힙 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-heap.md)|힙에 데이터를 저장하는 데 필요한 공간을 예측하는 단계와 필요한 계산을 설명합니다. 힙은 클러스터형 인덱스가 없는 테이블입니다.|  
|[클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)|클러스터형 인덱스에 데이터를 저장하는 데 필요한 공간을 예측하는 단계와 필요한 계산을 설명합니다.|  
|[비클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)|비클러스터형 인덱스에 데이터를 저장하는 데 필요한 공간을 예측하는 단계와 필요한 계산을 설명합니다.|  
  
  
