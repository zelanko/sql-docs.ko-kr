---
title: 테이블 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.tableproperties.storage.f1
- sql12.SWB.SELECTCOLUMNS.F1
- sql12.swb.tableproperties.filetable.f1
- sql12.swb.tableproperties.general.f1
- sql12.swb.tableproperties.changetracking.f1
ms.assetid: ad8a2fd4-f092-4c0f-be85-54ce8b9d725a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b07f157294700b3b3b7958ce4cdc6f1589bff864
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196715"
---
# <a name="table-properties"></a>테이블 속성
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 테이블 속성 편집 대화 상자에 표시된 테이블 속성에 대해 설명합니다. 이러한 속성을 표시하는 방법은 [테이블 정의 보기](view-the-table-definition.md)를 참조하세요.  
  
 **항목 내용**  
  
1.  [일반 페이지](#GeneralPage)  
  
2.  [변경 내용 추적 페이지](#ChangeTracking)  
  
3.  [파일 테이블 페이지](#FileTable)  
  
4.  [ 페이지](#Storage)  
  
##  <a name="GeneralPage"></a> 일반 페이지  
 **Database**  
 이 테이블이 포함된 데이터베이스의 이름입니다.  
  
 **Server**  
 현재 서버 인스턴스의 이름입니다.  
  
 **사용자**  
 이 연결을 사용하는 사용자의 이름입니다.  
  
 **만든 날짜**  
 테이블을 만든 날짜와 시간입니다.  
  
 **이름**  
 테이블의 이름입니다.  
  
 **스키마**  
 테이블을 소유하고 있는 스키마입니다.  
  
 **시스템 개체**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 내부 정보를 보관하는 데 사용하는 시스템 테이블을 나타냅니다. 시스템 테이블은 사용자가 직접 변경하거나 참조해서는 안 됩니다.  
  
 **ANSI NULL**  
 ANSI NULL 옵션이 ON으로 설정된 상태에서 개체가 만들어졌는지 여부를 나타냅니다. 자세한 내용은 [SET ANSI_NULLS&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)를 참조하세요.  
  
 **따옴표 붙은 식별자**  
 따옴표 붙은 식별자 옵션이 ON으로 설정된 상태에서 개체가 만들어졌는지 여부를 나타냅니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)를 참조하세요.  
  
 **잠금 에스컬레이션**  
 테이블의 잠금 에스컬레이션 세분성을 나타냅니다. 데이터베이스 엔진에서의 잠금에 대한 자세한 내용은 [SQL Server 트랜잭션 잠금 및 행 버전 관리 지침](https://msdn.microsoft.com/library/jj856598.aspx)을 참조하세요. 가능한 값은 다음과 같습니다.  
  
 AUTO  
 이 옵션을 선택하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 테이블 스키마에 적절한 잠금 에스컬레이션 세분성을 선택할 수 있습니다.  
  
-   테이블이 분할된 경우에는 잠금이 HOBT(힙 또는 B-트리) 세분성으로 에스컬레이션됩니다. 잠금이 HoBT 수준으로 에스컬레이션된 후에는 나중에 잠금이 TABLE 세분성으로 에스컬레이션되지 않습니다.  
  
-   테이블이 분할되지 않은 경우에는 잠금이 TABLE 세분성으로 에스컬레이션됩니다.  
  
 TABLE  
 테이블이 분할되었는지 여부에 관계없이 잠금 에스컬레이션이 테이블 수준 세분성에서 수행됩니다. 기본값은 TABLE입니다.  
  
 DISABLE  
 대부분의 경우 잠금 에스컬레이션이 허용되지 않습니다. 테이블 수준 잠금은 부분적으로 허용됩니다. 예를 들어 직렬화 가능 격리 수준에서 클러스터형 인덱스가 없는 테이블을 검색하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 테이블 잠금을 사용하여 데이터 무결성을 보호해야 합니다.  
  
 **테이블이 복제 되었습니다.**  
 테이블이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제를 사용하여 다른 데이터베이스에 복제된 경우를 나타냅니다. 가능한 값은 `True` 또는 `False`입니다.  
  
##  <a name="ChangeTracking"></a>변경 내용 추적 페이지  
 **변경 내용 추적**  
 테이블에 대해 변경 내용 추적이 설정되었는지 여부를 나타냅니다. 기본값은 `False`입니다.  
  
 이 옵션은 데이터베이스에 대해 변경 내용 추적이 설정된 경우에만 사용할 수 있습니다.  
  
 변경 내용 추적을 설정하려면 테이블에 기본 키가 있어야 하고, 해당 테이블을 수정할 수 있는 권한이 있어야 합니다. 
  [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)을 사용하여 변경 내용 추적을 구성할 수 있습니다.  
  
 **업데이트 된 열 추적**  
 
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 업데이트된 열을 추적하는지 여부를 나타냅니다.  
  
 변경 내용 추적에 대한 자세한 내용은 [변경 내용 추적 정보&#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md)를 참조하세요.  
  
##  <a name="FileTable"></a>FileTable 페이지  
 FileTable과 관련된 테이블의 속성을 표시합니다. 자세한 내용은 [FileTables&#40;SQL Server&#41;](../blob/filetables-sql-server.md)를 참조하세요.  
  
 **FileTable 이름 열 데이터 정렬**  
 FileTable의 **Name** 열에 적용되는 데이터 정렬입니다. 
  **Name** 열에는 파일 및 디렉터리 이름이 포함됩니다.  
  
 **FileTable 디렉터리 이름**  
 FileTable의 루트 폴더입니다.  
  
 **FileTable 네임 스페이스 사용**  
 
  `True` 값은 해당 테이블이 FileTable임을 나타냅니다. 이 값을 `False`로 변경하면 FileTable이 일반적인 사용자 테이블로 변경됩니다. 나중에 테이블을 다시 FileTable로 변경할 경우 테이블이 FileTable 일관성 검사를 통과해야 변환이 성공합니다.  
  
##  <a name="Storage"></a>저장소 페이지  
 선택한 테이블의 스토리지 관련 속성을 표시합니다.  
  
### <a name="compression"></a>압축  
 **압축 유형**  
 테이블의 압축 유형입니다. 이 속성은 분할되지 않은 테이블에만 사용할 수 있습니다. 자세한 내용은 [Data Compression](../data-compression/data-compression.md)을 참조하세요.  
  
 **페이지 압축을 사용 하는 파티션**  
 페이지 압축을 사용하는 파티션 번호입니다. 이 속성은 분할된 테이블에만 사용할 수 있습니다.  
  
 **압축 되지 않은 파티션**  
 압축되지 않은 파티션 번호입니다. 이 속성은 분할된 테이블에만 사용할 수 있습니다.  
  
 **행 압축을 사용 하는 파티션**  
 행 압축을 사용하는 파티션 번호입니다. 이 속성은 분할된 테이블에만 사용할 수 있습니다.  
  
### <a name="filegroup"></a>파일 그룹  
 **텍스트 파일 그룹**  
 테이블의 텍스트 데이터가 들어 있는 파일 그룹의 이름입니다.  
  
 **그룹별로**  
 테이블이 있는 파일 그룹의 이름입니다.  
  
 **테이블이 분할 되었습니다.**  
 가능한 값은 `True` 및 `False`입니다.  
  
 **Filestream 파일 그룹**  
 테이블에 FILESTREAM 특성이 있는 `varbinary(max)` 열이 있을 경우 FILESTREAM 데이터 파일 그룹의 이름을 지정합니다. 기본값은 기본 FILESTREAM 데이터 파일 그룹입니다.  
  
 테이블에 FILESTREAM 데이터가 없는 경우 이 필드가 비어 있습니다.  
  
### <a name="general"></a>일반  
 **Vardecimal 저장소 형식을 사용할 수 있습니다.**  
 인 `True`경우이 읽기 전용 값은 `decimal` 및 `numeric` 데이터 형식이 vardecimal 저장소 형식을 사용 하 여 저장 됨을 나타냅니다. 이 옵션을 변경 하려면 [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)의 `vardecimal storage format` 옵션을 사용 합니다. VarDecimal 스토리지 형식은 더 이상 사용되지 않습니다. 대신 ROW 압축을 사용하세요.  
  
 **인덱스 공간**  
 테이블의 인덱스가 차지하는 공간의 크기(MB)입니다. 이 값에 테이블에 대한 XML 인덱스 공간 사용량은 포함되지 않습니다. XML 인덱스가 해당 테이블에 속할 경우 [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) 를 대신 사용하세요.  
  
 **행 개수**  
 테이블의 행 수입니다.  
  
 **데이터 공간**  
 테이블의 데이터가 차지하는 공간의 크기(MB)입니다.  
  
### <a name="partitioning"></a>분할  
 이 섹션은 테이블이 분할된 경우에만 사용할 수 있습니다. 자세한 내용은 [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)을 참조하세요.  
  
 **파티션 열**  
 테이블이 분할된 열의 이름입니다.  
  
 **파티션 구성표**  
 테이블이 분할된 경우에 표시되는 파티션 구성표의 이름입니다. 테이블이 분할되지 않은 경우 이 필드가 비어 있습니다.  
  
 **파티션 수**  
 테이블에 있는 파티션의 수입니다.  
  
 **FILESTREAM 파티션 구성표**  
 테이블이 분할된 경우에 표시되는 FILESTREAM 파티션 구성표의 이름입니다. 테이블이 분할되지 않은 경우 이 필드가 비어 있습니다.  
  
 FILESTREAM 파티션 구성표는 **파티션 구성표** 옵션에서 지정한 구성표와 대칭이어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 정의 보기](view-the-table-definition.md)   
 [열 &#40;데이터베이스 엔진&#41;수정](../tables/modify-columns-database-engine.md)  
  
  
