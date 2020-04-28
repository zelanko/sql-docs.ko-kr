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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1d8e66c506518b77320347ce9120254aa1cae287
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307201"
---
# <a name="setting-odbc-connection-pooling-options"></a>ODBC 연결 풀링 옵션 설정
연결 풀링을 사용 하면 응용 프로그램에서 각 사용을 위해 다시 설정 하지 않아도 되는 연결 풀의 연결을 사용할 수 있습니다. **ODBC 데이터 원본 관리자** 대화 상자의 **연결 풀링** 탭을 사용 하 여 성능 모니터링을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 드라이버 이름을 두 번 클릭 하 여 연결 시간 제한 기간을 설정 합니다.  
  
 드라이버 수준에서 연결 풀링은 CPTimeout 레지스트리 값으로 설정 됩니다. 이러한 선택적 드라이버 사용을 통해 시스템 관리자는이를 지원할 수 있는 드라이버만 연결 풀링을 사용할 수 있습니다. 이 작업은 드라이버의 설치 프로그램 중에 CPTimeout의 기본값을 설정 하 여 수행 됩니다. 드라이버 이름을 두 번 클릭 하 여 연결 시간 제한 기간을 설정 합니다.  
  
 연결 풀링에 대 한 자세한 내용은 [ODBC 연결 풀링](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)을 참조 하세요.  
  
## <a name="performance-monitoring"></a>성능 모니터링  
 성능 모니터링은 다양 한 통계를 기록 하 여 연결 성능을 추적 합니다. 개발자는 다음과 같은 항목을 포함 하도록 이러한 통계를 사용자 지정할 수 있습니다.  
  
|카운터|정의|  
|-------------|----------------|  
|초당 ODBC 하드 연결 카운터|서버에 대 한 초당 실제 연결 수입니다. 환경에서 처음으로 부하가 많은 경우이 카운터는 매우 신속 하 게 수행 됩니다. 몇 초 후에 0으로 삭제 됩니다. 이는 연결 풀링이 작동 하는 일반적인 상황입니다. 서버에 대 한 연결이 설정 된 경우 사용 되 고 다시 사용 하기 위해 풀에 배치 됩니다.|  
|초당 ODBC 하드 연결 끊기 카운터|서버에서 발생 한 초당 하드 연결 끊기 수입니다. 연결 풀링을 통해 해제 되는 서버에 대 한 실제 연결입니다. 이 값은 시스템의 모든 클라이언트를 중지 하 고 연결이 시간 초과 되기 시작 하면 0에서 증가 합니다.|  
|초당 ODBC 소프트 연결 카운터 수|초당 풀에서 충족 하는 연결 수입니다. 즉, 사용자에 게 전달 된 해당 풀에서의 연결입니다. 이 카운터는 풀링이 작동 하는지 여부를 나타냅니다. 서버의 부하에 따라 초당 40-60 소프트 연결을 표시 하는 것이 일반적이 지 않습니다.|  
|초당 ODBC 소프트 연결 끊기 카운터|응용 프로그램에서 실행 한 초당 연결 끊기 수입니다. 응용 프로그램을 해제 하거나 연결을 끊으면 연결이 풀에 다시 배치 됩니다.|  
|ODBC 현재 활성 연결 카운터|풀에서 현재 사용 중인 연결 수입니다.|  
|ODBC 현재 사용 가능한 연결 카운터|풀에서 사용할 수 있는 현재 사용 가능한 연결 수입니다. 이러한 연결은 사용할 수 있는 라이브 연결입니다.|  
|현재 활성 풀|현재 활성화 된 풀 수입니다. 이 카운터는 연결 풀에서 연결을 관리 하는 드라이버에 대해 Windows 8에서 추가 되었습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조 하세요.|  
|만든 풀|활성 및 제거 된 풀을 포함 한 활성 풀 수입니다. 이 카운터는 연결 풀에서 연결을 관리 하는 드라이버에 대해 Windows 8에서 추가 되었습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조 하세요.|  
  
 고유한 모니터링 매개 변수를 지정 해야 합니다. 이 버전의 ODBC에는 성능 모니터링 샘플이 포함 되어 있습니다.
