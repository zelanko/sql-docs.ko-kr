---
title: 자동 증가가 켜져 모든 데이터 및 로그 파일에 대 한 업그레이드 프로세스 중 확인 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log files [SQL Server], size
- data files [SQL Server], size
- tempdb [SQL Server], size
- autogrow [SQL Server]
ms.assetid: a5860904-e2be-4224-8a51-df18a10d3fb9
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b903e8f22fce7404f418cfc0a81ac81e954ab06f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079460"
---
# <a name="verify-autogrow-is-turned-on-for-all-data-and-log-files-during-the-upgrade-process"></a>업그레이드 프로세스 중에 모든 데이터 및 로그 파일에 자동 증가 기능이 설정되어 있는지 확인합니다.
  업그레이드 관리자가 자동 증가로 설정되지 않은 데이터 또는 로그 파일을 검색했습니다. 새로운 기능과 향상 된 기능은 사용자 데이터베이스에 대 한 추가 디스크 공간이 필요 하며 **tempdb** 시스템 데이터베이스입니다. 리소스 업그레이드 및 후속 프로덕션 작업 중에 크기 증가 수용할 수 있도록 모든 사용자 데이터 및 로그 파일에 대 한 자동 증가 ON으로 설정 권장 및 **tempdb** 업그레이드 하기 전에 데이터 및 로그 파일입니다.  
  
 작업을 업그레이드하고 테스트한 후 자동 증가를 해제하거나 사용자 데이터 및 로그 파일에 따라 FILEGROWTH 증가분을 적절히 조정할 수 있습니다. 에 대해서는 자동 증가를 계속 하는 것이 좋습니다는 **tempdb** 시스템 데이터베이스입니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "tempdb의 용량 계획"을 참조하십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 **데이터 파일**  
  
 다음 표에서는 사용자 정의 데이터 파일에 대한 추가 디스크 공간 요구 사항을 유발하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 변경 내용을 나열합니다.  
  
|기능|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 변경 내용|  
|-------------|-----------------------------------------------------|  
|전체 텍스트|문서 ID(DOCID) 맵이 전체 텍스트 카탈로그 대신 데이터 파일에 저장됩니다.|  
|`text`, `ntext` 및 `image` 열|`text`, `ntext` 또는 `image` 데이터 형식으로 정의된 LOB(Large Object) 열은 열당 40바이트의 디스크 공간이 추가로 필요합니다. 이러한 디스크 증가는 각 LOB 열을 처음 업데이트할 때 한 번만 발생합니다.|  
|메타데이터|각 사용자 데이터베이스의 PRIMARY 파일 그룹에 데이터베이스 개체 및 사용자 권한에 대한 추가 시스템 메타데이터가 생성되어 유지 관리됩니다. 예를 들어 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 권한을 허가한 사용자 또는 권한을 허가 받은 사용자와 관련된 사용 권한이 단일 행에 비트맵으로 저장됩니다. 비트맵이 여러 개의 행으로 확장됩니다.<br /><br /> 업그레이드 프로세스 중에 기존 메타데이터와 새로운 메타데이터를 모두 저장할 수 있는 디스크 공간이 있어야 합니다. 기존 메타데이터는 업그레이드가 완료된 후 삭제됩니다.|  
  
 **트랜잭션 로그 파일**  
  
 다음 표에서는 사용자 정의 트랜잭션 로그 파일에 대한 추가 디스크 공간 요구 사항을 유발하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 변경 내용을 나열합니다.  
  
|기능|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 변경 내용|  
|-------------|-----------------------------------------------------|  
|복원 및 복구|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 충돌 복구의 실행 취소 단계에서 사용자가 데이터베이스에 액세스할 수 있습니다. 이는 충돌이 발생했을 때 커밋되지 않은 트랜잭션이 충돌 전에 유지하던 잠금을 다시 획득하기 때문에 가능합니다. 잠금은 트랜잭션이 롤백되는 동안 사용자의 다른 작업이 발생하지 않도록 트랜잭션을 보호합니다. 이 추가 잠금 정보를 트랜잭션 로그에 유지해야 합니다.|  
  
 **tempdb 데이터 및 로그 파일**  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **tempdb** 데이터베이스는 다음 개체를 저장 하는 데 사용 됩니다.  
  
-   테이블, 저장 프로시저, 테이블 변수, 커서와 같이 명시적으로 생성된 임시 개체  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 의해 생성된 내부 작업 테이블  
  
-   인덱스를 만들거나 다시 작성할 때 임시 정렬의 결과(SORT_IN_TEMPDB가 지정된 경우)  
  
 추가 개체도 사용 된 **tempdb** 데이터베이스입니다. 다음 표에서 변경 하거나 추가한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 추가 유발 하는 데 필요한 디스크 공간 **tempdb** 데이터 및 로그 파일입니다.  
  
|기능|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 변경 내용|  
|-------------|-----------------------------------------------------|  
|행 버전 관리|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 행 버전 관리는 다음에 대해 사용되는 일반적인 방법입니다.<br /><br /> 트리거는 지원: 트리거에서 inserted 및 deleted 테이블을 작성 합니다. 트리거에 의해 수정된 모든 행의 버전이 지정됩니다. 여기에는 트리거를 실행한 문에 의해 수정된 행과 트리거에 의해 수정된 모든 데이터가 포함됩니다. 버전 저장소를 사용 하는 트리거 후 **tempdb** 보유 하는 트리거에 의해 변경 된 행의 이전 이미지입니다. 트리거가 설정된 경우 데이터를 대량 로드하면 각 행의 복사본이 버전 저장소에 추가됩니다.<br /><br /> MARS(Multiple Active Result Sets) 지원. 활성 결과 집합이 있을 때 MARS 세션에서 INSERT, UPDATE 또는 DELETE와 같은 데이터 수정 문을 실행하면 이 수정 문의 영향을 받는 행의 버전이 지정됩니다.<br /><br /> ONLINE 옵션을 지정하는 인덱스 작업 지원 온라인 인덱스 작업은 행 버전 관리를 사용하여 다른 트랜잭션에서 수정하는 내용의 영향을 받지 않습니다. 따라서 이미 읽은 행에 대한 공유 잠금을 요청할 필요가 없습니다. 또한, 사용자가 동시에 업데이트 및 삭제 하는 동안 온라인 인덱스 작업의 버전 레코드를 위한 공간이 필요 **tempdb**합니다.<br /><br /> 행 버전 관리 기반의 트랜잭션 격리 수준을 지원 하 고: 읽기 새롭게 구현한 커밋된 행 버전 관리를 사용 하 여 문 수준의 읽기 일관성을 제공 하는 격리 수준입니다. 트랜잭션 수준의 읽기 일관성을 유지하는 새로운 스냅숏 격리 수준<br /><br /> <br /><br /> 행 버전에서 실행 되는 **tempdb** 버전 행 버전 관리 기반 격리 수준에서 실행 되는 트랜잭션의 요구 사항을 만족할 때까지 저장 합니다.<br /><br /> 행 버전 관리와 버전 저장소에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "행 버전 관리 기반 격리 수준 이해" 항목을 참조하십시오.|  
|임시 테이블 및 임시 변수 메타데이터의 캐싱|임시 테이블 및 임시 변수에서 메타 데이터 캐시에 캐시 되는 모든 메타 데이터에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 두 개의 추가 페이지가 할당 되 **tempdb**합니다.<br /><br /> 저장 프로시저 또는 트리거가 임시 테이블이나 임시 변수를 만드는 경우 해당 프로시저 또는 트리거의 실행이 완료되었을 때 임시 개체는 삭제되지 않습니다. 대신 임시 개체는 한 페이지로 잘리고 프로시저 또는 트리거가 다음 번 실행될 때 다시 사용됩니다.|  
|분할된 테이블의 인덱스|경우는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 각 파티션의 중간 정렬 실행에 필요한 보관 하기에 충분 한 공간 분할 된 인덱스를 작성 하기 위해 정렬을 수행할 **tempdb** SORT_IN_TEMPDB 인덱스 옵션이 지정 된 경우.|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 명시적으로 사용 하 여 **tempdb** (대화 당 약 1 KB) 메모리에 보관할 수 없는 기존 대화 컨텍스트를 보존할 때.<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] 암시적으로 사용 하 여 **tempdb** 쿼리 실행의 컨텍스트에서 개체의 캐싱을 통해 합니다. 타이머 이벤트 및 백그라운드에 전달된 대화에 사용되는 작업 테이블).<br /><br /> DBMail, 이벤트 알림 및 쿼리 알림 기능은 암시적으로 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용합니다.|  
|LOB(Large object) 데이터 형식<br /><br /> LOB 변수 및 매개 변수|데이터 형식 `varchar(max)`, `nvarchar(max)`, **varbinary (max) 텍스트**, `ntext`, `image,` 및 `xml` 큰 개체 형식입니다.<br /><br /> 데이터베이스에서 행 버전 관리 기반의 트랜잭션 격리 수준을 사용은 대형 개체를 수정 하면 LOB의 변경된 된 조각이 버전 저장소로 복사 됩니다 **tempdb**합니다.<br /><br /> 에 저장 된 큰 개체 데이터 형식으로 정의 된 매개 변수 **tempdb**합니다.|  
|CTE(공통 테이블 식)|결과, 스풀 작업에 대 한 임시 작업 테이블에서 생성 됩니다 **tempdb** 공통 테이블 식 쿼리를 실행 하면 됩니다.|  
  
## <a name="corrective-action"></a>수정 동작  
 데이터 또는 로그 파일이 자동 증가하도록 설정하려면 다음 문을 수정하여 데이터베이스에 대한 데이터 및 로그를 지정합니다. FILEGROWTH 증분을 현재 환경에 적합한 값으로 조정해야 합니다.  
  
```  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = tempdev,  
    FILEGROWTH = 20MB);  
GO  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = templog,  
    FILEGROWTH = 10MB);  
```  
  
 데이터 파일의 기본 증가분은 1MB입니다. 로그 파일 기본값은 10%입니다. FILEGROWTH 증분을 설정할 때 다음 일반 지침을 따르는 것이 좋습니다.  
  
|파일 크기|FILEGROWTH 증분|  
|---------------|--------------------------|  
|0 ~ 50 MB|10 MB|  
|100-200MB|20MB|  
|500MB 이상|10%|  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
