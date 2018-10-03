---
title: SSMS XEvent Profiler 사용 | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: yualan
ms.author: alayu
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a7548f79744f3a48633d42249da6f1946459571a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791801"
---
# <a name="use-the-ssms-xevent-profiler"></a>SSMS XEvent Profiler 사용
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XEvent Profiler는 확장 이벤트의 라이브 뷰어 창이 표시되는 SSMS(SQL Server Management Studio) 기능입니다. 이 개요에서는 이 프로파일러를 사용하는 이유, 주요 기능 및 확장 이벤트를 보기 시작하기 위한 지침을 설명합니다.

## <a name="why-would-i-use-the-xevent-profiler"></a>XEvent Profiler를 왜 사용해야 합니까?
SQL Profiler와 달리, XEvent Profiler는 SSMS에 직접 통합되고 SQL 엔진의 확장성 있는 확장 이벤트 기술을 기반으로 빌드됩니다. 이 기능을 사용하면 SQL Server에서 진단 이벤트의 라이브 스트리밍 뷰에 빠르게 액세스할 수 있습니다. 이 보기는 사용자 지정할 수 있으며, 사용자 지정 항목을 .viewsettings 파일로 다른 SSMS 사용자와 공유할 수 있습니다. XE Profiler에서 만든 세션은 SQL Profiler를 사용하는 경우 유사한 SQL 추적에 비해 SQL Server 실행에 대한 침입성이 더 줄어들었습니다. 이 세션도 기존 XE 세션 속성 UI를 사용하거나 TSQL로 사용자가 사용자 지정할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항
이 기능은 SSMS(SQL Server Management Studio) v17.3 이상에서만 사용할 수 있습니다. 최신 버전을 사용하고 있는지 확인하세요. 최신 버전은 [여기](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)에서 찾을 수 있습니다.

## <a id="getting-started"></a>시작
XEvent Profiler에 액세스하려면 다음 단계를 수행합니다.

1. **SQL Server Management Studio**를 엽니다.

2. SQL Server 데이터베이스 엔진의 인스턴스 또는 localhost에 연결합니다.

3. 개체 탐색기에서 XE Profiler 메뉴 항목을 찾아 ‘+’ 기호를 클릭하여 확장합니다.

   ![XEProfiler 메뉴](media/xevents-xe-profiler-menu.png)

4. 이 세션에서 모든 확장 이벤트를 확인하려는 경우 **표준**을 두 번 클릭합니다. 기록된 SQL 문을 확인하려는 경우 **T-SQL**을 클릭합니다. 세션을 아직 만들지 않은 경우 세션이 자동으로 만들어집니다.

   ![XEProfiler 세션](media/xevents-xe-profiler-start-session.png)

5. 이제 확장 이벤트를 볼 수 있습니다.

   ![XEProfiler 뷰어](media/xevents-xe-profiler-start-viewer.png)

## <a name="see-also"></a>참고 항목
[확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
[확장 이벤트 도구](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
