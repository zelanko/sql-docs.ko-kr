---
title: Query Processing 이벤트 데이터 열 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09e4a72c0b87fea41befca72a257b9d4c4648fd3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="query-processing-events-data-columns"></a>Query Processing 이벤트 데이터 열
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Query Processing Events 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|70|Query Cube Begin|쿼리 큐브를 시작합니다.|  
|71|Query Cube End|쿼리 큐브를 종료합니다.|  
|72|Calculate Non Empty Begin|비어 있지 않음 계산을 시작합니다.|  
|73|Calculate Non Empty Current|비어 있지 않음 계산을 현재 실행 중입니다.|  
|74|Calculate Non Empty End|비어 있지 않음 계산을 종료합니다.|  
|75|Serialize Results Begin|결과 직렬화를 시작합니다.|  
|76|Serialize Results Current|결과 직렬화를 현재 실행 중입니다.|  
|77|Serialize Results End|결과 직렬화를 종료합니다.|  
|78|Execute MDX Script Begin|MDX 스크립트 실행을 시작합니다.|  
|79|Execute MDX Script Current|MDX 스크립트를 현재 실행 중입니다. 사용되지 않습니다.|  
|80|Execute MDX Script End|MDX 스크립트 실행을 종료합니다.|  
|81|Query Dimension|쿼리 차원입니다.|  
|11|Query Subcube|사용 빈도 기반 최적화에 대한 쿼리 하위 큐브입니다.|  
|12|Query Subcube Verbose|세부 정보가 포함된 쿼리 하위 큐브입니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|60|Get Data From Aggregation|집계 데이터를 가져와 쿼리에 응답합니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|61|Get Data From Cache|캐시 중 하나의 데이터를 가져와 쿼리에 응답합니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|82|VertiPaq SE Query Begin|VertiPaq SE 쿼리|  
|83|VertiPaq SE Query End|VertiPaq SE 쿼리|  
|84|Resource Usage|명령 및 쿼리 종료 후에 읽기, 쓰기 및 CPU 사용량을 보고합니다.|  
|85|VertiPaq SE Query Cache Match|VertiPaq SE 쿼리 캐시를 사용합니다.|  
|98|Direct Query Begin|직접 쿼리를 시작합니다.|  
|99|Direct Query End|직접 쿼리를 종료합니다.|  
  
 다음 표에서는 이러한 각 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="query-cube-begin"></a>Query Cube Begin  
  
|||||  
|-|-|-|-|  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="query-cube-end"></a>Query Cube End  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="calculate-non-empty-begin"></a>Calculate Non Empty Begin  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="calculate-non-empty-current"></a>Calculate Non Empty Current  
  
|||||  
|-|-|-|-|  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: Get Data<br /><br /> 2: Process Calculated Members<br /><br /> 3: Post Order|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="calculate-non-empty-end"></a>Calculate Non Empty End  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="serialize-results-begin"></a>Serialize Results Begin  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="serialize-results-current"></a>Serialize Results Current  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: Serialize Axes<br /><br /> 2: Serialize Cells<br /><br /> 3: Serialize SQL Rowset<br /><br /> 4: Serialize Flattened Rowset|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="serialize-results-end"></a>Serialize Results End  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="execute-mdx-script-begin"></a>Execute MDX Script Begin  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: MDX Script<br /><br /> 2: MDX Script Command|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="execute-mdx-script-current"></a>Execute MDX Script Current  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="execute-mdx-script-end"></a>Execute MDX Script End  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: MDX Script<br /><br /> 2: MDX Script Command|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="query-dimension"></a>Query Dimension  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: Cache data<br /><br /> 2: Non-cache data|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="query-subcube"></a>Query Subcube  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: Cache data<br /><br /> 2: Non-cache data<br /><br /> 3: Internal data<br /><br /> 4: SQL data<br /><br /> 11: Measure Group Structural Change<br /><br /> 12: Measure Group Deletion|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="query-subcube-verbose"></a>Query Subcube Verbose  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 21: Cache data<br /><br /> 22: Non-cache data<br /><br /> 23: Internal data<br /><br /> 24: SQL data|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="get-data-from-aggregation"></a>Get Data From Aggregation  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="get-data-from-cache"></a>Get Data From Cache  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: Get data from measure group cache<br /><br /> 2: Get data from flat cache<br /><br /> 3: Get data from calculation cache<br /><br /> 4: Get data from persisted cache|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="vertipaq-se-query-begin"></a>VertiPaq SE Query Begin  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 0: VertiPaq Scan<br /><br /> 1: Tabular Query<br /><br /> 2: User Hierarchy Processing Query<br /><br /> 10: VertiPaq Scan internal<br /><br /> 11: Tabular Query internal<br /><br /> 12: User Hierarchy Processing Query internal|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ObjectReference|15|8|개체 참조로, 개체를 설명하는 태그를 사용하여 모든 부모에 대한 XML로 인코딩됩니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="vertipaq-se-query-end"></a>VertiPaq SE Query End  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 0: VertiPaq Scan<br /><br /> 1: Tabular Query<br /><br /> 10: VertiPaq Scan internal<br /><br /> 11: Tabular Query internal|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|ProgressTotal|9|1.|총 진행률입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ObjectReference|15|8|개체 참조로, 개체를 설명하는 태그를 사용하여 모든 부모에 대한 XML로 인코딩됩니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="resource-usage"></a>Resource Usage  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="vertipaq-se-query-cache-match"></a>VertiPaq SE Query Cache Match  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 0: VertiPaq Cache exact match|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ObjectReference|15|8|개체 참조로, 개체를 설명하는 태그를 사용하여 모든 부모에 대한 XML로 인코딩됩니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="direct-query-begin"></a>Direct Query Begin  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="direct-query-end"></a>Direct Query End  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Query Processing 이벤트 범주](../../analysis-services/trace-events/query-processing-events-category.md)  
  
  
