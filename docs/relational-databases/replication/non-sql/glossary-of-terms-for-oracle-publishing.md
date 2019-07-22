---
title: Oracle 게시를 위한 용어 설명 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], glossary
ms.assetid: e21dfa4b-6144-4be7-9cbf-ca2709b2bd9f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ac643b3c0c095dee143c3feca878bd4072273bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901106"
---
# <a name="glossary-of-terms-for-oracle-publishing"></a>Oracle 게시를 위한 용어 설명
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle 게시를 구성 및 관리할 때 다음 Oracle 용어에 익숙해야 합니다. 전체 Oracle 용어 목록은 Oracle 온라인 설명서를 참조하십시오.  
  
#### <a name="index-organized-tables-iot"></a>IOT(인덱스 구성 테이블)  
 인덱스 순서대로 데이터가 물리적으로 디스크에 저장되는 테이블로, 클러스터형 인덱스가 있는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블과 유사합니다. IOT는 클러스터형 인덱스가 있는 테이블로 구독자에 복제됩니다.  
  
#### <a name="instance"></a>인스턴스  
 Oracle 데이터베이스는 인스턴스와 연결됩니다. 인스턴스는 데이터베이스를 지원하는 메모리 및 백그라운드 프로세스로 구성됩니다. Oracle 인스턴스는 항상 단일 데이터베이스에 매핑되지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스는 여러 데이터베이스를 포함할 수 있습니다. Oracle 데이터베이스가 다중 인스턴스를 포함할 수 있는 경우도 있습니다.  
  
#### <a name="oracle-listener"></a>Oracle 수신기  
 Oracle 데이터베이스 인스턴스에 대한 들어오는 네트워크 트래픽을 처리합니다. Oracle 데이터베이스에 대한 네트워크 연결을 구성할 때 트래픽이 전송되는 프로토콜과 수신기가 트래픽을 수신하는 포트를 지정합니다. 일반적으로 수신기는 Oracle 데이터베이스 인스턴스와 동일한 컴퓨터에서 실행하도록 구성되며 하나 이상의 인스턴스를 제공하도록 구성될 수 있습니다.  
  
#### <a name="rowid"></a>ROWID  
 데이터베이스의 특정 행 위치를 가리키는 포인터입니다. ROWID를 사용하여 행을 검색하는 것이 테이블 검색 또는 인덱스를 사용하는 것보다 빠르므로 복제는 게시된 테이블의 변경 내용을 처리하는 중 일시적으로 ROWID를 사용합니다.  
  
#### <a name="sequence"></a>시퀀스  
 고유 번호를 생성하는 데 사용되는 데이터베이스 개체입니다. 복제는 시퀀스를 사용하여 게시된 테이블에 대한 변경 내용의 적용 순서를 지정합니다.  
  
#### <a name="sqlplus"></a>SQL\*Plus  
 Oracle 데이터베이스에 액세스하고 쿼리하는 데 사용되는 애플리케이션으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sqlcmd**와 유사합니다.  
  
#### <a name="synonym"></a>동의어  
 개체에 대한 별칭입니다. **MSSQLSERVERDISTRIBUTOR** 특수 공용 동의어는 Oracle 게시자를 구성할 때 자동으로 생성됩니다. 동의어는 **HREPL_Distributor** 테이블을 참조하고 게시자에 서비스를 제공하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에게 논리 포인터를 제공합니다.  
  
 Oracle 데이터베이스가 게시된 경우 이 공용 동의어는 게시자에 서비스를 제공하도록 이미 구성된 특정 배포자를 식별하므로 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자를 사용하도록 이 게시자를 구성하는 후속 시도가 실패합니다.  
  
#### <a name="tablespace"></a>테이블스페이스  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 파일 그룹과 거의 동일한 데이터베이스 스토리지 단위입니다.  
  
#### <a name="tns-service-name"></a>TNS 서비스 이름  
 TNS(Transparent Network Substrate)는 Oracle 데이터베이스에서 사용되는 통신 계층입니다. TNS 서비스 이름은 네트워크상에서 Oracle 데이터베이스 인스턴스를 식별하는 이름입니다. Oracle 데이터베이스에 대한 연결을 구성할 때 TNS 서비스 이름을 지정합니다. 복제는 TNS 서비스 이름을 사용하여 게시자를 식별하고 연결을 설정합니다.  
  
#### <a name="user-schema"></a>사용자 스키마  
 사용자 스키마는 특정 데이터베이스 개체 집합을 소유하는 데이터베이스 사용자로 생각할 수 있습니다. 복제 관리 사용자 스키마는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] MSSQLSERVERDISTRIBUTOR **공용 동의어를 제외하고 Oracle 데이터베이스에서** 복제 프로세스로 생성된 모든 개체를 소유합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 게시자에 생성되는 개체](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)   
 [SQL Server 이외 게시자](../../../relational-databases/replication/non-sql/non-sql-server-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
