---
title: SQL Server Express LocalDB 인스턴스 API 참조 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: faec46da-0536-4de3-96f3-83e607c8a8b6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a9290e2b9b64c04545c833a2d04620d87564026e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68021953"
---
# <a name="sql-server-express-localdb-reference---instance-apis"></a>SQL Server Express LocalDB 참조 - 인스턴스 API
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  기존 서비스 기반 SQL Server 환경에서는 단일 컴퓨터에 설치되는 개별 SQL Server 인스턴스가 실제로 분리됩니다. 즉, 각 인스턴스가 개별적으로 설치 및 제거되고, 별도의 이진 파일 집합을 사용하며, 별도의 서비스 프로세스에 따라 실행됩니다. SQL Server 인스턴스 이름을 사용하여 연결할 SQL Server 인스턴스를 지정합니다.  
  
 SQL Server Express LocalDB 인스턴스 API는 단순화 된 "light" 인스턴스 모델을 사용 합니다. 개별 LocalDB 인스턴스가 디스크와 레지스트리에서 분리되지만, 동일한 공유 LocalDB 이진 파일 집합을 사용합니다. 또한 LocalDB는 서비스를 사용하지 않으며, LocalDB 인스턴스는 LocalDB 인스턴스 API 호출을 통해 요청될 때 실행됩니다. LocalDB에서는 인스턴스 이름을 사용하여 작업할 LocalDB 인스턴스를 지정합니다.  
  
 LocalDB 인스턴스는 항상 단일 사용자가 소유 하며 인스턴스 공유를 사용 하도록 설정 하지 않으면이 사용자의 컨텍스트에서만 표시 되 고 액세스할 수 있습니다.  
  
 기술적으로 LocalDB 인스턴스는 기존 SQL Server 인스턴스와 다르지만 용도는 비슷합니다. 이러한 유사성을 강조 하 고 사용자를 SQL Server 하는 것을 보다 직관적으로 만드는 *인스턴스* 라고 합니다.  
  
 LocalDB에서는 AI(Automatic Instance) 및 NI(Named Instance)의 두 가지 인스턴스를 지원합니다. LocalDB 인스턴스에 대한 식별자는 인스턴스 이름입니다.  
  
## <a name="automatic-localdb-instances"></a>자동 LocalDB 인스턴스  
 자동 LocalDB 인스턴스는 "공용"입니다. 사용자를 위해 자동으로 만들어지고 관리 되며 모든 응용 프로그램에서 사용할 수 있습니다. 사용자의 컴퓨터에 설치 된 모든 버전의 LocalDB에 대해 하나의 자동 LocalDB 인스턴스가 있습니다.  
  
 자동 LocalDB 인스턴스는 효율적으로 관리됩니다. 사용자는 인스턴스를 만들 필요가 없습니다. 자동 LocalDB를 사용하면 애플리케이션을 쉽게 설치하고 다른 컴퓨터로 쉽게 마이그레이션할 수 있습니다. 대상 컴퓨터에 지정된 버전의 LocalDB가 설치되어 있을 경우 해당 버전에 대한 자동 LocalDB 인스턴스를 대상 컴퓨터에서도 사용할 수 있습니다.  
  
### <a name="automatic-instance-management"></a>자동 인스턴스 관리  
 사용자는 자동 LocalDB 인스턴스를 만들 필요가 없습니다. 지정 된 버전의 LocalDB를 사용자의 컴퓨터에서 사용할 수 있는 경우 인스턴스가 처음 사용 될 때 인스턴스가 지연 생성 됩니다. 사용자의 관점에서 자동 인스턴스는 LocalDB 이진 파일이 있는 경우 항상 존재 합니다.  
  
 삭제, 공유, 공유 해제 등과 같은 다른 인스턴스 관리 작업도 자동 인스턴스에 대해 수행됩니다. 특히 자동 인스턴스를 삭제하면 인스턴스가 효율적으로 다시 설정되어 다음에 시작할 때 다시 만들어집니다. 시스템 데이터베이스가 손상된 경우 자동 인스턴스를 삭제해야 할 수 있습니다.  
  
### <a name="automatic-instance-naming-rules"></a>자동 인스턴스 명명 규칙  
 자동 LocalDB 인스턴스는 예약된 네임스페이스에 속하는 특수한 인스턴스 이름 패턴을 사용합니다. 이는 명명된 LocalDB 인스턴스와 이름이 충돌하는 것을 방지하기 위한 것입니다.  
  
 자동 인스턴스 이름은 단일 "v" 문자가 앞에 오는 LocalDB 기준 릴리스 버전 번호입니다. 이는 "v"와 두 개의 숫자 사이에 마침표를 두는 것과 같습니다. 예: v 11.0 또는 V 12.00.  
  
 잘못된 자동 인스턴스 이름의 예를 들면 다음과 같습니다.  
  
-   11.0 (시작 부분에 "v" 문자가 없음)  
  
-   v11(점과 버전의 두 번째 숫자가 없음)  
  
-   v11. (버전의 두 번째 숫자가 없음)  
  
-   v11.0.1.2(버전 번호가 세 개 이상의 부분으로 구성됨)  
  
## <a name="named-localdb-instances"></a>명명된 LocalDB 인스턴스  
 명명 된 LocalDB 인스턴스는 "private"입니다. 인스턴스는 인스턴스를 만들고 관리 하는 단일 응용 프로그램에 의해 소유 됩니다. 명명된 LocalDB 인스턴스는 격리되며 향상된 성능을 제공합니다.  
  
### <a name="named-instance-creation"></a>명명된 인스턴스 만들기  
 사용자는 LocalDB 관리 API를 통해 명시적으로 명명된 인스턴스를 만들거나, 관리 애플리케이션에 대한 app.config 파일을 통해 암시적으로 만들어야 합니다. 관리 애플리케이션은 API를 사용할 수도 있습니다.  
  
 명명된 각각의 인스턴스에는 연결된 LocalDB 버전이 있습니다. 즉, 지정된 LocalDB 이진 파일 집합을 가리킵니다. 명명된 인스턴스의 버전은 인스턴스를 만드는 과정에서 설정됩니다.  
  
### <a name="named-instance-naming-rules"></a>명명된 인스턴스 명명 규칙  
 LocalDB 인스턴스 이름은 최대 128 자까지 사용할 수 있습니다. 제한은 **sysname** 데이터 형식에 의해 적용 됩니다. 이는 NetBIOS 이름이 16자의 ASCII 문자로 제한되는 기존 SQL Server 인스턴스 이름과 비교할 때 중요한 차이점입니다. 이러한 차이가 있는 이유는 LocalDB는 데이터베이스를 파일로 처리 하므로 파일 기반 의미 체계를 의미 하기 때문에 사용자가 인스턴스 이름을 자유롭게 선택할 수 있기 때문입니다.  
  
 LocalDB 인스턴스 이름은 파일 이름 구성 요소에 적합한 모든 유니코드 문자를 포함할 수 있습니다. 파일 이름 구성 요소에 잘못 된 문자가 포함 되는 경우 일반적으로 ASCII/Unicode 문자 1부터 31 까지의 문자, 따옴표 ("), 보다 작음\<(), 보다 큼 (>), 파이프 (|), 백스페이스 (\b), 탭 (\t), 콜론 (:), 별표 (*), 물음표 (?), 백슬래시 (\\) 및 슬래시 (/)를 전달 합니다. null 문자(\0)는 문자열 종료를 나타내는 데 사용되므로 허용됩니다. 첫 번째 null 문자 뒤의 모든 문자가 무시됩니다.  
  
> [!NOTE]  
>  부적합한 문자 목록은 운영 체제에 따라 다르며 이후 릴리스에서 변경될 수 있습니다.  
  
 인스턴스 이름의 선행 공백과 후행 공백은 무시되므로 제거됩니다.  
  
 이름 충돌을 방지 하기 위해 앞의 "자동 인스턴스 명명 규칙"에서 설명한 것 처럼 명명 된 LocalDB 인스턴스는 자동 인스턴스의 명명 패턴을 따르는 이름을 가질 수 없습니다. 자동 인스턴스 명명 패턴을 따르는 이름을 사용 하 여 명명 된 인스턴스를 만들려고 하면 기본 인스턴스가 효과적으로 만들어집니다.  
  
## <a name="sql-server-express-localdb-reference-topics"></a>SQL Server Express LocalDB 참조 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
 LocalDB 인스턴스 API를 찾을 수 있도록 헤더 파일 정보와 레지스트리 키를 제공합니다.  
  
 [명령줄 관리 도구: SqlLocalDB.exe](../../relational-databases/express-localdb-instance-apis/command-line-management-tool-sqllocaldb-exe.md)  
 명령줄에서 LocalDB 인스턴스를 관리하는 도구인 SqlLocalDB.exe에 대해 설명합니다.  
  
 [LocalDBCreateInstance 함수](../../relational-databases/express-localdb-instance-apis/localdbcreateinstance-function.md)  
 새 LocalDB 인스턴스를 만드는 함수에 대해 설명합니다.  
  
 [LocalDBDeleteInstance 함수](../../relational-databases/express-localdb-instance-apis/localdbdeleteinstance-function.md)  
 LocalDB 인스턴스를 제거하는 함수에 대해 설명합니다.  
  
 [LocalDBFormatMessage 함수](../../relational-databases/express-localdb-instance-apis/localdbformatmessage-function.md)  
 LocalDB 오류에 대한 지역화된 설명을 반환하는 함수에 대해 설명합니다.  
  
 [LocalDBGetInstanceInfo 함수](../../relational-databases/express-localdb-instance-apis/localdbgetinstanceinfo-function.md)  
 LocalDB 인스턴스의 존재 여부, 버전 정보, 실행 여부 등과 같은 LocalDB 관련 정보를 가져오는 함수에 대해 설명합니다.  
  
 [LocalDBGetInstances 함수](../../relational-databases/express-localdb-instance-apis/localdbgetinstances-function.md)  
 지정된 버전의 모든 LocalDB 인스턴스를 반환하는 함수에 대해 설명합니다.  
  
 [LocalDBGetVersionInfo 함수](../../relational-databases/express-localdb-instance-apis/localdbgetversioninfo-function.md)  
 지정된 LocalDB 버전에 대한 정보를 반환하는 함수를 설명합니다.  
  
 [LocalDBGetVersions 함수](../../relational-databases/express-localdb-instance-apis/localdbgetversions-function.md)  
 컴퓨터에서 사용할 수 있는 모든 LocalDB 버전을 반환하는 함수에 대해 설명합니다.  
  
 [LocalDBShareInstance 함수](../../relational-databases/express-localdb-instance-apis/localdbshareinstance-function.md)  
 지정된 LocalDB 인스턴스를 공유하는 함수에 대해 설명합니다.  
  
 [LocalDBStartInstance 함수](../../relational-databases/express-localdb-instance-apis/localdbstartinstance-function.md)  
 지정된 LocalDB 인스턴스를 시작하는 함수에 대해 설명합니다.  
  
 [LocalDBStartTracing 함수](../../relational-databases/express-localdb-instance-apis/localdbstarttracing-function.md)  
 사용자에 대한 API 추적을 사용하도록 설정하는 함수를 설명합니다.  
  
 [LocalDBStopInstance 함수](../../relational-databases/express-localdb-instance-apis/localdbstopinstance-function.md)  
 지정된 LocalDB 인스턴스를 중지하는 함수에 대해 설명합니다.  
  
 [LocalDBStopTracing 함수](../../relational-databases/express-localdb-instance-apis/localdbstoptracing-function.md)  
 사용자에 대한 API 추적을 사용하지 않도록 설정하는 함수를 설명합니다.  
  
 [LocalDBUnshareInstance 함수](../../relational-databases/express-localdb-instance-apis/localdbunshareinstance-function.md)  
 지정된 LocalDB 인스턴스 공유를 중지하는 함수에 대해 설명합니다.  
  
  
