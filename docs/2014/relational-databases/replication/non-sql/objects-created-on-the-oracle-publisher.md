---
title: Oracle 게시자에 생성되는 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], objects created
ms.assetid: c58a124b-4da7-46e2-9292-af8ce9e6664b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99e1d1f0692e5460e2c7003b0ab8dca860deca4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022141"
---
# <a name="objects-created-on-the-oracle-publisher"></a>Objects Created on the Oracle Publisher
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제는 변경 내용 추적 및 전달을 사용할 수 있도록 Oracle 게시자에 데이터베이스 개체를 설치합니다.[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 Oracle 게시자에 이진 파일을 설치하지 않습니다. 다음 표에서는 Oracle 게시자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 게시자로 식별될 때 Oracle 게시자에서 생성된 개체를 나열합니다. 개체 설명은 정보 제공의 목적으로만 제공됩니다. 이러한 개체는 수정하면 안 됩니다.  
  
|개체 이름|개체 유형|Description|  
|-----------------|-----------------|-----------------|  
|HREPL_ArticleNlog_V|Table|게시된 테이블에 변경 내용이 적용될 때 정보를 저장하는 데 사용되는 변경 내용 추적 테이블입니다. 변경 내용 추적 테이블은 게시된 각 테이블에 대해 생성됩니다.|  
|HREPL_Changes|Table|트랜잭션 집합에 할당되기 위해 대기 중인 변경 내용 수를 확인하기 위해 Xactset 작업에서 내부적으로 사용되는 테이블입니다. 이 작업에 대한 자세한 내용은 [Oracle 게시자를 위한 성능 튜닝](performance-tuning-for-oracle-publishers.md)을 참조하세요.|  
|HREPL_Distributor|Table|Oracle 게시자와 연결된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에 대한 정보를 유지 관리하는 데 사용되는 배포자 상태 테이블입니다.|  
|HREPL_Event|Table|스냅숏과 행 개수 요청을 동기화하는 데 사용되는 이벤트 테이블입니다.|  
|HREPL_Mutex|Table|Oracle 패키지 프로시저인 PopulatePollTable이 로그 판독기 에이전트와 데이터베이스 작업 모두에 의해 동시에 실행되지 않도록 하는 데 사용되는 테이블입니다.|  
|HREPL_Poll|Table|게시된 테이블에 대한 변경 내용 집합과 연결된 로그 테이블 항목을 식별하는 데 사용되는 테이블입니다.|  
|HREPL_PublishedTables|Table|트랜잭션 게시의 각 아티클에 대한 항목을 포함하는 테이블입니다.|  
|HREPL_Publisher|Table|게시자별 정보를 유지 관리하는 데 사용되는 게시자 상태 테이블입니다.|  
|HREPL_SchemaFilter|Table|새 게시 마법사를 통해 게시할 때 표시되지 않는 스키마를 포함하는 테이블입니다.|  
|HREPL_XactsetCreateTimes|Table|각 트랜잭션 집합과 연결된 작성 시간을 식별하는 테이블입니다.|  
|HREPL_XactsetJob|Table|Xactset 작업에 대한 현재 매개 변수 설정을 포함하는 테이블입니다.|  
|HREPL_Pollid|시퀀스|폴링 ID를 생성하는 데 사용되는 시퀀스입니다.|  
|HREPL_Seq|시퀀스|명령 변경의 순서를 지정하는 데 사용되는 시퀀스입니다.|  
|HREPL_Stmt|시퀀스|문 ID를 생성하는 데 사용되는 시퀀스입니다.|  
|HREPL|패키지 및 패키지 본문|게시자에서 생성된 게시자 지원 코드의 패키지입니다.|  
|MSSQLSERVERDISTRIBUTOR|공용 동의어|HREPL_Distributor 테이블에 대한 공용 동의어입니다. Oracle 게시자와 함께 사용하도록 배포자를 구성하면 이 동의어가 이미 데이터베이스에 있는 경우 동의어가 삭제되고 다시 생성됩니다.<br /><br /> CASCADE 옵션으로 공용 동의어와 구성된 Oracle 복제 사용자를 삭제하면 Oracle 게시자에서 모든 복제 개체가 제거됩니다.|  
|HREPL_Len_I_J_K|기능|Oracle 게시 패키지 코드 외부에 정의되어 LONG 열의 길이에 대한 쿼리에 사용되는 함수입니다. 게시된 LONG 열이 있는 테이블에 대한 매개 변수가 있는 명령을 생성할 때 사용됩니다. LONG 열이 있는 게시된 각 테이블에 대해 함수가 생성됩니다.|  
|HREPL_DropPublisher|절차|Oracle 게시 패키지 코드 외부에 정의되어 Oracle 게시자를 삭제하는 데 사용되는 프로시저입니다.|  
|HREPL_ExecuteCommand|절차|Oracle 게시 패키지 코드 외부에 정의되어 게시자에서 명령을 실행하는 데 사용되는 프로시저입니다.|  
|HREPL_ArticleN_Trigger_Row|트리거|게시된 각 테이블에 대해 생성되어 행 변경 내용을 추적하는 데 사용되는 트리거입니다.|  
|HREPL_ArticleN_Trigger_Stmt|트리거|게시된 각 테이블에 대해 생성되어 문 수준 변경 내용을 추적하는 데 사용되는 트리거입니다.|  
|HREPL_Article_I_J|보기|게시된 각 테이블에 대해 생성되어 게시된 테이블을 쿼리하는 데 사용되는 뷰입니다.|  
|HREPL_Log_I_J_K|보기|게시된 각 테이블에 대해 생성되어 변경 내용 추적 테이블을 쿼리하는 데 사용되는 뷰입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Oracle 게시자 구성](configure-an-oracle-publisher.md)   
 [Oracle 게시를 위한 용어 설명](glossary-of-terms-for-oracle-publishing.md)   
 [Oracle 게시 개요](oracle-publishing-overview.md)  
  
  
