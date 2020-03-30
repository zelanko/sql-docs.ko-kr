---
title: FILESTREAM 데이터용 클라이언트 애플리케이션 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32
ms.assetid: 8a02aff6-e54c-40c6-a066-2083e9b090aa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 385deb9dd689c6716ab8addaa64d8bf8bd62ed97
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68085389"
---
# <a name="create-client-applications-for-filestream-data"></a>FILESTREAM 데이터용 클라이언트 애플리케이션 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Win32 API를 사용하여 FILESTREAM BLOB의 데이터를 읽고 쓸 수 있습니다. 다음 단계가 필요합니다.  
  
-   FILESTREAM 파일 경로를 읽습니다.  
  
-   현재 트랜잭션 컨텍스트를 읽습니다.  
  
-   Win32 핸들을 가져오고 이 핸들을 사용하여 FILESTREAM BLOB의 데이터를 읽고 씁니다.  
  
> [!NOTE]  
>  이 항목의 예에서는 [FILESTREAM 사용 데이터베이스 만들기](../../relational-databases/blob/create-a-filestream-enabled-database.md) 및 [FILESTREAM 데이터 저장용 테이블 만들기](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)에서 만든 FILESTREAM 사용 데이터베이스 및 테이블이 필요합니다.  
  
##  <a name="functions-for-working-with-filestream-data"></a><a name="func"></a> FILESTREAM 데이터 작업을 위한 함수  
 FILESTREAM을 사용하여 BLOB(Binary Large Object) 데이터를 저장하면 Win32 API를 사용하여 파일을 작업할 수 있습니다. Win32 애플리케이션에서의 FILESTREAM BLOB 데이터 작업을 지원하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 다음 기능과 API를 제공합니다.  
  
-   [PathName](../../relational-databases/system-functions/pathname-transact-sql.md) 은 BLOB에 대한 토큰으로 경로를 반환합니다. 애플리케이션은 이 토큰을 사용하여 Win32 핸들을 얻고 BLOB 데이터에 대한 작업을 수행합니다.  
  
     FILESTREAM 데이터가 포함된 데이터베이스가 Always On 가용성 그룹에 속하는 경우 PathName 함수가 컴퓨터 이름 대신 VNN(가상 네트워크 이름)을 반환합니다.  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) 는 세션의 현재 트랜잭션을 나타내는 토큰을 반환합니다. 애플리케이션은 이 토큰을 사용하여 FILESTREAM 파일 시스템 스트리밍 작업을 트랜잭션에 바인딩합니다.  
  
-   [OpenSqlFilestream API](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 는 Win32 파일 핸들을 얻습니다. 애플리케이션에서는 이 핸들을 사용하여 FILESTREAM 데이터를 스트리밍한 후 [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)또는 [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)같은 Win32 API 함수에 핸들을 전달합니다. 애플리케이션이 핸들을 사용하여 다른 API를 호출할 경우 ERROR_ACCESS_DENIED 오류가 반환됩니다. 애플리케이션에서는 [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428)을 사용하여 핸들을 종료해야 합니다.  
  
 모든 FILESTREAM 데이터 컨테이너 액세스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션에서 수행됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 SQL 데이터 및 FILESTREAM 데이터 간에 일관성을 유지할 수 있습니다.  
  
##  <a name="steps-for-accessing-filestream-data"></a><a name="steps"></a> FILESTREAM 데이터에 액세스하는 단계  
  
###  <a name="reading-the-filestream-file-path"></a><a name="path"></a> FILESTREAM 파일 경로 읽기  
 FILESTREAM 테이블의 각 셀에는 해당 셀과 연결된 파일 경로가 있습니다. 이러한 경로를 읽으려면 **문에 있는** varbinary(max) **열의** PathName [!INCLUDE[tsql](../../includes/tsql-md.md)] 속성을 사용합니다. 다음 예에서는 **varbinary(max)** 열의 파일 경로를 읽는 방법을 보여 줍니다.  
  
 [!code-sql[FILESTREAM#FS_PathName](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_1.sql)]  
  
###  <a name="reading-the-transaction-context"></a><a name="trx"></a> 트랜잭션 컨텍스트 읽기  
 현재 트랜잭션 컨텍스트를 가져오려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) 함수를 사용합니다. 다음 예에서는 트랜잭션을 시작하고 현재 트랜잭션 컨텍스트를 읽는 방법을 보여 줍니다.  
  
 [!code-sql[FILESTREAM#FS_GET_TRANSACTION_CONTEXT](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_2.sql)]  
  
###  <a name="obtaining-a-win32-file-handle"></a><a name="handle"></a> Win32 파일 핸들 가져오기  
 Win32 파일 핸들을 가져오려면 OpenSqlFilestream API를 호출합니다. 이 API는 sqlncli.dll 파일에서 내보내집니다. 다음 Win32 API 중 하나로 반환된 핸들이 전달될 수 있습니다. [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)또는 [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427). 다음 예에서는 Win32 파일 핸들을 가져오고 이를 사용하여 FILESTREAM BLOB의 데이터를 읽고 쓰는 방법을 보여 줍니다.  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/create-client-applicatio_3.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/create-client-applicatio_4.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/create-client-applicatio_5.cpp)]  
  
##  <a name="best-practices-for-application-design-and-implementation"></a><a name="best"></a> 애플리케이션 디자인 및 구현을 위한 최상의 방법  
  
-   FILESTREAM이 사용된 애플리케이션을 디자인하고 구현할 때는 다음 지침을 고려하십시오.  
  
-   초기화되지 않은 FILESTREAM 열을 나타내는 데 0x 대신 NULL을 사용합니다. 0x 값을 사용하면 파일이 생성되고, NULL을 사용했을 때는 그렇지 않습니다.  
  
-   null이 아닌 FILESTREAM 열이 포함된 테이블에 삽입 및 삭제 작업을 사용하지 마십시오. 삽입 및 삭제 작업은 가비지 수집에 사용되는 FILESTREAM 테이블을 수정할 수 있습니다. 그러면 시간이 지남에 따라 애플리케이션 성능이 저하됩니다.  
  
-   복제가 사용되는 애플리케이션에 NEWID() 대신 NEWSEQUENTIALID()를 사용합니다. NEWSEQUENTIALID()는 이런 애플리케이션에서 GUID를 생성하는 성능이 NEWID()보다 우수합니다.  
  
-   FILESTREAM API는 데이터에 대한 Win32 스트리밍 액세스를 위해 디자인되었습니다. 2MB가 넘는 FILESTREAM BLOB(Binary Large Object)을 읽거나 쓰는 데 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하지 마세요. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 BLOB 데이터를 읽거나 써야 하는 경우에는 Win32에서 FILESTREAM BLOB을 열기 전에 먼저 모든 BLOB 데이터가 사용되었는지 확인합니다. 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터가 사용되지 않은 경우 후속 FILESTREAM 열기 또는 닫기 작업이 실패할 수 있습니다.  
  
-   FILESTREAM BLOB에 데이터를 업데이트하거나 추가하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하지 마십시오. 이러한 문을 사용하면 BLOB 데이터가 tempdb 데이터베이스에 스풀링된 후 새 물리적 파일에 스풀링됩니다.  
  
-   소규모 BLOB 업데이트를 FILESTREAM BLOB에 추가하지 마십시오. 추가할 때마다 기본 FILESTREAM 파일이 복사됩니다. 애플리케이션이 소규모 BLOB을 추가해야 하는 경우에는 BLOB을 **varbinary(max)** 열에 쓴 후 BLOB 개수가 미리 지정된 한도에 도달하면 FILESTREAM BLOB에 대한 단일 쓰기 작업을 수행합니다.  
  
-   애플리케이션에서 다수의 BLOB 파일의 데이터 길이를 검색하지 마십시오. 데이터 크기는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 저장되지 않으므로 이 작업에는 시간이 많이 소요됩니다. BLOB 파일의 길이를 확인해야 한다면 BLOB이 닫혀 있는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] DATALENGTH() 함수를 사용하여 그 크기를 검토하세요. DATALENGTH()는 BLOB 파일 크기를 확인하기 위해 파일을 열지 않습니다.  
  
-   애플리케이션이 SMB1(메시지 블록 1) 프로토콜을 사용하는 경우 성능 최대화를 위해 FILESTREAM BLOB 데이터를 60KB의 배수로 읽어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [FILESTREAM 애플리케이션에서 데이터베이스 작업과의 충돌 방지](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)   
 [OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Binary Large Object &#40;Blob&#41; 데이터 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [FILESTREAM 데이터 부분 업데이트](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)  
  
  
