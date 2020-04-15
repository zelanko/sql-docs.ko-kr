---
title: 스크롤 가능한 커서 및 트랜잭션 격리 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e40278bd209132736aee2788b5648ffa84a44e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304224"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>스크롤 가능 커서 및 트랜잭션 격리
다음 표에는 변경 의 가시성을 관리하는 요인이 나열되어 있습니다.  
  
|변경 사항:|가시성은 다음에 따라 달라집니다.|  
|----------------------|----------------------------|  
|커서|커서 유형, 커서 구현|  
|동일한 트랜잭션의 기타 명령문|커서 유형|  
|기타 거래의 진술|커서 유형, 트랜잭션 격리 수준|  
  
 이러한 요소는 다음 그림에 나와 있습니다.  
  
 ![변경 내용 표시를 제어하는 요소](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 다음 표에는 각 커서 유형이 자체적으로 변경한 내용, 자체 트랜잭션의 다른 작업 및 다른 트랜잭션을 검색하는 기능이 요약되어 있습니다. 후자의 변경 내용의 가시성은 커서 유형과 커서를 포함하는 트랜잭션의 격리 수준에 따라 달라집니다.  
  
|커서 유형\작업|자체|자신의<br /><br /> Txn|오트르 (주)<br /><br /> Txn<br /><br /> (RU[a])|오트르 (주)<br /><br /> Txn<br /><br /> (RC[a])|오트르 (주)<br /><br /> Txn<br /><br /> (RR[a])|오트르 (주)<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|정적|||||||  
|삽입|어쩌면 [b]|예|예|예|예|예|  
|업데이트|어쩌면 [b]|예|예|예|예|예|  
|DELETE|어쩌면 [b]|예|예|예|예|예|  
|키 집합|||||||  
|삽입|어쩌면 [b]|예|예|예|예|예|  
|업데이트|예|예|예|예|예|예|  
|DELETE|어쩌면 [b]|예|예|예|예|예|  
|동적|||||||  
|삽입|예|예|예|예|예|예|  
|업데이트|예|예|예|예|예|예|  
|DELETE|예|예|예|예|예|예|  
  
 [a] 괄호 안의 문자는 커서를 포함하는 트랜잭션의 격리 수준을 나타냅니다. 다른 트랜잭션의 격리 수준(변경이 이루어진 경우)은 관련이 없습니다.  
  
 RU: 커밋되지 않은 읽기  
  
 RC: 커밋된 읽기  
  
 RR: 반복 읽기  
  
 S: 직렬화 가능  
  
 [b] 커서가 구현되는 방법에 따라 다릅니다. 커서가 이러한 변경 내용을 검색할 수 있는지 여부는 **SQLGetInfo**의 SQL_STATIC_SENSITIVITY 옵션을 통해 보고됩니다.
