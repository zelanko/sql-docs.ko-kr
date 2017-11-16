---
title: "디스크 기반 테이블 저장소와 메모리 액세스에 최적화된 테이블 저장소 비교 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e1d68c71f727aefd0a95bb1e1c95d0a3fe77edb5
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="comparing-disk-based-table-storage-to-memory-optimized-table-storage"></a>디스크 기반 테이블 저장소와 메모리 액세스에 최적화된 테이블 저장소 비교
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
  
|범주|디스크 기반 테이블|메모리 액세스에 최적화된 내구성이 있는 테이블|  
|----------------|-----------------------|-------------------------------------|  
|DDL|메타데이터 정보는 데이터베이스의 기본 파일 그룹에 있는 시스템 테이블에 저장되고 카탈로그 보기를 통해 액세스할 수 있습니다.|메타데이터 정보는 데이터베이스의 기본 파일 그룹에 있는 시스템 테이블에 저장되고 카탈로그 보기를 통해 액세스할 수 있습니다.|  
|구조|행은 8K 페이지에 저장됩니다. 페이지는 같은 테이블의 행만 저장합니다.|행은 개별 행으로 저장됩니다. 페이지 구조는 없습니다. 데이터 파일에 있는 두 연속 행은 다른 메모리 액세스에 최적화된 테이블에 속할 수 있습니다.|  
|인덱스|인덱스는 데이터 행과 비슷한 페이지 구조로 저장됩니다.|인덱스 정의만 유지됩니다(인덱스 행은 유지되지 않음). 인덱스는 메모리 내에 유지되며 메모리 액세스에 최적화된 테이블이 데이터베이스를 다시 시작할 때 메모리로 로드되면 다시 생성됩니다. 인덱스 행은 유지되지 않으므로 인덱스 변경에 대한 로깅은 수행되지 않습니다.|  
|DML 작업|첫 번째 단계는 페이지를 찾은 다음 버퍼 풀로 로드하는 것입니다.<br /><br /> Insert<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 클러스터형 인덱스의 경우 행 순서에 대한 페이지 계정에 행을 삽입합니다.<br /><br /> Delete<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 페이지에서 삭제할 행을 찾아 삭제됨으로 표시합니다.<br /><br /> Update<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 페이지에서 행을 찾습니다. 업데이트는 키가 아닌 열에 대해 현재 위치에서 수행됩니다. 키 열 업데이트는 삭제 및 삽입 작업에 의해 수행됩니다.<br /><br /> DML 작업이 완료된 후 영향을 받는 페이지는 로깅 작업을 최소화하기 위해 버퍼 풀 정책, 검사점 또는 트랜잭션 커밋의 의 일부로 디스크에 플러시됩니다. 페이지에 읽고 쓰는 작업은 불필요한 I/O를 초래합니다.|메모리 액세스에 최적화된 테이블의 경우 데이터가 메모리에 있기 때문에 DML 작업은 직접 메모리에서 수행됩니다. 메모리 액세스에 최적화된 테이블에 대한 로그 레코드를 읽고 데이터 및 델타 파일에 유지시키는 백그라운드 스레드가 있습니다. 업데이트는 새로운 행 버전을 생성합니다. 하지만 업데이트는 삭제 후 삽입으로 기록됩니다.|  
|데이터 조각화|데이터 조작은 데이터를 조각화하여 부분적으로 채워진 페이지와 디스크에 연속되지 않고 논리적으로 연속된 페이지가 만들어집니다. 이로 인해 데이터 액세스 성능이 저하되고 데이터 조각 모음을 수행해야 합니다.|메모리 액세스에 최적화된 데이터는 페이지에 저장되지 않으므로 데이터 조각화가 없습니다. 그러나 행이 업데이트되고 삭제됨에 따라 데이터 및 델타 파일을 압축해야 합니다. 이런 작업은 병합 정책에 따라 백그라운드 MERGE 스레드에 의해 수행됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  

