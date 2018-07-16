---
title: SQL Server의 최대 용량 사양 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 76
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 08997fa0dd4fe66b4e3c22fd6447105d11991c29
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37296043"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>SQL Server의 최대 용량 사양
  다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소에 정의된 다양한 개체의 최대 크기 및 개수를 보여 줍니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기술과 관련된 표로 이동하려면 해당 링크를 클릭합니다.  
  
 [SQL Server 데이터베이스 엔진 개체](#Engine)  
  
 [SQL Server 유틸리티 개체](#Utility)  
  
 [SQL Server 데이터 계층 응용 프로그램 개체](#DAC)  
  
 [SQL Server 복제 개체](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] 개체  
 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 정의되거나 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 참조되는 다양한 개체의 최대 크기 및 개수를 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 개체(object)|최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 비트)|최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64비트)|  
|---------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|일괄 처리 크기<br /><br /> 참고: 네트워크 패킷 크기는 응용 프로그램과 관계형 간의 통신에 사용 되는 tabular data stream (TDS) 패킷의 크기 [!INCLUDE[ssDE](../includes/ssde-md.md)]합니다. 기본 패킷 크기는 4KB이며 네트워크 패킷 크기 구성 옵션으로 제어됩니다.|65,536 * 네트워크 패킷 크기|65,536 * 네트워크 패킷 크기|  
|짧은 문자열 열당 바이트 수|8,000|8,000|  
|GROUP BY, ORDER BY당 바이트 수|8,060|8,060|  
|인덱스 키당 바이트 수<br /><br /> 참고: 최대 인덱스 키의 바이트 수 900을 초과할 수 없습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 해당 열에서 900바이트 이상의 데이터로 삽입한 행이 없는 경우 최대 900바이트 이상까지 추가할 수 있는 크기의 가변 길이 열을 사용하여 키를 정의할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 비클러스터형 인덱스에 키가 아닌 열을 포함시켜 900바이트의 최대 인덱스 키 크기 제한을 피할 수 있습니다.|900|900|  
|외래 키당 바이트 수|900|900|  
|기본 키당 바이트 수|900|900|  
|행당 바이트 수<br /><br /> 참고:<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 가변 길이 열을 행 외부로 밀어넣을 수 있는 행 오버플로 저장소를 지원합니다. 행 외부로 밀어넣은 가변 길이 열의 주 레코드에는 24바이트의 루트만 저장됩니다. 이 때문에 유효 행 제한은 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]보다 높습니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서의 "8KB를 초과하는 행 오버플로 데이터" 항목을 참조하십시오.|8,060|8,060|  
|메모리 최적화 테이블의 행당 바이트 수<br /><br /> 참고:<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 메모리 내 OLTP는 행 오버플로 저장소를 지원 하지 않습니다. 가변 길이 열은 행에 밀어넣어지지 않습니다 이 때문에 메모리 최적화 테이블에서 지정할 수 있는 가변 길이 열의 최대 너비가 최대 행 크기로 제한됩니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)를 참조하세요.|지원되지 않음|8,060|  
|저장 프로시저의 원본 텍스트의 바이트 수|일괄 처리 크기 또는 250MB 미만|일괄 처리 크기 또는 250MB 미만|  
|`varchar(max)`, `varbinary(max)`, `xml`, `text` 또는 `image` 열당 바이트 수|2^31-1|2^31-1|  
|`ntext` 또는 `nvarchar(max)` 열당 문자 수|2^30-1|2^30-1|  
|테이블당 클러스터형 인덱스 수|1|1|  
|GROUP BY, ORDER BY의 열 수|바이트 수로만 제한|바이트 수로만 제한|  
|GROUP BY WITH CUBE 또는 WITH ROLLUP 문의 열 또는 식의 수|10|10|  
|인덱스 키당 열 수<br /><br /> 참고: 테이블에 하나 이상의 XML 인덱스가 있으면 사용자 테이블의 클러스터링 키 이므로 15 개 열으로 제한 XML 열이 기본 XML 인덱스의 클러스터링 키에 추가 됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 최대 16 개의 키 열 제한을 피할 비클러스터형 인덱스에 키가 아닌 열을 포함할 수 있습니다. 자세한 내용은 [Create Indexes with Included Columns](../relational-databases/indexes/create-indexes-with-included-columns.md)을 참조하세요.|16|16|  
|외래 키당 열 수|16|16|  
|기본 키당 열 수|16|16|  
|넓지 않은 테이블당 열 수|1,024|1,024|  
|넓은 테이블당 열 수|30,000|30,000|  
|SELECT 문당 열 수|4,096|4,096|  
|INSERT 문당 열 수|4096|4096|  
|클라이언트당 연결 수|구성된 연결의 최대 값|구성된 연결의 최대 값|  
|데이터베이스 크기|524,272TB|524,272TB|  
|다음 인스턴스당 데이터베이스 수: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|32,767|32,767|  
|데이터베이스당 파일 그룹 수|32,767|32,767|  
|메모리 최적화 데이터의 데이터베이스당 파일 그룹 수|지원되지 않음|1|  
|데이터베이스당 파일 수|32,767|32,767|  
|파일 크기(데이터)|16TB|16TB|  
|파일 크기(로그)|2TB|2TB|  
|데이터베이스당 메모리 최적화 데이터의 데이터 파일 수|지원되지 않음|4.096|  
|메모리 최적화 데이터의 데이터 파일당 델타 파일|지원되지 않음|1|  
|테이블당 외래 키 테이블 참조 수<br /><br /> 참고: 테이블에서 FOREIGN KEY 제약 조건의 무제한을 포함할 수 있지만 권장 되는 최대는 253 개입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 호스팅하는 하드웨어 구성에 따라 FOREIGN KEY 제약 조건을 이보다 더 많이 지정하면 쿼리 최적화 프로그램의 처리 성능이 떨어질 수 있습니다.|253|253|  
|식별자 길이(문자 수)|128|128|  
|컴퓨터당 인스턴스 수|모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전에 대해 독립 실행형 서버당 50개의 인스턴스<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 25 개의 인스턴스를 장애 조치 클러스터 설치를 위한 저장된 옵션으로 공유 클러스터 디스크를 사용 하는 경우 클러스터를 지원 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 클러스터 설치를 위한 스토리지 옵션으로 SMB를 선택 하는 경우 50 개의 인스턴스를 장애 조치 클러스터에서 지 원하는 파일 공유 자세한 내용은 [Hardware and Software Requirements for Installing SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)합니다.|독립 실행형 서버당 50개의 인스턴스<br /><br /> 클러스터 설치를 위한 저장 옵션으로 공유 클러스터 디스크를 사용하는 경우 장애 조치(failover) 클러스터에 25개의 인스턴스. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 클러스터 설치를 위한 스토리지 옵션으로 SMB 파일 공유 위치를 선택하는 경우 장애 조치(failover) 클러스터에 50개의 인스턴스를 지원합니다.|  
|메모리 최적화 테이블당 인덱스 수|지원되지 않음|8|  
|SQL 문이 포함된 문자열의 길이(일괄 처리 크기)<br /><br /> 참고: 네트워크 패킷 크기는 응용 프로그램과 관계형 간의 통신에 사용 되는 tabular data stream (TDS) 패킷의 크기 [!INCLUDE[ssDE](../includes/ssde-md.md)]합니다. 기본 패킷 크기는 4KB이며 네트워크 패킷 크기 구성 옵션으로 제어됩니다.|65,536 * 네트워크 패킷 크기|65,536 * 네트워크 패킷 크기|  
|연결당 잠금 수|서버당 최대 잠금 수|서버당 최대 잠금 수|  
|다음 인스턴스당 잠금 수: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> 참고:이 값 정적 잠금 할당입니다. 동적 잠금은 메모리로만 제한됩니다.|최대 2,147,483,647|메모리로만 제한|  
|중첩 저장 프로시저 수준 수<br /><br /> 참고: 저장된 프로시저에서 64 개 이상의 데이터베이스 또는 인터리빙 시 3 개 이상의 데이터베이스를 액세스할 경우 오류가 표시 됩니다.|32|32|  
|중첩 하위 쿼리 수|32|32|  
|중첩 트리거 수준 수|32|32|  
|테이블당 비클러스터형 인덱스 수|999|999|  
|CUBE, ROLLUP, GROUPING SETS, WITH CUBE, WITH ROLLUP 중 하나가 사용되는 경우 GROUP BY 절의 개별 식 수|32|32|  
|GROUP BY 절의 연산자에 의해 생성되는 그룹화 집합 수|4,096|4,096|  
|저장 프로시저당 매개 변수 개수|2,100|2,100|  
|사용자 정의 함수당 매개 변수 개수|2,100|2,100|  
|테이블당 REFERENCES 수|253|253|  
|테이블당 행 수|사용 가능한 저장소로 제한|사용 가능한 저장소로 제한|  
|데이터베이스당 테이블 수<br /><br /> 참고: 데이터베이스 개체는 테이블, 뷰, 저장된 프로시저, 사용자 정의 함수, 트리거, 규칙, 기본값 및 제약 조건 같은 개체를 포함 합니다. 한 데이터베이스에서 모든 개체 수의 합계는 2,147,483,647을 초과할 수 없습니다.|데이터베이스의 개체 수로 제한|데이터베이스의 개체 수로 제한|  
|분할된 테이블 또는 인덱스당 파티션 수|1,000<br /><br /> **\*\* 중요 \* \* ** 1,000 개 이상의 파티션이 있는 테이블 또는 인덱스를 만드는 32 비트 시스템에서 가능 하지만 지원 되지 않습니다.|15,000|  
|인덱싱되지 않은 열의 통계|30,000|30,000|  
|SELECT 문당 테이블 수|사용 가능한 리소스로만 제한|사용 가능한 리소스로만 제한|  
|테이블당 트리거 수<br /><br /> 참고: 데이터베이스 개체는 테이블, 뷰, 저장된 프로시저, 사용자 정의 함수, 트리거, 규칙, 기본값 및 제약 조건 같은 개체를 포함 합니다. 한 데이터베이스에서 모든 개체 수의 합계는 2,147,483,647을 초과할 수 없습니다.|데이터베이스의 개체 수로 제한|데이터베이스의 개체 수로 제한|  
|UPDATE 문 당 열 수(넓은 테이블)|4096|4096|  
|사용자 연결|32,767|32,767|  
|XML 인덱스|249|249|  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 개체  
 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티에서 테스트된 다양한 개체의 최대 크기 및 개수를 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 개체|최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 비트)|최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64비트)|  
|----------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티당 컴퓨터(물리적 컴퓨터 또는 가상 컴퓨터) 수|100|100|  
|컴퓨터당 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 인스턴스 수|5|5|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티당 총 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 수|200*|200*|  
|데이터 계층 응용 프로그램을 포함하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 인스턴스당 사용자 데이터베이스 수|50|50|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티당 총 사용자 데이터베이스 수|1,000|1,000|  
|데이터베이스당 파일 그룹 수|1|1|  
|파일 그룹당 데이터 파일 수|1|1|  
|데이터베이스당 로그 파일 수|1|1|  
|컴퓨터당 볼륨 수|3|3|  
  
 * 관리 되는 인스턴스의 최대 수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 지 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티는 서버의 하드웨어 구성에 따라 달라질 수 있습니다. 시작 정보는 [SQL Server 유틸리티 기능 및 태스크](../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 제어 지점은 일부 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 계층 응용 프로그램 개체  
 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC(데이터 계층 응용 프로그램)에서 테스트된 다양한 개체의 최대 크기 및 개수를 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC 개체|최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 비트)|최대 크기/개수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64비트)|  
|------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|DAC당 데이터베이스 수|1|1|  
|DAC당 개체 수*|데이터베이스의 개체 수 또는 사용 가능한 메모리로 제한|데이터베이스의 개체 수 또는 사용 가능한 메모리로 제한|  
  
 *제한에 포함된 개체의 유형은 사용자, 테이블, 뷰, 저장 프로시저, 사용자 정의 함수, 사용자 정의 데이터 형식, 데이터베이스 역할, 스키마 및 사용자 정의 테이블 형식입니다.  
  
##  <a name="Replication"></a> 복제 개체  
 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 복제에 정의된 다양한 개체의 최대 크기 및 개수를 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Replication 개체|최대 크기/개수 SQL Server(32비트)|최대 크기/개수 SQL Server(64비트)|  
|--------------------------------------------------|---------------------------------------------------|---------------------------------------------------|  
|아티클 수(병합 게시)|256|256|  
|아티클 수(스냅숏 또는 트랜잭션 게시)|32,767|32,767|  
|테이블의 열 수*(병합 게시)|246|246|  
|테이블의 열 수**([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스냅숏 또는 트랜잭션 게시)|1,000|1,000|  
|테이블의 열 수**(Oracle 스냅숏 또는 트랜잭션 게시)|995|995|  
|행 필터에 사용되는 열의 바이트 수(병합 게시)|1,024|1,024|  
|행 필터에 사용되는 열의 바이트 수(스냅숏 또는 트랜잭션 게시)|8,000|8,000|  
  
 *충돌 검색에 행 추적이 사용될 경우(기본값) 기본 테이블은 최대 1,024개의 열을 포함할 수 있지만 최대 246개의 열이 게시되도록 아티클에서 열을 필터링해야 합니다. 열 추적을 사용하면 기본 테이블은 최대 246개의 열을 포함할 수 있습니다.  
  
 **기본 테이블은 게시 데이터베이스에 허용되는 최대 열 수( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 경우 1,024개)를 포함할 수 있지만 열이 게시 유형에 지정된 최대 열 수를 초과하는 경우 아티클에서 열을 필터링해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Hardware and Software Requirements for Installing SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [시스템 구성 검사기의 검사 매개 변수](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [SQL Server 유틸리티 기능 및 태스크](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
