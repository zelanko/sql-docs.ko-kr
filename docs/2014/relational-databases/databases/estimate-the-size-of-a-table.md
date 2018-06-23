---
title: 테이블 크기 예측 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8410df06898ed7c536c8a6bc8c368c1ec68d6457
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092848"
---
# <a name="estimate-the-size-of-a-table"></a>테이블 크기 예측
  다음 단계를 통해 테이블에 데이터를 저장하는 데 필요한 공간을 추정할 수 있습니다.  
  
1.  [힙 크기 예측](estimate-the-size-of-a-heap.md) 또는 [클러스터형 인덱스의 크기 예측](estimate-the-size-of-a-clustered-index.md)의 설명에 따라 힙 또는 클러스터형 인덱스에 필요한 공간을 계산합니다.  
  
2.  비클러스터형 인덱스의 경우 [비클러스터형 인덱스의 크기 예측](estimate-the-size-of-a-nonclustered-index.md)의 설명에 따라 필요한 공간을 계산합니다.  
  
3.  1단계와 2단계에서 계산한 값을 더합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 크기 예측](estimate-the-size-of-a-database.md)   
 [힙 크기 예측](estimate-the-size-of-a-heap.md)   
 [클러스터형 인덱스의 크기 예측](estimate-the-size-of-a-clustered-index.md)   
 [비클러스터형 인덱스의 크기 예측](estimate-the-size-of-a-nonclustered-index.md)  
  
  