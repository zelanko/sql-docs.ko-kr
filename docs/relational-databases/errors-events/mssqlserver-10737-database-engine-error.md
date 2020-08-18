---
description: MSSQLSERVER_10737
title: MSSQLSERVER_10737 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 944f883e73cacf930d5cfff7eb5b59c5e8ed92b6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88337609"
---
# <a name="mssqlserver_10737"></a>MSSQLSERVER_10737
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|MSSQLSERVER|  
|이벤트 ID|10737|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|메시지 텍스트|ALTER TABLE REBUILD 또는 ALTER INDEX REBUILD 문에서 DATA_COMPRESSION 절에 지정된 파티션이 있으면 PARTITION=ALL을 지정해야 합니다. PARTITION=ALL 절은 DATA_COMPRESSION 절에 하위 집합만 지정된 경우에도 테이블 또는 인덱스의 모든 파티션이 다시 작성되도록 지원하는 데 사용됩니다.|  
  
## <a name="user-action"></a>사용자 동작  
ALTER TABLE 또는 ALTER INDEX 문에 PARTITION=ALL 절을 추가하거나 REBUILD PARTITION = \<partition-number-expr> WITH (DATA_COMPRESSION={ON | OFF})를 사용하여 특정 파티션을 다시 빌드합니다.  
  
