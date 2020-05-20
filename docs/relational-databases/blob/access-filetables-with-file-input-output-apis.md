---
title: 파일 입/출력 API를 사용하여 FileTable 액세스 | Microsoft 문서
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with file APIs
ms.assetid: fa504c5a-f131-4781-9a90-46e6c2de27bb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d1cdc6947c97052660dea3be9d6013a8e61a090d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72908782"
---
# <a name="access-filetables-with-file-input-output-apis"></a>파일 입/출력 API를 사용하여 FileTable 액세스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable에서 파일 시스템 I/O가 작동하는 방식에 대해 설명합니다.  
  
##  <a name="get-started-using-file-io-apis-with-filetables"></a><a name="accessing"></a> FileTable에서 파일 I/O API 사용 시작  
 FileTable은 대개 Windows 파일 시스템 및 파일 I/O API를 통해 사용합니다. FileTable은 다양한 사용 가능한 파일 I/O API를 통한 비트랜잭션 액세스를 지원합니다.  
  
1.  파일 I/O API 액세스는 일반적으로 파일 또는 디렉터리에 대한 논리 UNC 경로를 가져오는 것으로 시작됩니다. 애플리케이션에서는 [GetFileNamespacePath&#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) 함수와 함께 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 디렉터리 또는 파일에 대한 논리 경로를 가져올 수 있습니다. 자세한 내용은 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)을 참조하세요.  
  
2.  그러면 애플리케이션에서는 이 논리 경로를 사용하여 파일 또는 디렉터리에 대한 핸들을 가져오고 개체에 대해 일부 작업을 수행합니다. 경로를 CreateFile() 또는 CreateDirectory()와 같은 지원되는 파일 시스템 API 함수에 전달하여 파일을 만들거나 열고 핸들을 가져올 수 있습니다. 그런 다음 핸들을 사용하여 데이터 스트리밍, 디렉터리 열거 또는 구성, 파일 특성 가져오기 또는 설정, 파일 또는 디렉터리 삭제 등과 같은 작업을 수행할 수 있습니다.  

##  <a name="creating-files-and-directories-in-a-filetable"></a><a name="create"></a> FileTable에 파일 및 디렉터리 만들기  
 CreateFile 또는 CreateDirectory 같은 파일 I/O API를 호출하여 FileTable에서 파일 또는 디렉터리를 만들 수 있습니다.  
  
-   모든 CREATION_DISPOSITION 플래그, 공유 모드 및 액세스 모드가 지원됩니다. 여기에는 파일 만들기, 삭제 및 현재 위치 수정이 포함됩니다. 또한 FileNamespace 업데이트, 즉 디렉터리 만들기/삭제, 이름 바꾸기 및 이동 작업도 지원됩니다.  
  
-   새 파일 또는 디렉터리를 만드는 것은 기본 FileTable에 새 행을 만드는 것에 해당합니다.  
  
-   파일의 경우 스트림 데이터는 **file_stream** 열에 저장되는 반면 디렉터리의 경우에는 이 열이 null입니다.  
  
-   파일의 경우 **is_directory** 열에 **false**가 포함되어 있고, 디렉터리의 경우 이 열에 **true**가 포함되어 있습니다.  
  
-   액세스 공유 및 동시성은 여러 동시 파일 I/O 작업 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업이 계층 구조 내의 동일한 파일 또는 디렉터리에 영향을 주는 경우에 적용됩니다.  
  
##  <a name="reading-files-and-directories-in-a-filetable"></a><a name="read"></a> FileTable의 파일 및 디렉터리 읽기  
 커밋된 읽기 격리 의미 체계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 스트림 및 특성 데이터에 대한 모든 파일 I/O 액세스 작업에 적용됩니다.  
  
##  <a name="writing-and-updating-files-and-directories-in-a-filetable"></a><a name="write"></a> FileTable의 파일 및 디렉터리 쓰기와 업데이트  
  
-   FileTable에 대한 모든 파일 I/O 쓰기 또는 업데이트 작업은 비트랜잭션 방식으로 수행됩니다. 즉, 이러한 작업에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션이 바인딩되지 않고, ACID가 보장되지 않습니다.  
  
-   FileTable에 대한 모든 파일 I/O 스트리밍/현재 위치 업데이트는 지원됩니다.  
  
-   파일 I/O API를 사용하는 모든 FILESTREAM 데이터 또는 특성에 대한 업데이트는 FileTable에서 해당 **file_stream** 및 파일 특성 열을 업데이트합니다.  
  
##  <a name="deleting-files-and-directories-in-a-filetable"></a><a name="delete"></a> FileTable의 파일 및 디렉터리 삭제  
 모든 Windows 파일 I/O API 의미 체계는 파일 또는 디렉터리를 삭제하면 적용됩니다.  
  
-   디렉터리에 파일 또는 하위 디렉터리가 있는 경우 디렉터리가 삭제되지 않습니다.  
  
-   파일 또는 디렉터리를 삭제하면 FileTable에서 해당 행이 제거됩니다. 이 작업은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업을 통해 해당 행을 삭제하는 것과 같습니다.  
  
##  <a name="supported-file-system-operations"></a><a name="supported"></a> 지원되는 파일 시스템 작업  
 FileTable은 다음 파일 시스템 작업과 관련된 파일 시스템 API를 지원합니다.  
  
-   디렉터리 관리  
  
-   파일 관리  
  
 FileTable은 다음 작업을 지원하지 않습니다.  
  
-   디스크 관리  
  
-   볼륨 관리  
  
-   트랜잭션 NTFS  
  
##  <a name="additional-considerations-for-file-io-access-to-filetables"></a><a name="considerations"></a> FileTable에 대한 파일 I/O 액세스 시 추가 고려 사항  
  
###  <a name="using-virtual-network-names-vnns-with-always-on-availability-groups"></a><a name="vnn"></a> Always On 가용성 그룹에 VNN(가상 네트워크 이름) 사용  
 FILESTREAM 또는 FileTable 데이터가 포함된 데이터베이스가 Always On 가용성 그룹에 속하는 경우 파일 시스템 API를 통한 FILESTREAM 또는 FileTable 데이터에 대한 모든 액세스에는 컴퓨터 이름 대신 VNN이 사용됩니다. 자세한 내용은 [Always On 가용성 그룹의 FILESTREAM 및 FileTable&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)을 참조하세요.  
  
###  <a name="partial-updates"></a><a name="partial"></a> 부분 업데이트  
 [GetFileNamespacePath&#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) 함수를 사용하여 FileTable에서 FILESTREAM용으로 가져온 쓰기 가능한 핸들은 FILESTREAM 내용을 현재 위치에서 부분적으로 업데이트하는 데 사용할 수 있습니다. 이와 달리 트랜잭션된 FILESTREAM 액세스에는 **OpenSQLFILESTREAM()** 을 호출하고 명시적 트랜잭션 컨텍스트를 전달하여 가져온 핸들이 사용됩니다.  
  
###  <a name="transactional-semantics"></a><a name="trans"></a> 트랜잭션 의미 체계  
 파일 I/O API를 사용하여 FileTable의 파일에 액세스할 경우 이러한 작업은 어떤 사용자 트랜잭션과도 연관되지 않으며 다음과 같은 특징도 있습니다.  
  
-   FileTable의 FILESTREAM 데이터에 대한 비트랜잭션 액세스는 어떤 트랜잭션과도 연관되지 않으므로 특정 격리 의미 체계가 없습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 내부 트랜잭션을 사용하여 FileTable 데이터에 대해 잠금/동시성 의미 체계를 적용할 수 있습니다. 이러한 유형의 내부 트랜잭션은 커밋된 읽기 격리 수준으로 수행됩니다.  
  
-   이와 같이 FILESTREAM 데이터에 대한 비트랜잭션 작업에는 ACID가 보장되지 않습니다. 일관성은 파일 시스템에서 파일이 자동으로 업데이트될 때와 유사하게 보장됩니다.  
  
-   이러한 변경은 롤백할 수 없습니다.  
  
 그러나 **OpenSqlFileStream()** 을 호출하여 트랜잭션 FILESTREAM 액세스를 통해 FileTable의 FILESTREAM 열에 액세스할 수도 있습니다. 이러한 종류의 액세스는 완전한 트랜잭션이 될 수 있으며 현재 지원되는 모든 트랜잭션 일관성 수준을 유지합니다.  
  
###  <a name="concurrency-control"></a><a name="concurrency"></a> 동시성 제어  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 파일 시스템 애플리케이션과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 애플리케이션 간에는 물론 파일 시스템 애플리케이션 간에도 FileTable 액세스에 동시성 제어를 적용합니다. 이 동시성 제어는 FileTable 행에 대해 적절한 잠금을 얻음으로써 수행됩니다.  
  
###  <a name="triggers"></a><a name="triggers"></a> 트리거  
 파일 시스템을 통해 파일, 디렉터리 또는 해당 특성 만들기, 수정, 삭제 작업을 수행하면 FileTable에서는 해당되는 삽입, 업데이트 또는 삭제 작업이 수행됩니다. 또한 연결된 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] DML 트리거가 이러한 작업의 일부로 실행됩니다.  
  
##  <a name="file-system-functionality-supported-in-filetables"></a><a name="funclist"></a> FileTable에서 지원되는 파일 시스템 기능  
  
|기능|지원됨|주석|  
|----------------|---------------|--------------|  
|**Oplock**|yes|수준 2, 수준 1, 일괄 처리 및 필터 oplock을 지원합니다.|  
|**확장 특성**|예||  
|**구문 재분석 지점**|예||  
|**영구 ACL**|예||  
|**명명된 스트림**|예||  
|**스파스 파일**|yes|스파스는 파일에 대해서만 설정할 수 있으며 데이터 스트림 스토리지에는 영향을 줍니다. FILESTREAM 데이터는 NTFS 볼륨에 저장되므로 FileTable 기능은 NTFS 파일 시스템에 대한 요청을 전달하여 스파스 파일을 지원합니다.|  
|**압축**|yes||  
|**암호화**|yes||  
|**TxF**|예||  
|**파일 ID**|예||  
|**개체 ID**|예||  
|**심볼 링크**|예||  
|**하드 링크**|예||  
|**짧은 이름**|예||  
|**디렉터리 변경 알림**|예||  
|**바이트 범위 잠금**|yes|바이트 범위 잠금에 대한 요청은 NTFS 파일 시스템에 전달됩니다.|  
|**메모리 매핑된 파일**|예||  
|**취소 I/O**|yes||  
|**보안**|예|Windows 공유 수준 보안과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 테이블 및 열 수준 보안이 적용됩니다.|  
|**USN 저널**|예|FileTable의 파일 및 디렉터리에 대한 메타데이터 변경은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 DML 작업입니다. 따라서 변경 내용이 해당 데이터베이스 로그 파일에 기록됩니다. 그러나 크기를 변경한 경우를 제외하고 NTFS USN 저널에는 변경 내용이 기록되지 않습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 변경 내용 추적 기능을 사용할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [FileTable로 파일 로드](../../relational-databases/blob/load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [Transact-SQL을 사용하여 FileTable에 액세스](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [FileTable DDL, 함수, 저장 프로시저 및 뷰](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
