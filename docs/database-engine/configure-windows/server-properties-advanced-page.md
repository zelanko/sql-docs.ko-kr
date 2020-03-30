---
title: 서버 속성(고급 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.advanced.f1
ms.assetid: cc5e65c2-448e-4f37-9ad4-2dfb1cc84ebe
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1672b245f061f521c9114bca71f723fe75553c96
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68025595"
---
# <a name="server-properties---advanced-page"></a>서버 속성 - 고급 페이지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 페이지를 사용하여 고급 서버 설정을 확인하거나 수정할 수 있습니다.  
  
 **서버 속성 페이지를 보려면**  
  
-   [서버 속성 보기 또는 변경&#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
## <a name="containment"></a>Containment  
 포함된 데이터베이스 사용  
 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 포함된 데이터베이스를 허용하는지 여부를 나타냅니다. **True**인 경우 포함된 데이터베이스를 만들거나 복구하거나 연결할 수 있습니다. **False**인 경우 포함된 데이터베이스를 만들거나 복구하거나 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 수 없습니다. 포함 속성을 변경하면 데이터베이스 보안에 영향을 줄 수 있습니다. 포함된 데이터베이스를 사용하면 데이터베이스 소유자에게 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한을 부여할 수 있습니다. 포함된 데이터베이스를 사용하지 않으면 사용자의 연결을 금지할 수 있습니다. 포함 속성의 영향을 이해하려면 [Contained Databases](../../relational-databases/databases/contained-databases.md) 및 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)을 참조하십시오.  
  
## <a name="filestream"></a>FILESTREAM  
 **FILESTREAM 액세스 수준**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 현재 FILESTREAM 지원 수준을 표시합니다. 액세스 수준을 변경하려면 다음 값 중 하나를 선택합니다.  
  
 **사용 안 함**  
 BLOB(Binary Large Object) 데이터를 파일 시스템에 저장할 수 없습니다. 이것은 기본값입니다.  
  
 **Transact-SQL 액세스 사용**  
 파일 시스템을 통해서가 아니라 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 FILESTREAM 데이터에 액세스할 수 있습니다.  
  
 **모든 액세스 사용**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 과 파일 시스템을 통해 FILESTREAM 데이터에 액세스할 수 있습니다.  
  
 처음으로 FILESTREAM을 사용하는 경우 컴퓨터를 다시 시작하여 드라이버를 구성해야 할 수 있습니다.  
  
 **FILESTREAM 공유 이름**  
 설치하는 동안 선택한 FILESTREAM 공유의 읽기 전용 이름을 표시합니다. 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
## <a name="miscellaneous"></a>기타  
 **다른 트리거를 발생시키는 트리거 허용**  
 다른 트리거를 발생시키는 트리거를 허용합니다. 트리거는 최대 32 수준까지 중첩될 수 있습니다. 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)의 "중첩 트리거" 섹션을 참조하세요.  
  
 **차단된 프로세스 임계값**  
 차단된 프로세스 보고서가 생성되는 임계값(초)입니다. 0에서 86,400 사이의 임계값을 설정할 수 있습니다. 기본적으로 차단된 프로세스 보고서는 생성되지 않습니다. 자세한 내용은 [blocked process threshold 서버 구성 옵션](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)을 참조하세요.  
  
 **커서 임계값**  
 커서 키 집합이 비동기적으로 생성되는 커서 집합의 행 수를 지정합니다. 커서에서 결과 집합에 대해 키 집합을 생성할 때 쿼리 최적화 프로그램은 해당 결과 집합으로 반환될 행 개수를 계산합니다. 쿼리 최적화 프로그램의 계산 결과, 반환된 행 개수가 이 임계값보다 크면 커서가 계속 채워지는 동안 사용자가 커서에서 행을 인출할 수 있도록 커서가 비동기적으로 생성됩니다. 그렇지 않으면 커서가 동기적으로 생성되어 모든 행이 반환될 때까지 쿼리가 기다립니다.  
  
 커서 임계값을 -1로 설정하면 모든 키 집합이 동기적으로 생성되므로 작은 커서 집합에 유리합니다. 0으로 설정하면 모든 커서 키 집합이 비동기적으로 생성됩니다. 다른 값을 사용하면 쿼리 최적화 프로그램이 커서 집합에 있는 예상 행 개수를 비교하여 이 값이 설정된 개수보다 많으면 비동기적으로 키 집합을 생성합니다. 자세한 내용은 [커서 임계값 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-cursor-threshold-server-configuration-option.md)을 참조하세요.  
  
 **기본 전체 텍스트 언어**  
 전체 텍스트 인덱싱된 열에 대한 기본 언어를 지정합니다. 전체 텍스트 인덱싱된 데이터의 언어 분석은 데이터의 언어에 따라 달라집니다. 이 옵션의 기본값은 서버의 언어입니다. 표시되는 설정에 해당하는 언어에 대한 자세한 내용은 [sys.fulltext_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)를 참조하세요.  
  
 **기본 언어**  
 따로 지정하지 않는 한 모든 새 로그인의 기본 언어입니다.  
  
 **전체 텍스트 업그레이드 옵션**  
 데이터베이스를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 업그레이드할 때 전체 텍스트 인덱스를 마이그레이션하는 방법을 제어합니다. 이 속성은 데이터베이스 복사 마법사를 사용하여 데이터베이스를 연결하거나, 데이터베이스 백업 및 파일 백업을 복원하거나, 데이터베이스를 복사하여 업그레이드에 적용됩니다.  
  
 대체 방법은 다음과 같습니다.  
  
 **가져오기**  
 전체 텍스트 카탈로그를 가져옵니다. 이 옵션은 **다시 작성**보다 훨씬 빠릅니다. 그러나 전체 텍스트 카탈로그를 가져오면 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에 새로 도입된 향상된 단어 분리기가 사용되지 않으므로 전체 텍스트 카탈로그를 다시 작성해야 할 수 있습니다.  
  
 전체 텍스트 카탈로그를 사용할 수 없는 경우 연결된 전체 텍스트 인덱스가 다시 작성됩니다. 이 옵션은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 대해서만 사용할 수 있습니다.  
  
 **다시 빌드**  
 향상된 새로운 단어 분리기를 사용하여 전체 텍스트 카탈로그를 다시 작성합니다. 인덱스를 다시 작성하면 시간이 오래 걸릴 수 있으며 업그레이드 후 CPU 및 메모리가 많이 필요할 수 있습니다.  
  
 **재설정**  
 전체 텍스트 카탈로그를 다시 설정합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 전체 텍스트 카탈로그 파일이 제거되지만 전체 텍스트 카탈로그 및 전체 텍스트 인덱스의 메타데이터는 유지됩니다. 업그레이드가 끝나면 모든 전체 텍스트 인덱스의 변경 내용 추적이 해제되고 탐색이 자동으로 시작되지 않습니다. 업그레이드가 완료된 후 전체 채우기를 수동으로 실행할 때까지 카탈로그가 비어 있습니다.  
  
 전체 텍스트 업그레이드 옵션을 선택하는 방법은 [전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)를 참조하세요.  
  
> [!NOTE]  
>  [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)upgrade_option 동작을 사용하여 전체 텍스트 업그레이드 옵션을 설정할 수도 있습니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 연결, 복원 또는 복사하면 데이터베이스를 바로 사용할 수 있으며 해당 데이터베이스가 자동으로 업그레이드됩니다. 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는 **전체 텍스트 업그레이드 옵션** 서버 속성의 설정에 따라 인덱스를 가져오거나, 다시 설정하거나, 다시 작성합니다. 업그레이드 옵션이 **가져오기** 또는 **다시 작성**으로 설정되어 있는 경우 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 **가져오기**로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다. **전체 텍스트 업그레이드 옵션** 속성 설정을 보거나 변경하는 방법은 [서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)을 참조하세요.  
  
 **최대 텍스트 복제 크기**  
 단일 INSERT, UPDATE, WRITETEXT 또는 UPDATETEXT 문에서 복제된 열 또는 캡처된 열에 추가할 수 있는 **text**, **ntext**, **varchar(max)** , **nvarchar(max)** , **xml**및 **image** 데이터의 최대 크기(바이트)를 지정합니다. 설정을 변경하면 즉시 적용됩니다. 자세한 내용은 [max text repl size 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)을 참조하세요.  
  
 **시작 프로시저 검색**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작할 때 저장 프로시저의 자동 실행을 검색하도록 지정합니다. 이 옵션을 **True**로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 서버에 정의된 자동 실행 저장 프로시저를 모두 검색하여 실행합니다. **False** (기본값)로 설정하면 검색을 수행하지 않습니다. 자세한 내용은 [scan for startup procs 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)을 참조하세요.  
  
 **두 자리 연도 구분**  
 두 자릿수 연도로 입력될 수 있는 최고 연도 수를 나타냅니다. 나열된 연도와 99 이하인 연도는 두 자릿수 연도로 입력될 수 있습니다. 모든 다른 연도는 네 자릿수 연도로 입력되어야 합니다.  
  
 예를 들어, 기본 설정이 2049이면 '49/3/14'로 입력된 날짜는 2049년 3월 14일로 해석되고 '50/3/14'로 입력된 날짜는 1950년 3월 14일로 해석되는 것을 나타냅니다. 자세한 내용은 [두 자리 연도 구분 구성 서버 구성 옵션](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.  
  
## <a name="network"></a>네트워크  
 **네트워크 패킷 크기**  
 전체 네트워크에서 사용되는 패킷 크기(바이트)를 설정합니다. 기본 패킷 크기는 4096바이트입니다. 애플리케이션에서 대량 복사 작업을 수행하거나 많은 양의 **text** 또는 **image** 데이터를 주고받을 때 패킷 크기를 기본값보다 크게 설정하면 네트워크에서 읽기 및 쓰기의 양이 줄어들므로 효율성이 향상될 수 있습니다. 애플리케이션이 적은 정보를 주거나 받을 때는 대부분의 데이터를 전송할 수 있도록 패킷 크기를 512바이트로 설정합니다. 자세한 내용은 [network packet size 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-network-packet-size-server-configuration-option.md)을 참조하세요.  
  
> [!NOTE]  
>  성능이 향상될 것이라는 확신이 없으면 패킷 크기를 변경하지 마세요. 대부분의 애플리케이션에는 기본 패킷 크기가 제일 좋습니다.  
  
 **원격 로그인 제한 시간**  
 실패한 원격 로그인 시도에서 원래 상태로 되돌아오기까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 기다리는 시간(초)을 지정합니다. 이 설정은 유형이 다른 쿼리를 위한 OLE DB Provider로의 연결에 영향을 줍니다. 기본값은 20초입니다. 값을 0으로 설정하면 무한정 기다릴 수 있습니다. 자세한 내용은 [remote login timeout 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)을 참조하세요.  
  
 설정을 변경하면 즉시 적용됩니다.  
  
## <a name="parallelism"></a>병렬 처리:  
 **병렬 처리에 대한 비용 임계값**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 쿼리에 대한 병렬 계획을 만들고 실행하는 데 사용되는 최소 비용 임계값을 지정합니다. 이 비용은 특정 하드웨어 구성에서 직렬 계획을 실행하는 데 필요한 예상 경과 시간(초)을 참조합니다. 이 옵션은 대칭 다중 프로세서에 대해서만 설정해야 합니다. 자세한 내용은 [병렬 처리에 대한 비용 임계값 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md)을 참조하세요.  
  
 **잠금**  
 사용 가능한 최대 잠금 수를 설정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 잠금에 사용하는 메모리 용량을 제한합니다. 기본 설정은 0이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시스템 요구 사항의 변화를 기준으로 동적으로 잠금을 할당하거나 할당을 취소할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 잠금을 동적으로 사용하는 것이 권장 구성입니다. 자세한 내용은 [locks 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)을 참조하세요.  
  
 **최대 병렬 처리 수준**  
 병렬 계획 실행에 사용할 프로세서의 수를 최대 64개로 제한합니다. 기본값 0으로 설정하면 사용 가능한 모든 프로세서를 사용합니다. 1로 설정하면 병렬 계획을 생성하지 않습니다. 1보다 큰 값으로 설정하면 단일 쿼리 실행에 사용되는 최대 프로세서 수가 제한됩니다. 사용 가능한 프로세서 수보다 더 큰 수를 지정하면 사용 가능한 실제 프로세서 수가 사용됩니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.  
  
 **쿼리 대기**  
 쿼리의 리소스 대기 시간을 초 단위(0 - 2147483647)로 지정합니다. 기본값 -1로 설정하면 제한 시간이 예상 쿼리 비용의 25배로 계산됩니다. 자세한 내용은 [query wait 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
