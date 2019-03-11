---
title: Filetable(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], overview
- FileTables [SQL Server]
- FileTable [SQL Server], see FileTables [SQL Server]
- FileTable [SQL Server]
ms.assetid: a57b629c-e9ed-48fd-9a48-ed3787d80c8f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 178d926dbcbfc6e599a57207369bf61e603468a9
ms.sourcegitcommit: 8664c2452a650e1ce572651afeece2a4ab7ca4ca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56828453"
---
# <a name="filetables-sql-server"></a>FileTable(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 파일 데이터에 대해 Windows 파일 네임스페이스 및 Windows 애플리케이션과의 호환성을 지원합니다. FileTable을 통해 애플리케이션이 해당 스토리지 및 데이터 관리 구성 요소를 통합할 수 있으며, 구조화되지 않은 데이터 및 메타데이터에 대한 통합 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스(전체 텍스트 검색 및 의미 체계 검색 포함)가 제공됩니다.  
  
 즉, 파일 및 문서를 FileTable이라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 특수 테이블에 저장할 수 있지만, Windows 애플리케이션에서 해당 파일 및 문서에 액세스할 때는 파일 시스템에 저장된 파일 및 문서에 액세스할 때와 같은 방식으로 처리됩니다. 클라이언트 애플리케이션을 변경할 필요는 없습니다.  
  
 FileTable은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FILESTREAM 기술을 기반으로 구축된 기능입니다. FILESTREAM에 대한 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
##  <a name="Goals"></a> FileTable 기능의 이점  
 FileTable 기능의 목적은 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 내에 저장된 파일 데이터에 대한 Windows API 호환성을 제공합니다. Windows API 호환성은 다음과 같습니다.  
  
    -   FILESTREAM 데이터에 비트랜잭션 스트리밍 방식으로 액세스하여 해당 데이터를 현재 위치에서 업데이트할 수 있습니다.  
  
    -   디렉터리 및 파일의 계층 네임스페이스가 제공됩니다.  
  
    -   파일을 만든 날짜와 수정한 날짜 같은 파일 특성의 스토리지가 제공됩니다.  
  
    -   Windows 파일 및 디렉터리 관리 API가 지원됩니다.  
  
-   FILESTREAM 및 파일 특성 데이터를 통해 관리 도구, 서비스 및 관계형 쿼리 기능을 비롯한 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능과의 호환성이 제공됩니다.  
  
 파일 서버에 현재 파일로 존재하는 구조화되지 않은 데이터를 스토리지하고 관리하는 데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하려면 여러 가지 문제를 해결해야 했지만 FileTable을 사용하면 이러한 문제가 상당히 해결됩니다. 기업에서는 파일 서버의 데이터를 FileTable로 이동하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제공하는 통합된 관리 기능 및 서비스를 이용할 수 있습니다. 동시에 해당 데이터를 파일 시스템의 파일로 표시하는 기존의 Windows 애플리케이션을 위해 Windows 애플리케이션 호환성을 유지할 수 있습니다.  
 
  
##  <a name="Description"></a> FileTable 정의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 파일 및 디렉터리를 스토리지해야 하며 Windows API 호환성과 비트랜잭션 액세스가 필요한 애플리케이션을 위해 **FileTable**이라는 특수한 **파일 테이블**을 제공합니다. FileTable은 미리 정의된 스키마를 사용하여 파일 및 디렉터리 계층 구조 정보와 파일 특성은 물론 FILESTREAM 데이터도 저장하는 특수한 사용자 테이블입니다.  
  
 FileTable에서는 다음과 같은 기능을 제공합니다.  
  
-   FileTable은 디렉터리 및 파일의 계층 구조를 나타냅니다. FileTable은 이 계층 구조의 모든 노드(계층 구조에 포함된 디렉터리와 파일의 노드)와 관련된 데이터를 저장합니다. 이 계층 구조는 FileTable을 만들 때 지정하는 루트 디렉터리에서 시작됩니다.  
  
-   FileTable의 각 행은 파일 또는 디렉터리 하나를 나타냅니다.  
  
-   각 행에는 다음 항목이 포함됩니다. FileTable의 스키마에 대한 자세한 내용은 [FileTable Schema](../../relational-databases/blob/filetable-schema.md)를 참조하십시오.  
  
    -   스트림 데이터의 **file_stream** 열 및 **stream_id**(GUID) 식별자 (디렉터리의 경우 **file_stream** 열은 NULL입니다.)  
  
    -   현재 항목(파일 또는 디렉터리) 및 디렉터리 계층 구조를 나타내고 유지 관리하기 위한 **path_locator** 및 **parent_path_locator** 열  
  
    -   파일 I/O API에 유용한 파일 작성 날짜 및 수정 날짜 같은 10개의 파일 특성  
  
    -   파일 및 문서에 대한 전체 텍스트 검색과 의미 체계 검색을 지원하는 Type 열  
  
-   FileTable은 특정 시스템 정의 제약 조건 및 트리거를 적용하여 파일 네임스페이스의 의미 체계를 유지 관리합니다.  
  
-   데이터베이스가 비트랜잭션 액세스용으로 구성된 경우 FileTable에 표시되는 파일 및 디렉터리 계층 구조는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스용으로 구성된 FILESTREAM 공유를 통해 노출됩니다. Windows 애플리케이션에서는 이를 통해 파일 시스템에 액세스할 수 있습니다.  
  
 FileTable에는 다음과 같은 특징도 있습니다.  
  
-   FileTable에 저장된 파일 및 디렉터리 데이터는 Windows API 기반 애플리케이션의 비트랜잭션 파일 액세스를 위한 Windows 공유를 통해 노출됩니다. Windows 애플리케이션에서는 이러한 공유를 해당 애플리케이션의 파일 및 디렉터리를 포함하는 일반적인 공유와 동일하게 인식합니다. 애플리케이션에서는 풍부한 Windows API를 사용하여 이 공유에 있는 파일 및 디렉터리를 관리할 수 있습니다.  
  
-   공유를 통해 표시되는 디렉터리 계층 구조는 FileTable 내에서 유지 관리되는 완전히 논리적인 디렉터리 구조입니다.  
  
-   Windows 공유를 통해 파일 또는 디렉터리를 만들거나 변경하려고 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에서 해당 호출을 가로채어 FileTable에 있는 해당 관계형 데이터에 반영합니다.  
  
-   Windows API 작업은 본질적으로 비트랜잭션이며 사용자 트랜잭션과 관련이 없습니다. 그러나 일반 테이블에 있는 FILESTREAM 열의 경우와 마찬가지로 FileTable에 저장된 FILESTREAM 데이터에 대한 트랜잭션 액세스도 완전히 지원됩니다.  
  
-   일반적인 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스를 통해 FileTable을 쿼리하고 업데이트할 수도 있습니다. 또한 FileTable은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구나 백업 등의 기능과 통합되어 있습니다.  

-   dbmail을 통해 메일 요청을 보내고 파일 스트림 디렉터리에 있는 파일을(따라서 filetable도) 첨부할 수 없습니다. 파일 시스템 필터 드라이버 RsFx0420은 파일 스트림 폴더로 입출력되는 들어오는 I/O 요청을 검사합니다. 요청이 SQLServer 실행 파일 및 Filestream 코드에서 시작되지 않은 경우 해당 요청은 명시적으로 허용되지 않습니다.
  
##  <a name="additional"></a> FileTable 사용에 대한 추가 고려 사항  
  
###  <a name="DBA"></a> 관리 고려 사항  
 **FILESTREAM 및 FileTable 정보**  
  
-   FileTable은 FILESTREAM과는 별도로 구성합니다. 따라서 비트랜잭션 액세스를 사용하도록 설정하거나 FileTable을 만들지 않고도 FILESTREAM 기능을 계속 사용할 수 있습니다.  
  
-   FileTable을 통하지 않고 FILESTREAM 데이터에 비트랜잭션 방식으로 액세스할 수 있는 방법은 없습니다. 따라서 비트랜잭션 액세스를 사용하도록 설정해도 기존 FILESTREAM 열 및 애플리케이션의 동작에는 영향이 없습니다.  
  
 **FileTable 및 비트랜잭션 액세스 정보**  
  
-   데이터베이스 수준에서 비트랜잭션 액세스를 사용하거나 사용하지 않도록 설정할 수 있습니다.  
  
-   데이터베이스 수준에서 비트랜잭션 액세스를 해제하거나 읽기 전용 또는 모든 읽기/쓰기 액세스를 허용하도록 설정하는 방법으로 비트랜잭션 액세스를 구성하거나 세부적으로 조정할 수 있습니다.  
   
###  <a name="memory"></a> FileTable은 메모리 매핑된 파일을 지원하지 않음  
 FileTable은 메모리 매핑된 파일을 지원하지 않습니다. 메모장과 그림판이 메모리 매핑된 파일을 사용하는 애플리케이션 중 가장 일반적인 두 가지 예입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같은 컴퓨터에서 이러한 애플리케이션을 사용하여 FileTable에 저장된 파일을 열 수 없습니다. 하지만 원격 컴퓨터 환경에서는 메모리 매핑된 기능을 사용하지 않으므로 원격 컴퓨터에서 이러한 애플리케이션을 사용하여 FileTable에 저장된 파일을 열 수 있습니다.  
   
##  <a name="reltasks"></a> 관련 작업  
 [FileTable의 필수 구성 요소를 사용하도록 설정](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
 FileTable을 만들고 사용하기 위한 필수 구성 요소를 사용하도록 설정하는 방법에 대해 설명합니다.  
  
 [FileTable 만들기, 변경 및 삭제](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
 새 FileTable을 만들거나 기존 FileTable을 변경 또는 삭제하는 방법에 대해 설명합니다.  
  
 [FileTable로 파일 로드](../../relational-databases/blob/load-files-into-filetables.md)  
 파일을 FileTable로 로드 또는 마이그레이션하는 방법에 대해 설명합니다.  
  
 [FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
 파일이 FileTable에 저장되는 디렉터리 구조에 대해 설명합니다.  
  
 [Transact-SQL을 사용하여 FileTable에 액세스](../../relational-databases/blob/access-filetables-with-transact-sql.md)  
 FileTable에서 Transact-SQL DML(데이터 조작 언어) 명령이 작동하는 방식에 대해 설명합니다.  
  
 [파일 입/출력 API를 사용하여 FileTable 액세스](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
 FileTable에서 파일 시스템 I/O가 작동하는 방식에 대해 설명합니다.  
  
 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)  
 FileTable을 관리하는 데 사용되는 일반적인 관리 태스크에 대해 설명합니다.  
  
##  <a name="relcontent"></a> 관련 내용  
 [FileTable Schema](../../relational-databases/blob/filetable-schema.md)  
 FileTable의 미리 정의된 고정 스키마에 대해 설명합니다.  
  
 [FileTable과 기타 SQL Server 기능 간 호환성](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)  
 FileTable이 SQL Server의 다른 기능과 함께 작동하는 방식에 대해 설명합니다.  
  
 [FileTable DDL, 함수, 저장 프로시저 및 뷰](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
 FileTable 기능을 지원하기 위해 추가되거나 변경된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체를 나열합니다.  

## <a name="see-also"></a>참고 항목
[Filestream 및 FileTable 동적 관리 뷰(Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 및 FileTable 카탈로그 뷰(Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Filestream 및 FileTable 시스템 저장 프로시저(Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)


  
  
