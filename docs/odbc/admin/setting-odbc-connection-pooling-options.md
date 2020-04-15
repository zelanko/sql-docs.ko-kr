---
title: ODBC 연결 풀링 옵션 설정 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307201"
---
# <a name="setting-odbc-connection-pooling-options"></a>ODBC 연결 풀링 옵션 설정
연결 풀링을 사용하면 응용 프로그램에서 각 용도에 대해 다시 설정할 필요가 없는 연결 풀의 연결을 사용할 수 있습니다. **ODBC 데이터 원본 관리자** 대화 상자의 **연결 풀링 탭을** 사용하여 성능 모니터링을 활성화하고 비활성화할 수 있습니다. 드라이버 이름을 두 번 클릭하여 연결 시간 시간 시간 지정 기간을 설정합니다.  
  
 드라이버 수준에서 연결 풀링은 CPTimeout 레지스트리 값에 의해 활성화됩니다. 이 선택적 드라이버별 사용 은 시스템 관리자가 이를 지원할 수 있는 드라이버에 대해서만 연결 풀링을 활성화할 수 있도록 합니다. 드라이버 의 설정 프로그램 중에 CPTimeout의 기본값을 설정 하 여 수행 됩니다. 드라이버 이름을 두 번 클릭하여 연결 시간 시간 시간 지정 기간을 설정합니다.  
  
 연결 풀링에 대한 자세한 내용은 [ODBC 연결 풀링을](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)참조하십시오.  
  
## <a name="performance-monitoring"></a>성능 모니터링  
 성능 모니터링은 다양한 통계를 기록하여 연결 성능을 추적합니다. 이러한 통계는 개발자가 사용자 지정하여 다음과 같은 항목을 포함할 수 있습니다.  
  
|카운터|정의|  
|-------------|----------------|  
|초당 ODBC 하드 연결 카운터|서버에 대해 이루어지는 초당 실제 연결 수입니다. 환경에 처음으로 무거운 부하가 있을 때 이 카운터는 매우 빠르게 올라갑니다. 몇 초 후 0으로 떨어집니다. 연결 풀링이 작동할 때 정상적인 상황입니다. 서버에 대한 연결이 설정되면 다시 사용하기 위해 풀에 배치됩니다.|  
|ODBC 초당 하드 분리 카운터|서버에 발급된 초당 하드 연결 끊기 수입니다. 이러한 연결 풀링에 의해 해제 되는 서버에 대 한 실제 연결입니다. 이 값은 시스템의 모든 클라이언트를 중지하고 연결이 시간 초과하는 경우 0에서 증가합니다.|  
|초당 ODBC 소프트 커넥션 카운터|즉, 사용자에게 전달된 해당 풀의 연결, 즉 초당 풀에서 만족하는 연결 수입니다. 이 카운터는 풀링이 작동하는지 여부를 나타냅니다. 서버의 부하에 따라 초당 40-60개의 소프트 연결을 표시하는 것이 드문 일이 아닙니다.|  
|ODBC 소프트 단선 카운터 초당|응용 프로그램에서 발행한 초당 연결 끊기 수입니다. 응용 프로그램이 해제되거나 연결이 끊어지면 연결이 풀에 다시 배치됩니다.|  
|ODBC 현재 활성 연결 카운터|현재 사용 중인 풀의 연결 수입니다.|  
|ODBC 전류 무료 연결 카운터|풀에서 사용할 수 있는 현재 무료 연결 수입니다. 이러한 연결은 사용할 수 있는 라이브 연결입니다.|  
|현재 활성 상태인 풀|현재 활성 상태인 풀 수입니다. 이 카운터는 연결 풀에서 연결을 관리하는 드라이버에 대해 Windows 8에 추가되었습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조하십시오.|  
|생성된 풀|활성 및 제거된 풀을 포함하여 활성 풀 수입니다. 이 카운터는 연결 풀에서 연결을 관리하는 드라이버에 대해 Windows 8에 추가되었습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조하십시오.|  
  
 사용자 고유의 모니터링 매개 변수를 지정해야 합니다. 성능 모니터링을 위한 샘플이 이 버전의 ODBC에 포함되어 있습니다.
