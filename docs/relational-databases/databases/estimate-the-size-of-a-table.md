---
title: "테이블 크기 예측 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "페이지 [SQL Server], 공간"
  - "공간 [SQL Server], 테이블"
  - "행 크기 [SQL Server]"
  - "크기 [SQL Server], 테이블"
  - "열 크기 [SQL Server]"
  - "테이블 크기 예측 [SQL Server]"
  - "테이블 크기 [SQL Server]"
  - "테이블 크기 예측"
  - "클러스터형 인덱스, 테이블 크기"
  - "디스크 공간 [SQL Server], 테이블"
  - "공간 할당 [SQL Server], 테이블 크기"
  - "데이터베이스 디자인 [SQL Server], 크기 예측"
  - "페이지당 예약된 사용 가능한 행 수 [SQL Server]"
  - "테이블 크기 계산"
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 테이블 크기 예측
  다음 단계를 통해 테이블에 데이터를 저장하는 데 필요한 공간을 추정할 수 있습니다.  
  
1.  [힙 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-heap.md) 또는 [클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)의 설명에 따라 힙 또는 클러스터형 인덱스에 필요한 공간을 계산합니다.  
  
2.  비클러스터형 인덱스의 경우 [비클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)의 설명에 따라 필요한 공간을 계산합니다.  
  
3.  1단계와 2단계에서 계산한 값을 더합니다.  
  
## 참고 항목  
 [데이터베이스 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [힙 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [비클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  