---
title: SQL Server의 최대 용량 사양 | Microsoft 문서
ms.date: 11/06/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- objects [SQL Server]
- number capacity specifications [SQL Server]
- size [SQL Server], capacity specifications
- number of objects
- capacity specifications [SQL Server]
- maximum capacity specifications [SQL Server]
- size [SQL Server]
- replication capacity specifications [SQL Server]
- objects [SQL Server], capacity specifications
- Database Engine [SQL Server], capacity specifications
ms.assetid: 13e95046-0e76-4604-b561-d1a74dd824d7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 08097b4aac0d14a3da21443a4903df90797b9316
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71687366"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>SQL Server의 최대 용량 사양
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  다음 표에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소에 정의된 다양한 개체의 최대 크기 및 수가 지정되어 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기술과 관련된 표로 이동하려면 해당 링크를 클릭합니다.  
  
 [SQL Server 데이터베이스 엔진 개체](#Engine)  
  
 [SQL Server 유틸리티 개체](#Utility)  
  
 [SQL Server 데이터 계층 애플리케이션 개체](#DAC)  
  
 [SQL Server 복제 개체](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] 개체  
 다음 표에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 정의되거나 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 참조되는 다양한 개체의 최대 크기 및 개수가 나와 있습니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 개체(object)||최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64비트)|추가 정보|  
|---------------------------------------------------------|-|------------------------------------------------------------------|----------------------------|  
|일괄 처리 크기||65,536 * 네트워크 패킷 크기|네트워크 패킷 크기는 애플리케이션과 관계형 [!INCLUDE[ssDE](../includes/ssde-md.md)]간의 통신에 사용되는 TDS(Tabular Data Stream) 패킷의 크기입니다. 기본 패킷 크기는 4KB이며 네트워크 패킷 크기 구성 옵션으로 제어됩니다.|  
|짧은 문자열 열당 바이트 수||8,000||  
|GROUP BY, ORDER BY당 바이트 수||8,060||  
|인덱스 키당 바이트 수||클러스터형 인덱스의 경우 900바이트, 비클러스터형 인덱스의 경우 1,700바이트|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 클러스터형 인덱스 키의 최대 바이트 수는 900을 초과할 수 없습니다. 비클러스터형 인덱스 키에 대한 최대값은 1700바이트입니다.<br /><br /> 최대 크기가 제한을 초과하는 가변 길이 열을 사용하여 키를 정의할 수 있습니다. 그러나 이러한 열에 있는 데이터의 총 크기는 제한을 초과할 수 없습니다.<br /><br /> 비클러스터형 인덱스에 키가 아닌 열을 추가로 포함할 수 있으며 해당 열은 키의 크기 제한에 포함되지 않습니다. 키가 아닌 열은 일부 쿼리의 성능 향상에 도움이 될 수 있습니다.|  
|메모리 최적화 테이블의 인덱스 키당 바이트 수||비클러스터형 인덱스의 경우 2500바이트 모든 인덱스가 행에 맞기만 하면 해시 인덱스에 대한 제한은 없습니다.|메모리 최적화 테이블의 비클러스터형 인덱스에는 선언된 최대 크기가 2500바이트를 초과하는 키 열을 포함할 수 없습니다. 키 열의 실제 데이터가 선언된 최대 크기보다 짧은지 여부는 관련이 없습니다.<br /><br /> 해시 인덱스 키에 대한 하드 크기 제한은 없습니다.<br /><br /> 메모리 최적화 테이블의 인덱스는 기본적으로 모든 열을 처리하기 때문에 포괄 열의 개념이 없습니다.<br /><br /> 메모리 최적화 테이블의 경우 행 크기가 8060바이트인 경우에도 일부 가변 길이 열이 물리적으로 8060바이트 외부에 저장될 수 있습니다. 그러나 테이블의 모든 인덱스에 대한 모든 키 열과 테이블의 추가 고정 길이 열의 선언된 최대 크기는 8060바이트에 맞아야 합니다.|  
|외래 키당 바이트 수||900||  
|기본 키당 바이트 수||900||  
|행당 바이트 수||8,060|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 가변 길이 열을 행 외부로 밀어 넣을 수 있는 행 오버플로 스토리지를 지원합니다. 행 외부로 밀어넣은 가변 길이 열의 주 레코드에는 24바이트의 루트만 저장됩니다. 이 때문에 유효 행 제한은 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]보다 높습니다. 자세한 내용은 [대용량 행 지원](../relational-databases/pages-and-extents-architecture-guide.md#large-row-support)을 참조하세요.|  
|메모리 최적화 테이블의 행당 바이트 수||8,060|[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 이상에서는 메모리 최적화 테이블이 행 외부 스토리지를 지원합니다. 테이블에 있는 모든 열의 최대 크기가 8060바이트를 초과할 경우 가변 길이 열이 행 외부로 푸시됩니다. 이는 컴파일 타임 결정입니다. 행 외부에 저장된 열의 경우 8바이트 참조만 행 내부에 저장됩니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)를 참조하세요.|  
|저장 프로시저의 원본 텍스트의 바이트 수||일괄 처리 크기 또는 250MB 미만||  
|**varchar(max)** , **varbinary(max)** , **xml**, **text**또는 **image** 열당 바이트 수||2^31-1||  
|**ntext** 또는 **nvarchar(max)** 열당 문자 수||2^30-1||  
|테이블당 클러스터형 인덱스 수||1||  
|GROUP BY, ORDER BY의 열 수||바이트 수로만 제한||  
|GROUP BY WITH CUBE 또는 WITH ROLLUP 문의 열 또는 식의 수||10||  
|인덱스 키당 열 수||32|테이블에 하나 이상의 XML 인덱스가 있는 경우 XML 열이 기본 XML 인덱스의 클러스터링 키에 추가되므로 사용자 테이블의 클러스터링 키는 31개 열로 제한됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 비클러스터형 인덱스에 키가 아닌 열을 포함시켜 최대 32개의 키 열 제한을 피할 수 있습니다. 자세한 내용은 [Create Indexes with Included Columns](../relational-databases/indexes/create-indexes-with-included-columns.md)을 참조하세요.|  
|외래 키 또는 기본 키당 열 수||32||  
|`INSERT` 문당 열 수||4,096||  
|`SELECT` 문당 열 수||4,096||  
|테이블당 열 수||1,024|스파스 열 집합을 포함하는 테이블에는 최대 30,000개의 열이 포함됩니다. [스파스 열 집합](../relational-databases/tables/use-column-sets.md)을 참조하세요.|  
|`UPDATE` 문당 열 수||4,096|[스파스 열 집합](../relational-databases/tables/use-column-sets.md)에는 다른 한도가 적용됩니다.|  
|뷰당 열 수||1,024||  
|클라이언트당 연결 수||구성된 연결의 최대 값||  
|데이터베이스 크기||524,272TB||  
|다음 인스턴스당 데이터베이스 수: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||32,767||  
|데이터베이스당 파일 그룹 수||32,767||  
|메모리 최적화 데이터의 데이터베이스당 파일 그룹 수||1||  
|데이터베이스당 파일 수||32,767||  
|파일 크기(데이터)||16TB||  
|파일 크기(로그)||2TB||  
|데이터베이스당 메모리 최적화 데이터의 데이터 파일 수||4,096([!INCLUDE[ssSQL14](../includes/ssSQL14-md.md)]). [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 최신 버전은 엄격한 제한을 적용하지 않습니다.||  
|메모리 최적화 데이터의 데이터 파일당 델타 파일||1||  
|테이블당 외래 키 테이블 참조 수||발신 = 253, 수신 = 10,000|제한 사항에 대해서는 [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md)를 참조하세요.|  
|식별자 길이(문자 수)||128||  
|컴퓨터당 인스턴스 수||독립 실행형 서버당 50개의 인스턴스<br /><br /> 클러스터 설치를 위한 저장 옵션으로 공유 클러스터 디스크를 사용하는 경우 장애 조치(failover) 클러스터에 25개의 인스턴스. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 클러스터 설치를 위한 스토리지 옵션으로 SMB 파일 공유 위치를 선택하는 경우 장애 조치(failover) 클러스터에 50개의 인스턴스를 지원합니다.||  
|메모리 최적화 테이블당 인덱스 수||999([!INCLUDE[ssSQL17](../includes/ssSQL17-md.md)]부터 및 [!INCLUDE[ssSDSFull](../includes/ssSDSFull-md.md)])<br/>8([!INCLUDE[ssSQL14](../includes/ssSQL14-md.md)] 및 [!INCLUDE[ssSQL15](../includes/ssSQL15-md.md)])||  
|SQL 문이 포함된 문자열의 길이(일괄 처리 크기)||65,536 * 네트워크 패킷 크기|네트워크 패킷 크기는 애플리케이션과 관계형 [!INCLUDE[ssDE](../includes/ssde-md.md)]간의 통신에 사용되는 TDS(Tabular Data Stream) 패킷의 크기입니다. 기본 패킷 크기는 4KB이며 네트워크 패킷 크기 구성 옵션으로 제어됩니다.|  
|연결당 잠금 수||서버당 최대 잠금 수||  
|다음 인스턴스당 잠금 수: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||메모리로만 제한|이 값은 정적 잠금 할당용입니다. 동적 잠금은 메모리로만 제한됩니다.|  
|중첩 저장 프로시저 수준 수||32|하나의 저장 프로시저가 65개 이상의 데이터베이스에 액세스하거나 인터리빙 시 3개 이상의 데이터베이스에 액세스할 경우 오류가 발생합니다.|  
|중첩 하위 쿼리 수||32||  
|중첩 트리거 수준 수||32||  
|테이블당 비클러스터형 인덱스 수||999||  
|CUBE, ROLLUP, GROUPING SETS, WITH CUBE, WITH ROLLUP 중 하나가 사용되는 경우 GROUP BY 절의 개별 식 수||32||  
|GROUP BY 절의 연산자에 의해 생성되는 그룹화 집합 수||4,096||  
|저장 프로시저당 매개 변수 개수||2,100||  
|사용자 정의 함수당 매개 변수 개수||2,100||  
|테이블당 REFERENCES 수||253||  
|테이블당 행 수||사용 가능한 스토리지로 제한||  
|데이터베이스당 테이블 수||데이터베이스의 개체 수로 제한|데이터베이스 개체에는 테이블, 뷰, 저장 프로시저, 사용자 정의 함수, 트리거, 규칙, 기본값 및 제약 조건 등의 개체가 있습니다. 한 데이터베이스에서 모든 개체 수의 합계는 2,147,483,647을 초과할 수 없습니다.|  
|분할된 테이블 또는 인덱스당 파티션 수||15,000||  
|인덱싱되지 않은 열의 통계||30,000|| 
|SELECT 문당 테이블 수||사용 가능한 리소스로만 제한||  
|테이블당 트리거 수||데이터베이스의 개체 수로 제한|데이터베이스 개체에는 테이블, 뷰, 저장 프로시저, 사용자 정의 함수, 트리거, 규칙, 기본값 및 제약 조건 등의 개체가 있습니다. 한 데이터베이스에서 모든 개체 수의 합계는 2,147,483,647을 초과할 수 없습니다.|  
|사용자 연결||32,767||  
|XML 인덱스||249||  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 개체  
 다음 표에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티에서 테스트된 다양한 개체의 최대 크기 및 개수가 나와 있습니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 개체||최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64비트)|  
|----------------------------------------------|-|------------------------------------------------------------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티당 컴퓨터(물리적 컴퓨터 또는 가상 컴퓨터) 수||100|  
|컴퓨터당 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 인스턴스 수||5|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티당 총 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 수||200*|  
|데이터 계층 애플리케이션을 포함하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 인스턴스당 사용자 데이터베이스 수||50|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티당 총 사용자 데이터베이스 수||1,000|  
|데이터베이스당 파일 그룹 수||1|  
|파일 그룹당 데이터 파일 수||1|  
|데이터베이스당 로그 파일 수||1|  
|컴퓨터당 볼륨 수||3|  
  
 \* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티에서 지원하는 관리되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 최대 개수는 서버의 하드웨어 구성에 따라 달라질 수 있습니다. 시작 정보는 [SQL Server 유틸리티 기능 및 태스크](../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 제어 지점은 일부 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]버전에서는 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](https://msdn.microsoft.com/library/cc645993.aspx)을 참조하세요.    
  
##  <a name="DAC"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 계층 애플리케이션 개체  
 다음 표에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC(데이터 계층 애플리케이션)에서 테스트된 다양한 개체의 최대 크기 및 개수가 나와 있습니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC 개체||최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64비트)|  
|------------------------------------------|-|------------------------------------------------------------------|  
|DAC당 데이터베이스 수||1|  
|DAC당 개체 수*||데이터베이스의 개체 수 또는 사용 가능한 메모리로 제한|  
  
 *제한에 포함된 개체의 유형은 사용자, 테이블, 뷰, 저장 프로시저, 사용자 정의 함수, 사용자 정의 데이터 형식, 데이터베이스 역할, 스키마 및 사용자 정의 테이블 형식입니다.  
  
##  <a name="Replication"></a> 복제 개체  
 다음 표에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 복제에 정의된 다양한 개체의 최대 크기 및 개수가 나와 있습니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Replication 개체||최대 크기/개수 SQL Server(64비트)|  
|--------------------------------------------------|-|---------------------------------------------------|  
|아티클 수(병합 게시)||2048|  
|아티클 수(스냅샷 또는 트랜잭션 게시)||32,767|  
|테이블의 열 수*(병합 게시)||246|  
|테이블의 열 수**([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스냅샷 또는 트랜잭션 게시)||1,000|  
|테이블의 열 수**(Oracle 스냅샷 또는 트랜잭션 게시)||995|  
|행 필터에 사용되는 열의 바이트 수(병합 게시)||1,024|  
|행 필터에 사용되는 열의 바이트 수(스냅샷 또는 트랜잭션 게시)||8,000|  

 *충돌 검색에 행 추적이 사용될 경우(기본값) 기본 테이블은 최대 1,024개의 열을 포함할 수 있지만 최대 246개의 열이 게시되도록 아티클에서 열을 필터링해야 합니다. 열 추적을 사용하면 기본 테이블은 최대 246개의 열을 포함할 수 있습니다.  
  
 **기본 테이블은 게시 데이터베이스에 허용되는 최대 열 수( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 경우 1,024개)를 포함할 수 있지만 열이 게시 유형에 지정된 최대 열 수를 초과하는 경우 아티클에서 열을 필터링해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [시스템 구성 검사기의 검사 매개 변수](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [SQL Server 유틸리티 기능 및 태스크](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
