---
title: ODBC 연결 풀링 옵션 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43d4fe1ab363326269daf40375e126b930d2548b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901637"
---
# <a name="setting-odbc-connection-pooling-options"></a>ODBC 연결 풀링 옵션 설정
연결 풀링은 응용 프로그램 풀을 사용할 때마다 다시 설정할 수는 필요 하지 않은 연결의 연결을 사용 합니다. 사용할 수는 **연결 풀링을** 탭의 **ODBC 데이터 원본 관리자** 대화 상자를 사용 하 여 성능 모니터링을 사용 하지 않도록 설정 합니다. 연결 시간 제한 기간을 설정 하려면 드라이버 이름이 두 번 클릭 합니다.  
  
 드라이버 수준에서 연결 풀링이 CPTimeout 레지스트리 값으로 사용 됩니다. 이 선택적 드라이버 사용 하면 드라이버에서 지 원하는 방금 연결 풀링을 사용 하도록 시스템 관리자가 있습니다. 이 작업은 드라이버의 설치 프로그램 중 CPTimeout의 기본값을 설정 하 여 수행 됩니다. 연결 시간 제한 기간을 설정 하려면 드라이버 이름이 두 번 클릭 합니다.  
  
 연결 풀링에 대 한 자세한 내용은 참조 하세요. [ODBC 연결 풀링](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)합니다.  
  
## <a name="performance-monitoring"></a>성능 모니터링  
 다양 한 통계를 기록 하 여 연결 성과 추적 성능을 모니터링 합니다. 이러한 통계는 다음과 같은 항목을 포함 하도록 개발자가 사용자 지정할 수 있습니다.  
  
|카운터|정의|  
|-------------|----------------|  
|초당 ODBC 하드 연결 카운터|서버에 대 한 실제 초당 연결 횟수입니다. 환경을 전달 하 여 과도 한 로드를 처음으로이 카운터 상승할 매우 신속 하 게 합니다. 몇 초 후이를 0으로 삭제 됩니다. 연결 풀링이 작동 하는 경우 이것이 일반적인 상황입니다. 서버에 대 한 연결을 설정한 경우 이러한 사용 되며 다시 사용할 수 있도록 풀에 배치 합니다.|  
|ODBC 하드 초당 카운터 연결 끊기|하드 수가 서버에 발급 한 초당 연결을 끊습니다. 이들은 연결 풀링 하 여 릴리스되는 실제 서버에 연결 합니다. 시스템에서 모든 클라이언트를 중지 하 고 연결 시간 초과 하기 시작 하는 경우이 값은 0부터 증가 합니다.|  
|초당 ODBC 소프트 연결 카운터|두 번째 말해를 연결 하는 풀 당 풀에서 만족된 하는 연결 수를 사용자에 게 전달 되었습니다. 이 카운터는 풀링 작동 하는지 여부를 나타냅니다. 서버의 부하에 따라 초당 40-60 소프트 연결을 표시 하려면이 옵션에 대 한 일반적이 지 않은 아닙니다.|  
|ODBC 연결 끊기 소프트 카운터 per Second|수가 응용 프로그램에서 발급 한 초당 연결을 끊습니다. 응용 프로그램 해제 또는 연결을 끊을 경우 연결 풀에 다시 배치 됩니다.|  
|ODBC 현재 활성 연결 카운터|풀에서 현재 사용 중인 연결의 수입니다.|  
|ODBC 현재 사용 가능한 연결이 카운터|풀에서 사용할 수 있는 사용 가능한 연결입니다. 현재 개수입니다. 이들은 용도로 사용할 수 있는 라이브 연결입니다.|  
|현재 활성 풀|현재 풀 수입니다. 이 카운터는 Windows 8에서는 연결 풀에서 연결을 관리 하는 드라이버에 대 한 추가 되었습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.|  
|만든 풀|활성, 활성 및 제거 풀 포함 하 여 풀의 수입니다. 이 카운터는 Windows 8에서는 연결 풀에서 연결을 관리 하는 드라이버에 대 한 추가 되었습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.|  
  
 사용자 고유의 모니터링 매개 변수를 지정 해야 합니다. 성능 모니터링에 대 한 샘플은이 버전의 ODBC 사용 하 여 설명 되어 있습니다.
