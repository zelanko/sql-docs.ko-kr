---
title: FileTable과 기타 SQL Server 기능 간 호환성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], using with other features
ms.assetid: f12a17e4-bd3d-42b0-b253-efc36876db37
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8a6ac6668ff362a986646c4e01b1f0e5e722611c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955363"
---
# <a name="filetable-compatibility-with-other-sql-server-features"></a>FileTable과 기타 SQL Server 기능 간 호환성
  FileTable이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 기능과 함께 작동하는 방식에 대해 설명합니다.  
  
##  <a name="alwayson-availability-groups-and-filetables"></a><a name="alwayson"></a>AlwaysOn 가용성 그룹 및 Filetable  
 FILESTREAM 또는 FileTable 데이터가 포함된 데이터베이스가 AlwaysOn 가용성 그룹에 속하는 경우  
  
-   FileTable 기능은 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]에서 부분적으로 지원됩니다. 장애 조치(Failover) 이후 FileTable 데이터는 주 복제본에서 액세스할 수 있지만 FileTable 데이터를 읽기 가능한 보조 복제본에서는 액세스할 수 없습니다.  
  
    > [!NOTE]  
    >  장애 조치(Failover) 이후 모든 FILESTREAM 기능이 지원됩니다. FILESTREAM 데이터는 읽기 가능한 두 보조 복제본 및 새로운 주 복제본에서 액세스할 수 있습니다.  
  
-   FILESTREAM 및 FileTable 함수가 컴퓨터 이름 대신 VNN(가상 네트워크 이름)을 사용하거나 반환합니다. 이러한 함수에 대한 자세한 내용은 [Filestream 및 FileTable 함수&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql)를 참조하세요.  
  
-   파일 시스템 API를 통한 FILESTREAM 또는 FileTable 데이터에 대한 모든 액세스에는 컴퓨터 이름 대신 VNN이 사용되어야 합니다. 자세한 내용은 [AlwaysOn 가용성 그룹의 FILESTREAM 및 FileTable&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)을 참조하세요.  
  
##  <a name="partitioning-and-filetables"></a><a name="OtherPartitioning"></a> 분할과 FileTable  
 분할은 FileTable에서 지원되지 않습니다. 여러 FILESTREAM 파일 그룹에 대한 지원을 사용하면 SQL 2008 FILESTREAM과 달리 대부분의 시나리오에서 분할에 의존하지 않고도 순수한 확장 문제를 처리할 수 있습니다.  
  
##  <a name="replication-and-filetables"></a><a name="OtherRepl"></a>복제 및 Filetable  
 복제 및 관련 기능(트랜잭션 복제, 병합 복제, 변경 데이터 캡처 및 변경 내용 추적 포함)은 FileTable에서 지원되지 않습니다.  
  
##  <a name="transaction-semantics-and-filetables"></a><a name="OtherIsolation"></a>트랜잭션 의미 체계 및 Filetable  
 **Windows 애플리케이션**  
 Windows 애플리케이션은 데이터베이스 트랜잭션을 인식하지 못하므로 Windows 쓰기 작업에서는 데이터베이스 트랜잭션의 ACID 속성을 제공하지 않습니다. 따라서 Windows 업데이트 작업에는 트랜잭션 롤백 및 복구를 수행할 수 없습니다.  
  
 **Transact-SQL 애플리케이션**  
 FileTable의 FILESTREAM(file_stream) 열에서 작동하는 TSQL 애플리케이션의 경우 격리 의미 체계는 일반적인 사용자 테이블의 FILESTREAM 데이터 형식을 사용할 때와 동일합니다.  
  
##  <a name="query-notifications-and-filetables"></a><a name="OtherQueryNot"></a>쿼리 알림 및 Filetable  
 쿼리의 WHERE 절이나 다른 부분에 FileTable의 FILESTREAM 열에 대한 참조를 포함할 수 없습니다.  
  
##  <a name="select-into-and-filetables"></a><a name="OtherSelectInto"></a>SELECT INTO 및 Filetable  
 FileTable에서 실행된 SELECT INTO 문은 일반적인 테이블의 FILESTREAM 열과 마찬가지로 만들어진 대상 테이블의 FileTable 의미 체계를 전파하지 않습니다. 모든 대상 테이블 열은 일반적인 열과 같이 동작하며 FileTable 의미 체계가 연결되지 않습니다.  
  
##  <a name="triggers-and-filetables"></a><a name="OtherTriggers"></a>Triggers 및 Filetable  
 **DDL(데이터 정의 언어) 트리거**  
 DDL 트리거의 경우 FileTable과 관련하여 특별히 고려해야 할 사항이 없습니다. 일반적인 DDL 트리거는 CREATE/ALTER DATABASE 작업과 FileTable에 대한 CREATE/ALTER TABLE 작업이 수행될 때 실행됩니다. 트리거는 EVENTDATA() 함수를 호출하여 DDL 명령 텍스트 및 기타 정보를 비롯한 실제 이벤트 데이터를 검색할 수 있습니다. 기존 Eventdata 스키마에 대한 새 이벤트나 변경 내용은 없습니다.  
  
 **DML(데이터 조작 언어) 트리거**  
 트리거를 만드는 DDL 작업 중에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   FileTable은 DML 작업에 대한 INSTEAD OF 트리거를 지원하지 않습니다. 이는 FILESTREAM 열이 포함된 모든 테이블에 적용되던 기존 제한 사항입니다.  
  
-   FileTable은 DML 작업에 대한 AFTER 트리거를 지원하지 않습니다.  
  
-   FileTable에 정의된 트리거는 부모 FileTable을 포함하여 모든 FileTable을 업데이트할 수 없습니다. 이 제한 사항은 주로 동일한 트랜잭션의 파일 시스템 액세스가 보유하는 잠금으로 인해 트리거와의 잠금 충돌이 발생하지 않도록 하기 위한 것입니다.  
  
 **비트랜잭션 액세스 및 이러한 액세스가 트리거에 미치는 영향**  
 -   데이터베이스에서 비트랜잭션 업데이트 액세스가 허용되는 경우 해당 데이터베이스의 FileTable을 비롯하여 모든 테이블에 있는 FILESTREAM 데이터를 현재 위치에서 업데이트할 수 있습니다. 이러한 가능성 때문에 FILESTREAM 내용의 이전 이미지를 트리거에서 사용하지 못할 수 있습니다.  
  
-   파일 시스템을 통한 비트랜잭션 업데이트 작업의 경우 SQL Server에서는 내부 트랜잭션을 만들어 CloseHandle 작업을 캡처하며, 이 트랜잭션의 일부로 정의된 DML 트리거가 실행될 수 있습니다. 트리거 본문 내부의 트랜잭션에 대한 롤백은 금지되지는 않지만 FILESTREAM의 변경 내용은 롤백되지 않습니다.  이러한 롤백은 FILESTREAM 내용이 변경된 경우에도 Update 트리거가 실행되지 않도록 할 수도 있습니다.  
  
-   이러한 영향 이외에도 FileTable의 트리거는 두 가지 동작을 더 처리해야 합니다.  
  
    -   파일 시스템을 통해 FileTable에 대한 비트랜잭션 업데이트 작업을 수행하는 경우 FILESTREAM 내용이 다른 Win32 작업에 의해 배타적으로 잠겨 트리거 본문을 통한 읽기/쓰기 액세스가 허용되지 않을 수 있습니다. 이 경우 트리거 본문 내의 FILESTREAM 내용에 액세스하려고 하면 "공유 위반 오류"가 발생할 수 있습니다. 이러한 오류를 적절히 처리하도록 트리거를 디자인해야 합니다.  
  
    -   일부 경우에는 파일 시스템 액세스에 공유 모드가 허용되어 있어서 다른 비트랜잭션 업데이트 작업에서 동시에 쓰기 작업을 수행할 수 있으므로 FILESTREAM의 AFTER 이미지는 안정적이지 않을 수 있습니다.  
  
-   관리 작업이나 데이터베이스 충돌로 인해 Win32 핸들이 명시적으로 중지된 경우와 같이 Win32 핸들이 비정상적으로 종료된 경우에는 이 비정상적으로 종료된 Win32 애플리케이션에서 FILESTREAM 내용을 변경했더라도 복구 작업 중 사용자 트리거가 실행되지 않습니다.  
  
##  <a name="views-and-filetables"></a><a name="OtherViews"></a>뷰 및 Filetable  
 **뷰**  
 다른 테이블과 마찬가지로 FileTable에서도 뷰를 만들 수 있습니다. 그러나 FileTable에서 만든 뷰에는 다음 고려 사항이 적용됩니다.  
  
-   뷰에는 FileTable 의미 체계가 없습니다. 즉, 파일 특성 열을 비롯한 뷰의 열은 특별한 의미 체계가 없는 일반적인 뷰 열처럼 동작하며, 이는 파일/디렉터리를 나타내는 행에도 동일하게 적용됩니다.  
  
-   "업데이트 가능한 뷰" 의미 체계에 따라 뷰를 업데이트할 수 있지만 테이블에서와 마찬가지로 기본 테이블 제약 조건에 따라 업데이트가 거부될 수 있습니다.  
  
-   파일의 경로를 뷰의 명시적 열로 추가하여 뷰에 시각화할 수 있습니다. 다음은 그 예입니다.  
  
     `CREATE VIEW MP3FILES AS SELECT column1, column2, ..., GetFileNamespacePath() AS PATH, column3,...  FROM Documents`  
  
 **인덱싱된 뷰**  
 현재 인덱싱된 뷰에는 FILESTREAM 열이나 FILESTREAM 열에 종속된 계산/지속형 계산 열이 포함될 수 없습니다. 이 동작은 FileTable에 정의된 뷰에도 그대로 적용됩니다.  
  
##  <a name="snapshot-isolation-and-filetables"></a><a name="OtherSnapshots"></a> 스냅샷 격리와 FileTable  
 RCSI(커밋된 읽기 스냅샷 격리)와 SI(스냅샷 격리)는 데이터에 대한 업데이트 작업이 수행 중인 경우에도 판독기에서 데이터의 스냅샷을 사용할 수 있도록 하는 기능에 의존합니다. 그러나 FileTable을 사용하면 Filestream 데이터에 대한 비트랜잭션 쓰기 액세스가 허용됩니다. 따라서 FileTable이 포함된 데이터베이스에서 이러한 기능을 사용하는 경우에는 다음 제한 사항이 적용됩니다.  
  
-   FileTable이 포함된 데이터베이스를 변경하여 RCSI/SI를 사용하도록 설정할 수 있습니다.  
  
-   데이터베이스에 대해 비트랜잭션 액세스가 FULL로 설정된 경우 트랜잭션이 RCSI에서 실행되거나 SI가 다음과 같이 동작합니다.  
  
    -   FileTable의 file_stream 열에 대한 모든 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 읽기가 실패합니다. file_stream 열에 대한 INSERT 및 UPDATE는 해당 열에서 읽는 경우만 아니면 성공합니다.  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문에서 READCOMMITTEDLOCK 테이블 힌트를 지정한 경우 읽기가 성공하며, 행 버전 관리를 사용하는 대신 행에 대한 잠금이 사용됩니다.  
  
    -   트랜잭션된 Win32 FileStream 열기 요청도 실패합니다.  
  
    -   트랜잭션되지 않은 FileTable Win32 액세스는 성공합니다. FileTable이 수행한 모든 내부 쿼리는 영향을 받지 않습니다.  
  
    -   전체 텍스트 인덱싱은 데이터베이스 옵션이 READ_COMMITTED_SNAPSHOT이든 ALLOW_SNAPSHOT_ISOLATION이든 관계없이 항상 성공합니다.  
  
##  <a name="readable-secondary-databases"></a><a name="readsec"></a>읽을 수 있는 보조 데이터베이스  
 읽기 가능한 보조 데이터베이스에는 이전 섹션인 [스냅샷 격리와 FileTable](#OtherSnapshots)에 설명된 것처럼 스냅샷과 동일한 고려 사항이 적용됩니다.  
  
##  <a name="contained-databases-and-filetables"></a><a name="CDB"></a> 포함된 데이터베이스와 FileTable  
 FileTable 기능이 종속되는 FILESTREAM 기능을 사용하려면 데이터베이스 외부에서의 몇 가지 구성이 필요합니다. 따라서 FILESTREAM 또는 FileTable을 사용하는 데이터베이스는 완전히 포함되지 않습니다.  
  
 포함된 사용자와 같은 포함된 데이터베이스의 특정 기능을 사용하려면 데이터베이스 포함 옵션을 PARTIAL로 설정하면 됩니다. 그러나 이 경우 일부 데이터베이스 설정은 데이터베이스에 포함되지 않으며 데이터베이스를 이동할 때 자동으로 이동되지 않는다는 것을 알고 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [FileTable 관리](manage-filetables.md)  
  
  
