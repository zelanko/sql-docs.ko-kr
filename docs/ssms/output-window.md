---
title: "SSMS 출력 창 | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Output Window [SQL Server Management Studio]
- Activity Monitor [SQL Server Management Studio]
- Object Explorer [SQL Server Management Studio]
ms.assetid: a2ce1a07-b4e2-471c-87d2-b8de5e6c6864
caps.latest.revision: "1"
author: shueybubbles
ms.author: davidshi
manager: kenvh
ms.workload: Inactive
ms.openlocfilehash: 68fedd92d79f508e0b85f369019a886356ed8475
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="output-window-in-sql-server-management-studio"></a>SQL Server Management Studio의 출력 창
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 출력 창은 [보기] 메뉴 또는 Ctrl+Alt+O 키 조합을 사용하여 열 수 있습니다. 사용 가능한 여러 출력 채널이 있습니다.

다음 표에서는 각 출력 채널과 연결된 메시지 유형에 대한 개요를 제공합니다.

|채널|Description|
|-----------|---------------|  
|**원격 분석**|원격 분석은 Microsoft에서 수집하는 [익명 기능 사용 현황 데이터](sql-server-management-studio-ssms.md)의 스트림입니다. 이러한 이벤트는 SSMS 사용량에 대한 사용자 고유의 레코드를 보관하는 데 유용할 수 있습니다. 이러한 이벤트는 출력 창이 열려 있는 동안 확장한 개체 탐색기 노드 및 SSMS 세션 중 실행한 명령을 식별하는 데 도움이 될 수 있습니다.|
|**개체 탐색기**|이 채널은 개체 탐색기에서 노드를 확장하는 데 필요한 쿼리 텍스트와 SQL 쿼리의 경과된 시간을 출력합니다. 각 쿼리는 쿼리 시작 및 쿼리 종료 이벤트를 기록합니다. 각 이벤트에는 쿼리하는 엔터티와 연결된 타임스탬프 및 URN이 있습니다. [URN](https://technet.microsoft.com/library/microsoft.sqlserver.management.smo.urn(v=sql.90).aspx)은 기본 SQL 관리 개체를 나타내며 XPath 스타일 계층 구조로 이루어져 있습니다. 예를 들어 “MyServer” 서버의 “Db” 데이터베이스에 있는 “Table1”이라는 테이블의 URN은 “Server[@Name='MyServer']/Database[@Name='Db']/Table[/@Name='Table1']”이 됩니다. 개체 탐색기에서 노드 하나를 확장하면 여러 매개 변수를 사용하여 여러 쿼리를 수행할 수 있습니다. 쿼리 종료 이벤트에는 TSQL 텍스트와 함께 쿼리의 경과된 시간이 포함됩니다. 개체 탐색기가 특정 노드를 확장하는 데 평소와 달리 느려지는 경우 서버 성능 분석에 이 쿼리 데이터가 유용할 수 있습니다. **참고**- 개체 탐색기의 일부 노드는 확장 시 이 수준의 쿼리 세부 정보를 제공하지 않습니다.|
|**작업 모니터**|이 채널은 서버에 대한 [작업 모니터를 열](https://docs.microsoft.com/en-us/sql/relational-databases/performance-monitor/activity-monitor) 때 시작됩니다. 이 스트림에는 각 쿼리의 쿼리 텍스트 부분과 타임스탬프, 오류 메시지, 연결 문제로 모니터가 일시 중지되었음을 나타내는 알림을 표시하는 이벤트가 포함됩니다. 작업 모니터가 유휴 상태이거나 업데이트되지 않는 것 같은 경우 자세한 내용을 보려면 이 출력 채널을 확인하세요.|





