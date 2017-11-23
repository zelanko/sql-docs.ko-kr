---
title: "ODBC 연결 풀링 옵션 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: admin
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d44325018516574641ccb938a8d7acbefb121cd4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="setting-odbc-connection-pooling-options"></a>ODBC 연결 풀링 옵션 설정
연결 풀링은 사용할 때마다 다시 설정에 필요 하지 않은 연결 풀에서 연결을 사용 하도록 응용 프로그램입니다. 사용할 수는 **연결 풀링** 탭은 **ODBC 데이터 원본 관리자** 대화 상자를 사용 하도록 설정 하 고 성능 모니터링을 사용 하지 않도록 설정 합니다. 연결 제한 시간을 설정 하는 드라이버 이름을 두 번 클릭 합니다.  
  
 드라이버 수준에서 연결 풀링이 CPTimeout 레지스트리 값으로 사용 됩니다. 이 선택적 드라이버 사용 하면 드라이버에서 지 원하는 방금 연결 풀링을 사용 하려면 시스템 관리자가 있습니다. 이 작업은 드라이버의 설치 프로그램 동안 CPTimeout의 기본값을 설정 하 여 수행 됩니다. 연결 제한 시간을 설정 하는 드라이버 이름을 두 번 클릭 합니다.  
  
 연결 풀링에 대 한 자세한 내용은 참조 [ODBC 연결 풀링](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)합니다.  
  
## <a name="performance-monitoring"></a>성능 모니터링  
 성능 모니터링 다양 한 통계를 기록 하 여 연결 성능을 추적 합니다. 이러한 통계는 다음과 같은 항목을 포함 하려면 개발자가 사용자 지정할 수 있습니다.  
  
|카운터|정의|  
|-------------|----------------|  
|ODBC 하드 연결 카운터 per Second|서버에 적용 된 초당 실제 연결의 수입니다. 사용자 환경 로드가 많은 경우 처음으로이 카운터 상승할 매우 신속 하 게 합니다. 몇 초 후 0 짧아집니다. 이 연결 풀링이 작동 하는 경우 일반적인 상황입니다. 서버에 대 한 연결을 설정 하는 경우 이러한 사용 되며 다시 사용할 수 있도록 풀에 배치 합니다.|  
|ODBC 하드 / 초 카운터 연결 끊기|하드 수 / 초는 서버에 발급 된 연결을 끊습니다. 이들은 연결 풀링에 발표 되는 서버에 실제 연결입니다. 시스템에서 모든 클라이언트를 중지 하 고 연결 시간 초과로 시작 하는 경우이 값은 0에서 증가 합니다.|  
|ODBC 연결 소프트 카운터 per Second|초당 풀에 의해 만족된 연결 수가-즉, 해당 풀에서는 연결 된 사용자에 게 전달 합니다. 이 카운터는 풀링이 작동 하는지 여부를 나타냅니다. 서버의 부하에 따라이 40-60 초 당 소프트 연결 표시에 대 한도 드물지 않습니다.|  
|ODBC 연결 끊기 소프트 카운터 per Second|개수는 응용 프로그램에서 발급 한 초당 연결을 끊습니다. 응용 프로그램 해제 되거나 연결 해제, 연결이 다시 풀에에서 배치 됩니다.|  
|ODBC 현재 활성 연결 카운터|풀에서 현재 사용 중인 연결의 수입니다.|  
|ODBC 현재 사용 가능한 연결이 카운터|풀에서 사용할 수 있는 사용 가능한 연결의 현재 수입니다. 이들은 사용 하기 위해 사용할 수 있는 라이브 연결입니다.|  
|현재 활성 풀|현재 풀 수를 지정 합니다. 이 카운터는 연결 풀에서 연결을 관리 하는 드라이버에 대 한 Windows 8에서 추가 되었습니다. 자세한 내용은 참조 [드라이버 인식 연결 풀링](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.|  
|생성 된 풀|활성 있었으며 제거 됨 풀 포함 하 여 현재 풀 수를 지정 합니다. 이 카운터는 연결 풀에서 연결을 관리 하는 드라이버에 대 한 Windows 8에서 추가 되었습니다. 자세한 내용은 참조 [드라이버 인식 연결 풀링](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.|  
  
 사용자 고유의 모니터링 매개 변수를 지정 해야 합니다. 성능 모니터링에 대 한 예제는이 버전의 ODBC와 설명 되어 있습니다.
